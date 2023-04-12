## 切换默认 namespace

```bash
kubectl config set-context --current --namespace=argocd
```

## 批量删除 pods

```bash
kubectl get po -n apihut| awk '{print $1}' | xargs kubectl delete po -n apihut
```