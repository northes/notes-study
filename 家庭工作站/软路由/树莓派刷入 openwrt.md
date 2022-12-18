## 下载固件

### 第三方固件

https://doc.openwrt.cc/2-OpenWrt-Rpi/

https://openwrt.cc/releases/targets/bcm27xx/bcm2711/

### 官方固件

https://firmware-selector.openwrt.org/?version=22.03.2&target=bcm27xx%2Fbcm2711&id=rpi-4

## 刷入固件

可以使用树莓派官方的镜像输入工具进行刷入

或者 `win32 disk imager`

## 设置静态IP

openwrt 默认地址为 192.168.1.1

将tf卡插入树莓派后，使用网线连接树莓派与电脑

浏览器输入 192.168.1.1 访问成功即表示系统已成功启动（如果树莓派的红灯和绿灯还在交替闪烁，证明还在初始化，等红灯常亮时再试试）

> 默认账号密码
> root
> password （或空）

通过 ssh 修改静态ip

```shell
uci set network.lan.ipaddr=192.168.31.2
uci commit network  
/etc/init.d/network restart
```

> 注意，ip需要修改为与欲接入的上级路由处于同一个网段
> 如 上级路由为 192.168.31.1 ，则网段为 192.168.31.x

修改后，拔出并重新插入连接到电脑的网线，通过修改后的ip访问

### 关闭桥接

在 接口 - LAN - 物理设置 下

取消勾选 桥接接口

并选择 以太网适配器 "eth0"

### 修改 Lan 口参数

![](Pasted%20image%2020221217224516.png)

网络 > 接口 > 找到对应的Lan口进行编辑

- 协议：静态地址
- IPV4地址：192.168.31.2 （保持不变）
- 网关：填写上级路由IP，如 192.168.31.1
- 广播：将上级路由网段的最后一段改为 255，如192.168.31.255
- DNS地址：192.168.31.1（或者其他）
- 忽略此接口/不在此接口提供 DHCP 服务：勾选

修改后点击 确认并应用

应用成功后拔下网线，并插入上级路由中，此时，已经可以用刚才修改的静态ip进行访问了