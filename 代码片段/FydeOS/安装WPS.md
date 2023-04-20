## 下载

[WPS Office 2019 for Linux-支持多版本下载\_WPS官方网站](https://linux.wps.cn/)

## 初始化环境

```bash
sudo apt update -y
sudo apt install nemo
# 安装下载下来的 deb
sudo dpkg -i wps.xxx.deb
wget http://ftp.br.debian.org/debian/pool/contrib/m/msttcorefonts/ttf-mscorefonts-installer_3.7_all.deb
sudo dpkg -i ttf-mscorefonts-installer_3.7_all.deb
sudo apt -f install
```

## 设置中文

```bash
# 安装中文字体
sudo apt install fonts-wqy-microhei fonts-wqy-zenhei
# 修改语言环境
sudo dpkg-reconfigure locales
# zh_CN.UTF-8
# 回车跳到下一个界面继续选择 zh_CN.UTF-8
sudo reboot
```

宿主机也重启下

Done!