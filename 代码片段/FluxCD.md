## Flux系统配置

```shell  
flux bootstrap git \  
--url=https://git.northes.co/apihut/docs.git \  
--username=northes \  
--password=29183927Abcd \  
--token-auth=true \  
--branch=dev \  
--namespace=flux-system \  
--path=./clusters/default  
```  
  
## Git源,HelmChart文件部署

```shell  
flux create source git flux-test \  
--url=https://git.northes.co/pioneer/flux-test \  
--branch=main \  
--interval=1m \  
--username=northes \  
--password=29183927Abcd \  
--namespace=default \  
--export > ./clusters/my-cluster/source.yaml  
  
  
flux create hr flux-test \  
--interval=10s \  
--source=GitRepository/flux-test \  
--chart=./deploy/flux-test \  
--namespace=default \  
--export > ./clusters/my-cluster/helm.yaml  
```  
  
## Chart仓库源,HelmChart部署

```shell  
flux create source helm apihut \  
--url=https://charts.northes.co \  
--interval=1m \  
--username=northes \  
--password=29183927abcd \  
--namespace=default  
  
flux create hr apihut-docs \  
--interval=1m \  
--source=HelmRepository/apihut \  
--chart=apihut-docs \  
--target-namespace=default \  
--namespace=default  
#--chart-version=">4.0.0"  
```

## 命令

```shell
flux get source chart -w

```