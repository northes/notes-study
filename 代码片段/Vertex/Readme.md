## 使用 Docker 运行

```bash
docker pull lswl/vertex-base:latest
```

```bash
docker run -d \
  --name vertex \
  -v /root/vertex:/vertex \
  -p 3000:3000 \
  -e TZ=Asia/Shanghai \
  --restart unless-stopped \
  lswl/vertex:stable
```