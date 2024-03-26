```bash
CGO_ENABLE=0 GOARCH=amd64 GOOS=linus go build -ldflags "-s -w -extldflags '-static'" -o ./app
```

`CGO_ENABLE=0`：关闭 `CGO`

`GOARCH`：指定构建架构

`GOOS`：指定构建系统

`-ldflags`：linking flags 链接标志
  - `-s -w`：用于从二进制文件中删除调试信息
  - `-extldflags '-static'`：使用静态链接二进制文件，即使启用了 `CGO`，动态链接使我们的二进制文件需要外部库(Linux中的.so文件)。可以通过对二进制文件使用 `ldd` 命令来检查外部库依赖关系。在 `scratch`、`alpine` 中，我们没有安装这些库。在这种情况下，我们必须使用静态链接 -- 所有库都将编译到我们程序的二进制文件中。

`-n`：加入 `-n` 标志打印详细的编译过程

`-work`：指示编译器编译完成后保留编译临时工作目录

`-a`：强制编译所有包

`-p`：指定编译过程中的线程数

## 相关工具

upx 压缩二进制文件 [upx](../UPX/upx.md)

## 相关文章

gccgo 使用 gcc 实现的编译器 [Setting up and using gccgo - The Go Programming Language](https://go.dev/doc/install/gccgo)

Go 自举(Bootstrapping)设计文档 [Go 1.3+ Compiler Overhaul - Google 文档](https://docs.google.com/document/d/1P3BLR31VA8cvLJLfMibSuTdwTuF7WWLux71CYD0eeD8/edit?pli=1)