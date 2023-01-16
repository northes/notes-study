## 网络

如本地已有 mysql 、redis ，需要加入网络，参考下文

[更换网络](../Docker/更换网络.md)

## 项目配置文件

加入网络后，项目配置文件数据库地址直接填 mysql:3306 或 redis:6379 即可

## 参考

```yaml
version: '3.6'
services:
  game:
    image: golang:1.19-alpine
    volumes:
      - /Users/mac/go:/go
      - /Users/mac/Library/Caches/go-build:/root/.cache/go-build
      - /Users/mac/go/src/gitlab.shouyouqianxian.com/xia/game_server/conf/game:/go/src/gitlab.shouyouqianxian.com/xia/game_server/conf
    networks:
      - web
      - default
    working_dir: 
      /go/src/gitlab.shouyouqianxian.com/xia/game_server
    ports:
      - 8080:8080
      - 18080:18080
    command: 
      - go
      - run
      - --tags=wx_mini,dev,game
      - main.go
  rank:
    image: golang:1.19-alpine
    volumes:
      - /Users/mac/go:/go
      - /Users/mac/Library/Caches/go-build:/root/.cache/go-build
      - /Users/mac/go/src/gitlab.shouyouqianxian.com/xia/game_server/conf/rank:/go/src/gitlab.shouyouqianxian.com/xia/game_server/conf
    networks:
      - web
      - default
    working_dir: 
      /go/src/gitlab.shouyouqianxian.com/xia/game_server
    command: 
      - go
      - run
      - --tags=wx_mini,dev,rank
      - main.go
networks:
  web:
    external: true
```