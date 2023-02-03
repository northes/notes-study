## 使用 Docker

[镜像构建方式](../../开发/技术选型/容器.md#镜像构建方式)

使用 DooD 的方式，直接 debian 镜像手撸命令

### 插件 Docker Pipeline

- “文档” [docker-workflow-plugin/Docker.groovy at master · jenkinsci/docker-workflow-plugin · GitHub](https://github.com/jenkinsci/docker-workflow-plugin/blob/master/src/main/resources/org/jenkinsci/plugins/docker/workflow/Docker.groovy)

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