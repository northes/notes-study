


系统 `Windows11`

1. Windows 安全中心-重新打开内核隔离

![](assets/Pasted%20image%2020230426231255.png)


2. 设置-应用-可选功能-更多Windows功能

- Hyper-V
- Windows 沙盒
- Windows 虚拟机监控程序平台
- 适用于 Linux 的 Windows 子系统
- 虚拟机平台

3.  执行命令

```
bcdedit /set hypervisorlaunchtype auto
```

4. 重启