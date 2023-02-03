## 使用 Docker

```groovy
agent {
    docker {
        image 'gcr.io/kaniko-project/executor:debug'
        args "--entrypoint=''" // Jenkins 会先启动容器，并使用 cat 命令 hold 住，需使用 debug 的 Tag 的镜像，并修改 entrypoint
        label "agent-1"
    }
}
```


## Step

### 大段脚本

```
sh """
    # 构建镜像
    cd demo ;
    docker build -t demo/demo-web-app:1.1.1_xxxxxxxx1 . ;
    #docker push demo/demo-web-app:1.1.1_xxxxxxxx1 ;       
"""
```