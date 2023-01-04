
## docker

### 命令

```shell
docker run -d  --name rabbitmq -e RABBITMQ_DEFAULT_USER=user -e RABBITMQ_DEFAULT_PASS=password -p 5671:5671 -p 5672:5672 -p 15672:15672 rabbitmq:management
```

### 镜像

rabbitmq:latest

不带web管理界面

rabbitmq:management

自带web管理界面

### 端口

5671
5672
15672：管理界面

> 默认管理账号密码：guest/guest

