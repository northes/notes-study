释放 53 端口

# 停止

## 检查端口

```
lsof -i :53
```

## 修改配置

`/etc/systemd/resolved.conf`

```
# 放开 DNS= 和 DNSStubListener 的注释
# 设置

DNS=127.0.0.1
DNSStubListener=no
```

## 建立软链接

```bash
ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf
```

## 重启

```bash
reboot
```

# 重新启用

`/etc/systemd/resolved.conf`

```
# 注释
DNS=
DNSStubListener=no
```

移除软链接

```bash
rm /etc/resolv.conf
```

重启

```bash
reboot
```