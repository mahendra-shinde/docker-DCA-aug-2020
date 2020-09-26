## Create A Docker Image using Local Machine

Create a folder 'demo-app' and create TWO files 
- index.html

- Dockerfile
    ```
    from nginx
    copy index.html /usr/share/nginx/html/
    ```

Build a Container Image with name `myapp`

`docker build -t myapp . `

Login in your DockerHub account and then RETAG this Image
```
docker login -u [DOCKERID] -p [DOCKERPASS]
docker tag myapp [DOCKERID]/myapp
docker push [DOCKERID]/myapp
```

Create a swarm service with 3 instances
Create a deployment & service for kubernetes
