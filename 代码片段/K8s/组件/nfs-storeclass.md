## 环境准备

- 测试裸机情况下能否成功挂载 nfs
- 安装 nfs-client , `apt install nfs-common`

[搭建 NFS](../../Linux/磁盘与挂载/搭建%20NFS.md)

## 使用 Helm 安装

[nfs-subdir-external-provisioner/README.md at master · kubernetes-sigs/nfs-subdir-external-provisioner · GitHub](https://github.com/kubernetes-sigs/nfs-subdir-external-provisioner/blob/master/charts/nfs-subdir-external-provisioner/README.md)

```bash
helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/

helm install nfs-subdir-external-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
    --set nfs.server=x.x.x.x \
    --set nfs.path=/exported/path
```

## 测试

查看 storeClass

```bash
kubectl get sc
```

应用测试 pvc

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: nfsclaim
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: nfs
  resources:
    requests:
      storage: 100Mi
```

查看 pvc 状态

```bash
kubectl get pvc
```

进入 nfs 文件夹下查看是否成功创建了目录