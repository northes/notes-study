
## 官网

https://www.rancher.cn/k3s/

## kube 配置文件

复制配置文件到默认路径

```shell
cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
```

## k3s 配置文件

`/ect/rancher/k3s/config.yaml`

```yaml
disable: traefik,metrics-server
```

## 重启

```shell
# Server || 单节点 
sudo systemctl restart k3s 
# Agent 
sudo systemctl restart k3s-agent
```

## 负载均衡

- [Site Unreachable](https://github.com/k3s-io/klipper-lb)