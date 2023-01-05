## 安装

ssh 分为 client 和 server，首先检查是否安装并开启了 ssh server


```shell
# 查看已安装的包
dpkg -l|grep ssh
# 安装server
apt-get install openssh-server
yum install openssh-server
# 安装client，如需
apt-get install openssh-client
```

安装好后再次检查已安装的包，成功安装后检查是否运行

```shell
ps -e|grep ssh
```

有 sshd 则表示成功运行

如果每次可以通过以下方式启动

```shell
sudo /etc/init.d/ssh start

sudo service ssh start
```

## 配置

### 配置文件

`/etc/ssh/sshd_config`

### 允许 root 用户以任何方式登录

```
#修改如下内容 设置PermitRootLogin 其他的配置默认是不开启root访问的
PermitRootLogin yes
```

重启服务

```shell
sudo service sshd restart
# or
sudo systemctl restart sshd
```

### 修改端口

在配置文件中修改

```
Port 10022
```