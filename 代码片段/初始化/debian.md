```bash
export http_proxy=http://192.168.31.40:7890
export https_proxy=http://192.168.31.40:7890

apt update
apt upgrade
apt install vim git curl wget

vi /etc/ssh/sshd_config
systemctl restart sshd
```

```bash
vi /etc/rc.local
chmod +x /etc/rc.local
reboot
```