[镜像加速](../Linux/debian/镜像加速.md)

## 安装基础工具

```bash
apt-get install \
    ca-certificates \
    curl \
    gnupg \
    lsb-release
```

## 添加 GPG

```bash
mkdir -m 0755 -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/debian/gpg | gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

## 添加仓库

```bash

```