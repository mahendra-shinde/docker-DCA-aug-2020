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

1.  Create the volume
    
    ```
    $ docker volume create webdata
    $ docker volume inspect webdata
    ```

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

## Volume Binding (with Host Path)

1.  Create a local directory with `index.html` file

```
$ mkdir \temp-web
$ cd \temp-web
$ notepad index.html
### Add few lines of HTML and Save+Close notepad
```

2.  Launch container which uses "C:\temp-web" as a VOLUME BIND

```
$ docker run -d --name c2 -p 8080:80 -v c:\temp-web:/usr/share/nginx/html nginx
```

3.  Visit `http://localhost:8080`

4.  Make changes to `c:\temp-web\index.html` and then REFRESH web-browser.

5.  Clean-Up

```
$ docker stop c2
$ docker rm c2
```
