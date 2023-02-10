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
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" | tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## 安装

```bash
apt-get update && apt-get install docker-ce-cli
```