## 安装必要工具

```bash
apt-get install cifs-utils vim
```

## 挂载

```bash
mount -t cifs <共享点路径> <挂载点> -o username=<用户名>,password=<密码>
```

## 例子

```bash
mount -t cifs \\192.168.31.5/video /tmp/nas -o username=<用户名>

# 报错 mount.cifs: bad UNC (\192.168.31.5) 时尝试
mount -t cifs //192.168.31.5/video /tmp/nas -o username=<用户名>

# 报错
# mount error(22): Invalid argument
# Refer to the mount.cifs(8) manual page (e.g. man mount.cifs) and kernel log messages (dmesg)
# 时，检查共享点是否缺少具体路径，如 //192.168.31.5/video 而不是 //192.168.31.5
```

## 开机自动挂载

[开机自动挂载](开机自动挂载.md)