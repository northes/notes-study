## 私有仓库配置

`/etc/rancher/k3s/registries.yaml`

```yaml
mirrors:
  hub.northes.io:
    endpoint:
      - "http://192.168.31.5:5050"
  docker.io:
    endpoint:
      - "http://192.168.31.5:5050"
  ghcr.io:
    endpoint:
      - "http://192.168.31.5:5050"
  quay.io:
    endpoint:
      - "http://192.168.31.5:5050"
```