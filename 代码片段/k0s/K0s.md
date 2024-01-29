```bash
# 指定版本 K0S_VERSION=v1.28.6+k0s.0 
# Debug等级日志 DEBUG=true	
curl -sSLf https://get.k0s.sh | sudo DEBUG=true sh
sudo k0s sysinfo
sudo k0s install controller --single
sudo k0s start
sudo k0s status
watch 'k0s kubectl get pods --all-namespaces'
```

## 架构

- [Architecture - Documentation](https://docs.k0sproject.io/v1.28.6+k0s.0/architecture/)


## 配置文件

详解：[Configuration Options - Documentation](https://docs.k0sproject.io/head/configuration/)

```bash
# 验证配置
k0s validate config --config path/to/config/file
```

## 本地负载均衡器

- [Node-local load balancing - Documentation](https://docs.k0sproject.io/v1.28.6+k0s.0/nllb/)

## Q&A

### 获取不到 controller 节点

```bash
kubectl get no
# 仅仅列出 worker 节点
```

默认情况下，控制平面根本不运行 kubelet，并且不接受任何工作负载，因此控制器不会显示在 kubectl 的节点列表中。如果希望控制器接受工作负载并运行 Pod，请使用： `k0s controller --enable-worker` （建议仅作为 test/dev/POC 环境）。