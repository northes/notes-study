```yaml
kind: pipeline  
type: kubernetes  
name: build  
  
steps:  
  - name: docker build hash & push  
    image: plugins/docker  
    settings:  
      username:  
        from_secret: docker_username  
      password:  
        from_secret: docker_password  
      repo: northes/apihut-server  
      tags: dev-${DRONE_COMMIT_SHA:0:8}  
      dockerfile: Dockerfile 
  
trigger:  
  branch:  
    - dev  
  
---  
kind: pipeline  
type: kubernetes  
name: build && deploy  
  
steps:  
  - name: docker build tag & push  
    image: plugins/docker  
    settings:  
      username:  
        from_secret: docker_username  
      password:  
        from_secret: docker_password  
      repo: northes/apihut-server  
      tags: ${DRONE_TAG##v}  
  
  - name: "chart package"  
    image: alpine/helm:3.10.1  
    environment:  
      username:  
        from_secret: helm_username  
      password:  
        from_secret: helm_password  
    commands:  
      - helm repo add chartmuseum https://charts.northes.co --username=$username --password=$password  
      - helm plugin install https://github.com/chartmuseum/helm-push  
      - helm cm-push ./deploy/chart chartmuseum --version=${DRONE_TAG##v} --app-version=${DRONE_TAG##v}  
  
trigger:  
  event:  
    - tag
```