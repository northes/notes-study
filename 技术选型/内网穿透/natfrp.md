```yaml
version: '3'
services:
  launcher:
    image: natfrp/launcher:latest
    restart: always
    ports:
      - "4101:4101"
    volumes:
      - xxx:/run/FrpcWorkingDirectory
```


## 配置https

1. 管理后台创建 HTTPS 类型的隧道
2. 自动 HTTPS 填写绑定的域名
	![](assets/Pasted%20image%2020231123115759.png)
3. 激活隧道
4. 申请证书 （腾讯云）
5. 下载 nginx 格式证书
6. 前往本地配置的 volumes 内，此时应该可以看到出现了对应域名的 frp 自签证书，将自签证书替换为申请到的证书
7. 重启隧道
8. 完成，可通过 https 访问