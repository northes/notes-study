## 切换默认 namespace

```bash
kubectl config set-context --current --namespace=argocd
```

## 批量删除 pods

```bash
k get po -n apihut| grep apihut |awk '{print $1}' | xargs kubectl delete po -n apihut
```

## 删除 namespace 下所有资源(namespace 保留) 

```bash
kubectl delete all --all -n <namespace>
```

## node 详情

```bash
kubectl get no -o wide
```

## 封锁并清空节点

```bash
kubectl cordon <node-name>
kubectl drain <node-name> --ignore-daemonset
```