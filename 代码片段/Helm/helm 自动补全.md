```bash
apt-get install bash-completion
```

`~/.bashrc`

```
source /usr/share/bash-completion/bash_completion

alias h='helm'
source <(helm completion bash)
complete -F __start_helm h
```