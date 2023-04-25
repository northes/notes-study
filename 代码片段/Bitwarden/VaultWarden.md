
自部署服务端的第三方开源实现

```bash
docker pull vaultwarden/server:latest
docker run -d --name vaultwarden -v /root/vaultWarden_data/:/data/ -p 8080:80 --restart always vaultwarden/server:latest
```