## 部署

```
docker run -d \
  --name=qbittorrent \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Asia/Shanghai \
  -e WEBUI_PORT=8081 \
  -p 8081:8081 \
  -p 6881:6881 \
  -p 6881:6881/udp \
  -v /root/qbittorrent_data/config:/config \
  -v /root/qbittorrent_data/downloads:/downloads \
  --restart unless-stopped \
  linuxserver/qbittorrent:latest
```

## 账号

默认账号 `admin` 密码 `adminadmin`

## 设置

### 连接

- 监听端口：随机
- 勾选使用映射自路由的 UPnP ...

### BitTorrent

- 加密模式：强制加密