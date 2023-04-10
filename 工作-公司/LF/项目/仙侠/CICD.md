## Jenkins

```groovy
pipeline{
    agent none
    stages{
        stage('Prepare and Build') {
            agent {
                docker {
                    image 'szyhf/golang:alpine'
                    label 'agent-1'
                }
            }
            environment {
                SKIP_UPDATE_TOOLS = 'true'

                // 如要修改缓存路径，需同时修改所有阶段的 GOPATH
                GOPATH = "${WORKSPACE}/.go"
                GOMODCACHE = "${WORKSPACE}/.go/pkg/mod"
                GOCACHE = "${WORKSPACE}/.go/.cache/go-build"
                GOLANGCI_LINT_CACHE = "${WORKSPACE}/.go/.cache/golangci-lint"
                GOPROXY = 'https://goproxy.cn,direct'
                GOPRIVATE = 'gitlab.shouyouqianxian.com'
            }
            steps {
                echo WORKSPACE
                // 使用凭证拉取私有仓库
                sshagent (credentials: ["xia-deployer-ssh_private_key"]) {
                    sh """
                        mkdir -p /root/.ssh
                        chmod 700 /root/.ssh
                        ssh-keyscan gitlab.shouyouqianxian.com > /root/.ssh/known_hosts;
                        ssh -T git@gitlab.shouyouqianxian.com;
                        go env;
                        go install gitlab.shouyouqianxian.com/bingo/bing@master;

                        # 下载game_server_proto
                        rm -rf $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server_proto;
                        mkdir -p $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server_proto;
                        git archive --remote git@gitlab.shouyouqianxian.com:xia/game_server_proto.git master | tar -x -C $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server_proto;

                        # 下载game_server
                        rm -rf $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server;
                        git clone --depth=1 -b ${params.GAME_BRANCH} git@gitlab.shouyouqianxian.com:xia/game_server.git $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server;
                        cd $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server ;
                        go work init ;
                        go work use $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server_proto ;
                        chmod +x ./update.sh ;
                        ./update.sh -gd=${params.GAME_PLATFORM}

                        # 构建并生成 kaniko 脚本
                        cd $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server ;
                        chmod +x ./docker/push/auto.sh ;
                        ./docker/push/auto.sh ${params.GAME_PLATFORM},${params.GAME_MODE},${params.GAME_SERVER_TYPE} dabai=${params.DABAI_ATTER} kaniko;
                    """                   
                }
            }
        }
        stage('Push') {
            agent {
                docker {
                    image 'gcr.io/kaniko-project/executor:debug'
                    args "--entrypoint=''" // Jenkins 会先启动容器，并使用 cat 命令 hold 住，需使用 debug 的 Tag 的镜像，并修改 entrypoint
                    label "agent-1"
                }
            }
            environment {
                CI_PROJECT_DIR = "${GOPATH}/src/gitlab.shouyouqianxian.com/xia/game_server"
                CI_COMMIT_BRANCH = "${GAME_BRANCH}"
                KANIKO_AUTH_FILE = credentials('xia-deployer-kaniko.config.json')
                GOPATH = "${WORKSPACE}/.go"
            }
            steps {
                sh """
                    cat $KANIKO_AUTH_FILE > /kaniko/.docker/config.json ; # auth 不需要 https 开头
                    cd $GOPATH/src/gitlab.shouyouqianxian.com/xia/game_server ;
                    chmod +x ./kaniko.sh ;
                    ./kaniko.sh 
                """
            }
        }
    }
    post {
        success {
            echo '构建成功！🎉🎉'
        }
        failure {
            echo '构建失败，请检查！🙈'
        }
    }
}
```