```bash
docker run -d \
  --name=transmission \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Asia/Shanghai \
  -e TRANSMISSION_WEB_HOME=/transmissionic/ `#optional` \
  -e USER=username `#optional` \
  -e PASS=password `#optional` \
  -e WHITELIST=iplist `#optional` \
  -e PEERPORT=peerport `#optional` \
  -e HOST_WHITELIST=dnsname list `#optional` \
  -p 9091:9091 \
  -p 51413:51413 \
  -p 51413:51413/udp \
  -v /path/to/data:/config \
  -v /path/to/downloads:/downloads \
  -v /path/to/watch/folder:/watch \
  --restart unless-stopped \
  linuxserver/transmission:latest
```


## 报错

- 在Homelab中通过homelab账号，SMB协议挂载的路径，会报错权限不足，将环境变量中的PUID和PGID修改为0即可
- 下载一直没速度，检查tracker站是否可以不翻墙访问，如果不是，上代理