青龙面板

```shell
docker run -dit -v $PWD/data:/ql/data -p 5700:5700 --name qinglong --hostname localhost --restart unless-stopped whyour/qinglong:latest
```