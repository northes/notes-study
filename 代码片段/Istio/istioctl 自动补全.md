```bash
apt-get install bash-completion
```

`~/.bashrc`

```
source /usr/share/bash-completion/bash_completion

export PATH=$PATH:/root/workspace/istio-1.16.1/bin
alias i='istioctl'
source <(istioctl completion bash)
complete -F __start_istioctl i
```