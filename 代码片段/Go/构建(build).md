```bash
CGO_ENABLE=0 GOARCH=amd64 GOOS=linus go build -ldflags "-s -w -extldflags '-static'" -o ./app
```

`CGO_ENABLE=0`：关闭 `CGO`

`GOARCH`：指定构建架构

`GOOS`：指定构建系统

`-ldflags`：linking flags 链接标志
  - `-s -w`：用于从二进制文件中删除调试信息
  - `-extldflags '-static'`：使用静态链接二进制文件，即使启用了 `CGO`，动态链接使我们的二进制文件需要外部库(Linux中的.so文件)。可以通过对二进制文件使用 `ldd` 命令来检查外部库依赖关系。在 `scratch`、`alpine` 中，我们没有安装这些库。在这种情况下，我们必须使用静态链接 -- 所有库都将编译到我们程序的二进制文件中。

## 相关工具

upx 压缩二进制文件 [upx](../UPX/upx.md)