
## Docker

```bash
docker run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
```

```bash
docker run -itd --name mysql -p 3306:3306 -v /Users/mac/datas/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 mysql:5.7
```

> ARM 结构使用 bitnami/mysql

## Podman

```bash
podman run -e MYSQL_ROOT_PASSWORD=123456 -v /root/datas/mysql_data:/bitnami/mysql/data --name mysql -p 3306:3306 bitnami/mysql:5.7
```