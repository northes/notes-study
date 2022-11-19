https://jellyfin.org/downloads/docker

```shell
docker pull jellyfin/jellyfin:latest
mkdir -p /srv/jellyfin/{config,cache}
docker run -d -v /srv/jellyfin/config:/config -v /srv/jellyfin/cache:/cache -v /media:/media --net=host jellyfin/jellyfin:latest
```

```shell
docker run -d -v E:\Workspace\Jellyfin\config:/config -v E:\Workspace\Jellyfin\cache:/cache -v E:\Workspace\Jellyfin\media:/media -p 8096:8096 jellyfin/jellyfin:latest
```