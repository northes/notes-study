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


默认账号 `admin` 密码 `adminadmin`