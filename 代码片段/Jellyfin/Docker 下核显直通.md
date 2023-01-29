
## 1. 将核显直通到 LXC 中

[LXC 直通核显](../PVE/LXC%20直通核显.md)

## 2. 将核显直通到 Docker 中

命令行中加入

```bash
docker run ...
--device=/dev/dri/renderD128 \ #映射核显驱动
...
jellyfin/jellyfin
```

或

Portainer

![](assets/Pasted%20image%2020230129121902.png)

## 3. 设置 Jellyfin

![](assets/Pasted%20image%2020230129121953.png)

打开以提高兼容性

![](assets/Pasted%20image%2020230129122016.png)