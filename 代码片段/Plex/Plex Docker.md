一个自部署的影音服务器

[GitHub - plexinc/pms-docker: Plex Media Server Docker repo, for all your PMS docker needs.](https://github.com/plexinc/pms-docker)

## host network

```
docker run \
-d \
--name plex \
--network=host \
-e TZ="<timezone>" \
-e PLEX_CLAIM="<claimToken>" \
-v <path/to/plex/database>:/config \
-v <path/to/transcode/temp>:/transcode \
-v <path/to/media>:/data \
plexinc/pms-docker
```

## bridge network

```
docker run \
-d \
--name plex \
-p 32400:32400/tcp \
-p 8324:8324/tcp \
-p 32469:32469/tcp \
-p 1900:1900/udp \
-p 32410:32410/udp \
-p 32412:32412/udp \
-p 32413:32413/udp \
-p 32414:32414/udp \
-e TZ="<timezone>" \
-e PLEX_CLAIM="<claimToken>" \
-e ADVERTISE_IP="http://<hostIPAddress>:32400/" \
-h <HOSTNAME> \
-v <path/to/plex/database>:/config \
-v <path/to/transcode/temp>:/transcode \
-v <path/to/media>:/data \
plexinc/pms-docker
```