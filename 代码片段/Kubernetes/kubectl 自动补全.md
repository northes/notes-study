```bash
apt-get install bash-completion
```

`~/.bashrc`

```
source /usr/share/bash-completion/bash_completion

alias k='kubectl'
source <(kubectl completion bash)
complete -F __start_kubectl k
```