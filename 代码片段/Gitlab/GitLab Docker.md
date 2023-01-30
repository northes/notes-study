```bash
docker run --detach \
  --hostname gitlab.example.com \
  --publish 1443:443 --publish 180:80 --publish 122:22 \
  --name gitlab \
  --restart always \
  --volume /root/gitlab_data/config:/etc/gitlab \
  --volume /root/gitlab_data/logs:/var/log/gitlab \
  --volume /root/gitlab_data/data:/var/opt/gitlab \
  --shm-size 256m \
  gitlab/gitlab-ce:latest
```