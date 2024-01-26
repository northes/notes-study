```bash
curl -sSLf https://get.k0s.sh | sudo sh
sudo k0s sysinfo
sudo k0s install controller --single
sudo k0s start
sudo k0s status
watch 'k0s kubectl get pods --all-namespaces'
```