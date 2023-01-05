
## 创建特权容器

![](assets/Pasted%20image%2020230105221858.png)

## 配置 LXC

宿主机中编辑 LXC 配置文件，需将 LXC 关机

`vi /etc/pve/lxc/[id].conf`

```
lxc.apparmor.profile: unconfined
lxc.cgroup.devices.allow: a
lxc.cap.drop:
lxc.mount.auto: "proc:rw sys:rw"
```

## LXC 内创建脚本

`/etc/rc.local`

```
#!/bin/sh -e

# Kubeadm 1.15 needs /dev/kmsg to be there, but it's not in lxc, but we can just use /dev/console instead
# see: https://github.com/kubernetes-sigs/kind/issues/662
if [ ! -e /dev/kmsg ]; then
    ln -s /dev/console /dev/kmsg
fi

# https://medium.com/@kvaps/run-kubernetes-in-lxc-container-f04aa94b6c9c
mount --make-rshared /
```


授权并重启

```shell
chmod +x /etc/rc.local
reboot
```

## 正常安装 K3s

```shell
# 通用
curl -sfL https://get.k3s.io | sh -
# 国内
curl -sfL https://rancher-mirror.rancher.cn/k3s/k3s-install.sh | INSTALL_K3S_MIRROR=cn sh -
```

## 参考

- [Site Unreachable](https://gist.github.com/triangletodd/02f595cd4c0dc9aac5f7763ca2264185)