## 列出 controller 节点

```bash
k0s etcd member-list
```

## 移除 controller 节点 

```bash
# First, list the Etcd members
k0s etcd member-list
{"members":{"controller01":"<PEER_ADDRESS1>", "controller02": "<PEER_ADDRESS2>", "controller03": "<PEER_ADDRESS3>"}}
# Then, remove the controller01 using its peer address
k0s etcd leave --peer-address "<PEER_ADDRESS1>"
```

## 创建配置文件

```bash
k0s config create > /etc/k0s/k0s.yaml
k0sctl init > k0sctl.yaml
```