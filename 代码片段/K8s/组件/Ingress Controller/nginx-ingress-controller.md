## 文档

- [Installation Guide - Ingress-Nginx Controller](https://kubernetes.github.io/ingress-nginx/deploy/)

## 使用 Yaml 清单安装

### 清单

`kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.8.2/deploy/static/provider/cloud/deploy.yaml`

注意修改对应的版本号

### 使用主机网络模式安装

当没有 `LoadBalance` 时，可以使用主机网络模式安装，即使用节点本地的 `80`,`443` 端口

注意修改

```yaml
spec:
  template:
    spec:
      hostNetwork: true
```

也可以完全删除名为 `ingress-nginx-controller`  的 `Service`

使用离线安装的方式需注意 [离线安装](../../离线安装.md)




## 获取客户端IP

> [!Tips]
> 自带的 traefik 未测试，目前使用的是 nginx ingress controller

由于自带 load-balance 组件的影响，传递到 ingress 的通常是集群内部地址

### 部署

使用 Helm 部署时，添加 `externalTrafficPolicy=Local` 的设置，[参考](https://kubernetes.github.io/ingress-nginx/deploy/#cloud-deployments)

```shell
helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace --set controller.service.externalTrafficPolicy=Local
```

> 如果是已经安装的情况下，需要重启所有 nginx 相关的 pod (简单粗暴直接删除即可，由 Daemon Set 、Deployment 重新拉起即可)
> ❗ 修改完后一定要重启 pod


#### 配置文件

⚡ 配置文件不需要作任何修改，记录下来仅作为当时尝试过的记录（踩过的坑）

ConfigMap  `ingress-nginx-controller`

```yaml
apiVersion: v1  
kind: ConfigMap  
metadata:  
  name: ingress-nginx-controller  
  namespace: ingress-nginx  
data:  
  compute-full-forwarded-for: 'true'  
  use-forwarded-headers: 'true'  
  enable-real-ip: 'true'
```


#### ingress.yaml

需要加上 ingressClass

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
...
spec:
  ingressClassName: nginx
  ...
```


### 验证

查看 `ingress-nginx-controller` 日志

![[Pasted image 20221204234721.png]]


### 参考

https://github.com/k3s-io/klipper-lb/issues/31

https://comphilip.wordpress.com/2021/05/23/k3s-thing-make-traefik-forward-real-client-ip/

https://kubernetes.io/docs/tutorials/services/source-ip/#source-ip-for-services-with-type-loadbalancer

https://kubernetes.github.io/ingress-nginx/deploy/#cloud-deployments

https://stackoverflow.com/questions/70356717/nginx-ingress-controllers-load-balancer-is-hiding-the-real-client-ip