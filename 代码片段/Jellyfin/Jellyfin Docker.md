❗❗❗
如需挂载 NAS 中文件，需提前设置好共享目录与权限，并启动 SMB 服务（或其他）
[挂载远端 SMB 目录](../Linux/挂载远端%20SMB%20目录.md)

## 官方

https://jellyfin.org/downloads/docker

```shell
docker pull jellyfin/jellyfin:latest

mkdir -p /srv/jellyfin/{config,cache}

docker run -d --name jellyfin \
-v /root/jellyfin_data/config:/config \
-v /root/jellyfin_data/cache:/cache \
-v /media:/media \
--net=host \
-p 8096:8096 \
-p 8920:8920 \
jellyfin/jellyfin:latest
```

## 第三方

```
nyanmisaka/jellyfin:latest
```

## 添加代理

添加环境变量

```
http_proxy=http://192.168.31.40:7890
https_proxy=http://192.168.31.40:7890
```