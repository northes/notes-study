
```
docker save ${IMG} | bzip2 | ssh root@${HOST} docker load
```