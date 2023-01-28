宿主机->Pod

```
kubectl cp /tmp/test_pod.txt default/mycentos-7b59b5b755-8rbgc:/root
```

Pod -> 宿主机

```bash
kubectl cp default/mycentos-7b59b5b755-8rbgc:/root/from_pod.txt  /tmp/from_pod.new
```