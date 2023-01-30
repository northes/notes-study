
[GitHub - google/gvisor: Application Kernel for Containers](https://github.com/google/gvisor)

将容器与宿主机隔离，目前已集成在 Docker 和 K8s

通过指定 `runtime` 和 添加 `--force` 参数，指定容器使用 `gVisor` 运行

```bash
docker run --runtime=runsc -v $(pwd):/workspace -v ~/.config:/root/.config \
gcr.io/kaniko-project/executor:latest \
--dockerfile=<path to Dockerfile> --context=/workspace \
--destination=gcr.io/my-repo/my-image --force
```