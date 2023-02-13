## 插件启动异常

1.  前往系统管理页面，查看是否需要升级。由于 Docker 镜像存在滞后的问题，因此需要启动后再手动更新一下系统
2.  勾选全部插件，更新
3.  重启

## 警告在主节点构建的安全问题

```bash
Building on the built-in node can be a security issue. You should set the number of executors on the built-in node to 0. See the documentation.
```

1.  添加从节点
2.  修改主节点的可执行任务数（Number of executors）为 0
3.  视情况增大从节点的可执行任务数

## Pipeline 执行报错

### 缺少 Doker 插件

```bash
WorkflowScript: 59: Invalid agent type "docker" specified. Must be one of [any, label, none] @ line 59, column 17.
                   docker {
```

安装 Docker,Docker Pipeline 插件

Docker Pipeline 插件依赖于 Docker Commons 插件, Docker Commons 插件会自行联网并安装 docker cli ，国内网络环境大概率安装失败，参考 [Docker Cli 运行报错](#Docker Cli 运行报错) 安装或挂载

### Docker Cli 运行报错

```bash
docker: /lib/x86 64-linux-gnu/libc.so.6: version 'GLIBC 2.32' not found (required by docker) 
docker: /lib/×86 64-linux-gnu/libc.so.6: version "GLIBC_2.34' not found (required by docker)
```

出现在将宿主机的 docker-cli 挂载进容器后执行

出现此问题时的环境为

- 宿主机: ubuntu 22.04(jammy)
- Jenkins Controller: alpine 3.17.1
- Jenkins Agent: debian 11(bullseye)

```bash
# ubuntu:jammy 下 docker-cli 的动态库依赖，版本 20.10.23
	linux-vdso.so.1 (0x00007ffccbbf7000)
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fde925b9000)
	/lib64/ld-linux-x86-64.so.2 (0x00007fde9521f000)
# alpine:3.17.1 下 docker-cli 的动态库依赖，版本 20.10.21
	/lib/ld-musl-x86_64.so.1 (0x7fc530d3c000)
	libc.musl-x86_64.so.1 => /lib/ld-musl-x86_64.so.1 (0x7fc530d3c000)
# debian:bullseye 下 docker-cli 的动态库依赖，版本 23.0.1
	linux-vdso.so.1 (0x00007ffc8a9e9000)
	libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007effe3658000)
	libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007effe3652000)
	libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007effe347d000)
	/lib64/ld-linux-x86-64.so.2 (0x00007effe4f60000)
```

#### 原因

docker 使用包管理器安装，且宿主机系统跟容器系统不一致

-   docker-cli 使用包管理器进行安装时，会使用系统的动态链接库，以及时应用系统的安全更新。
    
-   使用二进制安装的形式将使用静态链接库(可以屏蔽各系统间的差异)，但无法随系统安全更新自动更新 [https://docs.docker.com/engine/install/binaries/](https://docs.docker.com/engine/install/binaries/)

#### 解决

-   手动进入各个容器，使用包管理器安装
-   提前备好二进制文件，进行挂载
-   自行构建镜像，打包好所需工具

## 查看系统自带的环境变量

```
http://<jenkins-host>/env-vars.html
```

## 修改从节点工作目录不生效

-   需重启从节点，如从节点使用 Docker 运行，还需要修改映射关系

## 查看已添加的从节点密钥

在 系统管理 > 脚本命令行 处执行

```bash
for (aSlave in hudson.model.Hudson.instance.slaves) 
{ println aSlave.name + "," + aSlave.getComputer().getJnlpMac() }
```

## 通过 API 执行 Job

-   鉴权方式：Basic Auth
-   Token 生成：用户设置-API Token
-   Method：POST
-   只能通过 `Query` 或者 `Form-data` 传参，`Json` 不生效，大小写敏感

```bash
curl --location --request POST 'http://<jenkins_host>/job/<job_name>/buildWithParameters?DABAI_ATTER=Jenkins_with_api&GAME_BRANCH=1.0&GAME_MODE=chan&GAME_PLATFORM=wx_mini_1&GAME_SERVER_TYPE=game' \
--header 'Authorization: Basic <Base64(Username:Token)>'
```

### 文档

-   [https://www.jenkins.io/doc/book/using/remote-access-api/](https://www.jenkins.io/doc/book/using/remote-access-api/)

## 通过 API 执行报错 500

检查是否是类型为选项的参数，传入参数与已配置的任一选项都不符