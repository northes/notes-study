
## docker

```bash
docker run --name redis -p 6379:6379 -d redis
```

## bitnami/redis

```bash
docker run -d --name redis \
	-p 6379:6379 \
    -e ALLOW_EMPTY_PASSWORD=yes \
    -v /path/to/redis-persistence:/bitnami/redis/data \
    bitnami/redis:latest
```

```bash
docker run -d --name redis\
-p 6379:6379 \
    -e ALLOW_EMPTY_PASSWORD=yes \
    -v /Users/mac/datas/redis/data:/bitnami/redis/data \
    bitnami/redis:latest
```

## podman

```bash
podman run -e ALLOW_EMPTY_PASSWORD=yes -v /root/datas/redis_data:/bitnami/redis/data --name redis -p 6379:6379 bitnami/redis:latest
```