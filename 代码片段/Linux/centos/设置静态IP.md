
```shell
vim /etc/sysconfig/network-scripts/ifcfg-eth0
```

```yaml
BOOTPROTO="static" #dhcp改为static 
ONBOOT="yes" #开机启用本配置
IPADDR=192.168.7.106 #静态IP
GATEWAY=192.168.7.1 #默认网关
NETMASK=255.255.255.0 #子网掩码
DNS1=192.168.7.1 #DNS 配置
```

修改后重启网络

```shell
systemctl restart network
```

查看变化

```shell
ip addr
```
