## 官网

- [OrbStack · Fast, light, simple Docker & Linux on macOS](https://orbstack.dev/)

Docker Desktop 的直接替代品

## 使用

直接启动 OrbStack

## 常见问题

- [Frequently asked questions · OrbStack Docs](https://docs.orbstack.dev/faq#diff-docker)

### 返回使用 Docker Desktop

```bash
docker context use desktop-linux
```

### 无法连接到位于 unix://.orbstack/run/docker.sock 的 Docker 守护进程

1. 启动 OrbStack

或

刚刚卸载了 OrbStack，将 `context` 切换回 `default`

```
docker context use default
``` 