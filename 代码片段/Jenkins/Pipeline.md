## 使用 Docker

DooD（Docker outside of Docker）


- [pipeline中使用docker-脚本小站](https://www.scriptjc.com/article/1224)
- [Jenkins-pipeline-Docker 实现CI/CD](https://chinalhr.github.io/post/jenkins-java-ci-cd/)
- [用安装在 Docker 中的 jenkins 运行 Docker 任务](https://www.up4dev.com/2018/11/27/run-docker-by-jenkins-in-docker/)

## Step

### 大段脚本

```
sh """
    #构建镜像
    cd demo
    docker build -t demo/demo-web-app:1.1.1_xxxxxxxx1 .
    #docker push demo/demo-web-app:1.1.1_xxxxxxxx1              
"""
```