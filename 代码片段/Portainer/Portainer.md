```shell
docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /volume1/data/portainer_data:/data \
    portainer/portainer-ce:latest
```

`portainer/portainer-ee:latest` 为商业版

汉化版

```shell
docker run -d -p 8000:8000 -p 9443:9443 --name=portainer --restart=always \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -v /root/portainer_data:/data \
    6053537/portainer-ce:latest
```