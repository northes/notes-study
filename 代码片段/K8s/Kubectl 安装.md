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
