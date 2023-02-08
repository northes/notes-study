
```bash
docker run -d \
    --name embyserver \
    --volume /data/emby_data/config:/config \
    --volume /video:/media \
    --net=host \
    --device /dev/dri:/dev/dri \
    --publish 8096:8096 \
    --publish 8920:8920 \
    --env UID=1000 \
    --env GID=100 \
    --env GIDLIST=100 \
    emby/embyserver:latest
```