## 激活

```bash
sudo fallocate -l 20G /mnt/.swapfile # 创建 20G 空文件
sudo mkswap /mnt/.swapfile    # 转换为交换分区文件
sudo chmod 600 /mnt/.swapfile # 修改权限为 600
sudo swapon /mnt/.swapfile    # 激活交换分区
free -m # 查看当前内存使用情况(包括交换分区)
```

## 停用

```bash
sudo swapoff /mnt/.swapfile
rm -rf /mnt/.swapfile
```