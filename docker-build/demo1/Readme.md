# Basic Static WebApplication

## Notes

* Docker build process cannot access files & directories OUTSIDE current context (directory which contains Dockerfile)
* Avoid un-necessary files in current context
* All docker commands should be executed from current directory, othewise build would fail.
* Once build is successful, try a test container
* You can always push the newly built image to your container registry (need credentials)

## Demo Steps

1.  Create the HTML files / Static Webproject
2.  Create Dockerfile 
    ```
    from nginx
    ## for multiple files
    ## copy webfolder/ /usr/share/nginx/html/
    copy index.html /usr/share/nginx/html/
    ```

3.  Build an image 'myapp'
    
    > DO NOT FORGET DOT AT THE END

    `docker build -t myapp . `

4.  Test Run a container and delete it

    ```
    $ docker run --name c1 -d -p 8080:80 myapp
    $ wget http://localhost:8080
    $ docker stop c1
    $ docker rm c1
    ```