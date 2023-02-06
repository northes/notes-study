`/usr/lib/systemd/system/docker.service`

再后面添加监听地址与端口

```ExecStart=/usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock -H tcp://0.0.0.0:2375
```

重启

```bash
systemctl daemon-reload
systemctl restart docker
```

测试

```bash
curl -XGET http://localhost:2375/version
```

使用远程守护进程

```bash
docker -H tcp://192.168.31.26:2375 info
```

```
export DOCKER_HOST="tcp://192.168.31.26:2375"
```