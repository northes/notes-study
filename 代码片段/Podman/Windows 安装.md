
## 报错

Error: the WSL import of guest OS failed: exit status 0xffffffff

1. 开启 Hyper-V 功能，重启
2. 删除已创建的 WSL [删除WSL机器](../WSL/常用命令.md)
3. 重新创建 WSL `podman machine init`