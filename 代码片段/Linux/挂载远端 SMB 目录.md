安装必要工具

```
apt-get install cifs-utils vim
```

挂载

```
mount -t cifs <共享点路径> <挂载点> -o username=<用户名>,noserverino
```

例子

```
mount -t cifs \\192.168.31.5 /tmp/nas -o username=<用户名>
```