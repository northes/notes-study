## Delve

```bash
https://github.com/go-delve/delve
```

## 安装

```bash
go install github.com/go-delve/delve/cmd/dlv@latest
```

## 运行

```bash
# 当前处于入口文件（main）目录
dlv debug
# 指定入口文件或目录
dlv debug github.com/xx/foo/bar
dlv debug github.com/xx/foo/bar/main.go
# 传递参数运行
dlv debug github.com/xx/foo/bar -- -arg1 value
# 使用tag构建
dlv debug github.com/xx/foo/bar --build-flags="-tags=xx,yy,zz"
```

```bash
# 运行测试
dlv test
# 运行二进制文件
dlv exec
# 附加到正在运行的进程上
dlv attach
```

## 命令

| 命令            | 解释                                 | 示例                                        |
|:--------------- |:------------------------------------ |:------------------------------------------- |
| help            | 查看帮助                             |                                             |
| funcs           | 搜索函数，可指定包名，正则表达式匹配 | `funcs: test.Test*`                         |
| break(b)        | 设置断点                             | `b main.main`,在 `main.main` 函数处设置断点 |
| breakpoints(bp) | 查看断点信息                         |                                             |
| continue(c)     | 继续执行，直到下一个断点或结束       |                                             |
| next(c)         | 执行代码下一行,不会进入函数内部      |                                             |
| step(s)         | 单步执行,会进入函数内部按行执行      |                                             |
| stepout(so)     | 跳回到调用当前函数的地方             |                                             |
| restart(r)      | 重新运行                             |                                             |
| gr              | 查看goroutine                        |                                             |
| grs             | 查看所有goroutine                    |                                             |
| list(ls)        | 查看源代码                           | `ls main.main`、`ls main.go:17`             |
| exit(q)         | 退出                                 |                                             |
| clear           | 清除指定断点名或id                   | `clear 1`                                   |
| clearall        | 清除所有断点                         |                                             |
| locals          | 参看当前局部变量                     |                                             |


## 例子

```bash
# 查看本地变量
locals
# 打印，可以打印变量或结构体(通过locals或者args查看到变量名，如 req)
print req
```