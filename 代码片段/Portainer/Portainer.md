```shell
docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /data/portainer_data:/data \
    portainer/portainer-ee:latest
```

`portainer/portainer-ce:latest` 为商业版

汉化版

```shell
docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /root/portainer_data:/data \
    6053537/portainer-ce:latest
```