
1. 设置

```shell
## '16.x' 不需要改，就是.x结尾
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash -

curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
```

2. 安装

此时经过上一步的操作，将会安装到指定版本，否则安装的版本会很低

```shell
apt-get install -y nodejs
```

3. 检验

```shell
node --version
```