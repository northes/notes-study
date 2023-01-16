```bash
apt-get install bash-completion
```

`.bashrc`

```
source /usr/share/bash-completion/bash_completion

alias k='kubectl'
source <(kubectl completion bash)
complete -F __start_kubectl k

export PATH=$PATH:/root/workspace/istio-1.16.1/bin
alias i='istioctl'
source <(istioctl completion bash)
complete -F __start_istioctl i

alias h='helm'
source <(helm completion bash)
complete -F __start_helm h
```