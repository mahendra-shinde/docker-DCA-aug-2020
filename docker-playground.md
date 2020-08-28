## Docker Playground [Lab Environment]

1. Visit https://hub.docker.com and `Sign Up` or `Sign In`

    1.1 Use `Sign Up` to create a new docker-id using Valid EMail address
    1.2 Use `Sign In` to login with existing docker-id

2.  Visit https://labs.play-with-docker.com/ and login with docker-id

3.  Running Hello world

    ```
    # Create & Start container 'c1' from Image 'hello-world'
    $ docker run --name c1 hello-world
    # List all Containers ( '-a' for Stopped containers )
    $ docker ps -a
    $ docker logs c1
    # Remove SINGLE container
    $ docker rm c1
    ## Remove ALL containers (Shell Magic!!)
    ## CANNOT USE IN CMD TERMINAL
    $ docker rm $(docker ps -aq)
    ```

4.  Running simple 'nginx' container !

    ```
    $ docker run --name c2 -d nginx
    $ docker ps
    $ docker inspect c2
    ## Get the "IPAddress" for container (Should be: 172.17.0.2)
    $ curl http://172.17.0.2/
    $ docker stop c2
    $ curl http://172.17.0.2/
    $ docker rm c2
    ```