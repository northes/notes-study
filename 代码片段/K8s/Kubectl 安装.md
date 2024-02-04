## 安装 

- [Install and Set Up kubectl on Linux | Kubernetes](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)

## 自动补全

```bash
apt-get install bash-completion

# bash
echo 'source <(kubectl completion bash)' >>~/.bashrc

# 别名
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc

source ~/.bashrc
```

## kubeconfig

默认情况下 ，`kubectl` 在 `$HOME/.kube` 目录下查找名为 `config` 的文件。同时可以通过设置 `KUBECONFIG` 环境变量或者 `--kubeconfig` 显式指定 kubeconfig 文件。

### 多集群访问

[配置对多集群的访问 | Kubernetes](https://kubernetes.io/zh-cn/docs/tasks/access-application-cluster/configure-access-multiple-clusters/)

[使用 kubeconfig 文件组织集群访问 | Kubernetes](https://kubernetes.io/zh-cn/docs/concepts/configuration/organize-cluster-access-kubeconfig/)