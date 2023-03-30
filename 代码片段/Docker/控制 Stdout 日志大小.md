docker 容器的控制台输出都会保存到 `/var/lib/docker/containers/<id>/<id>-logs.json` 中，过大的日志保存记录会导致磁盘占用过大，通过控制日志记录大小以使其保持在合理范围内

- 修改后仅对新容器生效
- 超过大小的日志文件会被覆盖重写


## 全局

`/etc/docker/daemon.json`

```json
{
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "10m",
    "max-file": "3" 
  }
}
```

## 单个容器

```bash
docker run \
      --log-driver json-file --log-opt max-size=10m \
      alpine echo hello world
```

## Docker-compose

```yaml
version: '3'
services:
  redis:
    image: redis:5.0
    restart: always
    container_name: IP20-redis-6378
    environment:
    - TZ=Asia/Shanghai
    ports:
    - 6378:6378
    volumes:
    - ./redis.conf:/etc/redis/redis.conf
    command: redis-server /etc/redis/redis.conf
    logging:
	  driver: "json-file" # none 不记录 stdout
	  options: 
		max-size: "5g"
```

## 参考

- [JSON File logging driver](https://docs.docker.com/config/containers/logging/json-file/)