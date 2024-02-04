```bash
# 指定版本 K0S_VERSION=v1.28.6+k0s.0 
# Debug等级日志 DEBUG=true	
curl -sSLf https://get.k0s.sh | sudo DEBUG=true sh
sudo k0s sysinfo
sudo k0s install controller --single
sudo k0s start
sudo k0s status
watch 'k0s kubectl get pods --all-namespaces'
```

## 架构

- [Architecture - Documentation](https://docs.k0sproject.io/v1.28.6+k0s.0/architecture/)


## 配置文件

详解：[Configuration Options - Documentation](https://docs.k0sproject.io/head/configuration/)

```bash
# 验证配置
k0s validate config --config path/to/config/file
```


## 部署清单(manifests)

k0s 会持续监控此目录下的文件清单变动并自动应用，清单移除、修改，已部署的应用也会移除、修改

`/var/lib/k0s/manifests`

！需要显式指定 namespace，不会自动加到 default

类似于 `kubectl apply -f /var/lib/k0s/manifests`

- [Manifest Deployer - Documentation](https://docs.k0sproject.io/stable/manifests/)


## IngressController

支持使用官方的 `nginx-controller`

[Nginx-ingress-controller](../K8s/组件/Ingress%20Controller/Nginx-ingress-controller.md)


## 常用路径

```bash
# 配置文件
/etc/k0s
# sock, cri，默认配置文件
/run/k0s
# 数据库，kubelet，pki，镜像
/var/lib/k0s
```


## Q&A

### 获取不到 controller 节点

```bash
kubectl get no
# 仅仅列出 worker 节点
```

默认情况下，控制平面根本不运行 kubelet，并且不接受任何工作负载，因此控制器不会显示在 kubectl 的节点列表中。如果希望控制器接受工作负载并运行 Pod，请使用： `k0s controller --enable-worker` （建议仅作为 test/dev/POC 环境）。


### 无法通过 extensions 配置开启 openebs

拓展需要联网安装，网络不通会导致失败

检查：

```bash
kubectl get chart -A
# 例如：openebs 一直安装不成功
k describe chart k0s-addon-chart-openebs -n kube-system
```

下载对应的 chart，使用本地安装的方式安装

- [OpenEBS Helm Repository | OpenEBS Helm Charts](https://openebs.github.io/charts/)

```bash
# 安装好会有两个 storeClass 可供使用
root@k0s-deploy:~/k0s# k get sc
NAME                         PROVISIONER        RECLAIMPOLICY   VOLUMEBINDINGMODE      ALLOWVOLUMEEXPANSION   AGE
openebs-device               openebs.io/local   Delete          WaitForFirstConsumer   false                  11m
openebs-hostpath (default)   openebs.io/local   Delete          WaitForFirstConsumer   false                  11m
```

`openebs-hostpath` 是映射到 `/var/openebs/local` 的存储类

`openebs-device` 未配置，可以由清单部署程序根据 [OpenEBS 文档](https://openebs.io/docs/) 进行配置

### 无法找到 ClusterConfig CRD 类型 (No resources found)

使用了动态配置才会有

- [Dynamic Configuration - Documentation](https://docs.k0sproject.io/stable/dynamic-configuration/)

所有 controller 启用 `--enable-dynamic-config` 标志以使用动态配置，同时存在动态配置和静态配置(使用 `k0s.yaml` 文件)的方式会导致冲突

除了 `spec.api` 和 `spec.storage` 下的配置，其他配置都可以动态更新。
下面这些选项同样不可修改

- `network.podCIDR`
- `network.serviceCIDR`
- `network.provider`

```bash
# 修改配置
k0s config edit
# /var/lib/k0s/pki/admin.conf 等同于 kubeconfig
# 查看配置应用成功与否
k0s config status
```

### Node-local load balancing 节点本地负载均衡

简而言之：主要是用于多 controller ，且 controller 无外部负载均衡器的集群中，用于 worker 与 controller 的通信。避免只有一个入口导致这个入口宕掉了导致所有 worker 无法连上 controller

注意与 `LoadBalancer Service` 负载均衡器区别