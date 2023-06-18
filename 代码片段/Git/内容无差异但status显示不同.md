```bash
# 修改换行符配置
# 提交时转换为LF(Linux)，检出时不转换
git config --global core.autocrlf input
# 拒绝提交包含混合换行符的文件
git config --global core.safecrlf true
# 忽略文件权限差异
git config core.filemode false
```