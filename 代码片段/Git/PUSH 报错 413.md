
```
error: RPC failed; HTTP 413 curl 22 The requested URL returned error: 413
send-pack: unexpected disconnect while reading sideband packet
fatal: the remote end hung up unexpectedly
```

检查 git 服务前面是否有 nginx 等网关，如果有，则需要调整最大允许的请求大小


### 例子

以下为私有化部署的Gitea在推送大文件时遇到的这个问题，通过在 ingress 注解中添加

```yaml
  annotations:   
    nginx.ingress.kubernetes.io/proxy-body-size: "100M"
```

解决