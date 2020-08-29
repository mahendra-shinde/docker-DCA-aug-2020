# Container Volumes

* Volumes are `Persisted file storage` for containers.
* Volumes are RETAINED after containers are REMOVED.
* Volumes CAN BE shared by multiple containers.
* Volumes CAN BE ATTACHED only at CREATION time.
* Syntax Volume Mapping:
    `docker run [OTHER-OPTIONS] -v [VOLNAME]:[GUESTFS_PATH]:[ACCESS_MODE] [IMAGE]`
* Default Access mode is `RW` (ReadWrite), alternate option is `RO` (ReadOnly)

## Docker Volume commands:

```
# List all Volumes
$ docker volume ls
# View details of volume 'v1'
$ docker volume inspect v1
# Delete volume 'v1'
# docker volume rm v1
```

## Volume demo

1.  Create a new NGINX container with Port forwarding and volume mapping

    ```
    $ docker run --name c1 -d -v webdata:/usr/share/nginx/html  -p 8080:80  nginx
    $ docker exec -it c1 sh
    $ cd /usr/share/nginx/html
    # Remove original index.html
    $ rm index.html
    $ echo "<h2>Hello Mahendra</h2>" > index.html
    $ exit
    ```

2.  Try Accessing URL `http://localhost:8080` from web browser.

3.  Try to Stop->Delete->Create the container

    ```
    $ docker stop c1
    $ docker rm c1
    $ docker run --name c1 -d -v webdata:/usr/share/nginx/html  -p 8080:80  nginx
    ```

4.  Try Accessing URL `http://localhost:8080` from web browser.

5.  Clean-up

    ```
    $ docker rm -f c1
    $ docker volume rm webdata
    ```

