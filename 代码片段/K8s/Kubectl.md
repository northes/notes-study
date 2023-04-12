## 切换默认 namespace

```bash
kubectl config set-context --current --namespace=argocd
```

## 批量删除 pods

```bash
kubectl get po -n apihut| awk '{print $1}' | xargs kubectl delete po -n apihut
```

## 删除 namespace 下所有资源(namespace 保留) 

```bash
kubectl delete all --all -n <namespace>
```