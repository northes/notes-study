离线部署

## 准备

[Releases · k0sproject/k0s](https://github.com/k0sproject/k0s/releases)

1. airgap-bundle tar包
2. k0s 二进制文件

[GitHub - k0sproject/k0sctl: A bootstrapping and management tool for k0s clusters.](https://github.com/k0sproject/k0sctl)

1. k0sctl 工具

### 端口

查看所有需要的端口：[Networking (CNI) - Documentation](https://docs.k0sproject.io/v1.28.6+k0s.0/networking/) （注意替换URL中的版本）


## SSH

确保运行 k0sctl 工具的机器能够通过密钥的方式连上所有需要部署机器

## 配置文件

配置详解：[GitHub - k0sproject/k0sctl: A bootstrapping and management tool for k0s clusters.](https://github.com/k0sproject/k0sctl)

```bash
# 生成配置文件
k0sctl init > k0sctl.yaml
```

```yaml
apiVersion: k0sctl.k0sproject.io/v1beta1
kind: Cluster
metadata:
  name: k0s-cluster
spec:
  hosts:
  - ssh:
      address: 192.168.31.40 # 集群机器地址
      user: root
      port: 22
      keyPath: ~/.ssh/id_rsa
    role: controller # 可配 controller、worker、controller+worker、single
    uploadBinary: true # 上传k0s二进制文件，而不是下载
    k0sBinaryPath: ./k0s # 指定上传的二进制文件路径
  - ssh:
      address: 192.168.31.42
      user: root
      port: 22
      keyPath: ~/.ssh/id_rsa
    role: worker
    uploadBinary: true
    k0sBinaryPath: ./k0s
    files: # 在开启部署前需上传的文件
      - src: ./k0s-airgap-bundle-v1.28.6+k0s.0-amd64 # 下载的对应版本的 bundle 包
        dstDir: /var/lib/k0s/images/ # 上传到目标机器的位置，k0s启动时将会从这个固定路径读取所有的镜像并载入 containerd，方便离线部署
        perm: 0755
  - ssh:
      address: 192.168.31.43
      user: root
      port: 22
      keyPath: ~/.ssh/id_rsa
    role: worker
    uploadBinary: true
    k0sBinaryPath: ./k0s
    files:
      - src: ./k0s-airgap-bundle-v1.28.6+k0s.0-amd64
        dstDir: /var/lib/k0s/images/
        perm: 0755
  k0s:
    version: 1.28.6+k0s.0 # 指定版本，需要与上传的二进制文件相同
    versionChannel: stable
    dynamicConfig: false
    config: # 未提供的配置将使用默认值，这里的配置指的是 k0s.yaml
      apiVersion: k0s.k0sproject.io/v1beta1
      kind: ClusterConfig
      metadata:
        name: my-k0s-cluster
      spec:
        images:
          default_pull_policy: Never # 指定镜像从不拉取，适用于离线部署
```

## 部署

```bash
# 打印debug日志
k0sctl apply -c k0sctl.yaml -d
# 如果 k0sctl.yaml 文件就在运行命令的目录，可省略
k0sctl apply -d
```

## 生成 kubeconfig 文件

```bash
# 如果 k0sctl.yaml 文件就在运行命令的目录，可省略指定。否则需要 -c \ --config 显式指定 k0sctl.yaml 文件路径
k0sctl kubeconfig > kubeconfig
```

```bash
# 使用指定的 kubeconfig 文件连接集群
kubectl get po --kubeconfig kubeconfig -A
```

## 卸载

```bash
# 可省略，同上
k0sctl reset --config k0sctl.yaml
```