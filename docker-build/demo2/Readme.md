# Java WebApplication using Tomcat

## Notes

* Docker build process cannot access files & directories OUTSIDE current context (directory which contains Dockerfile)
* Avoid un-necessary files in current context
* All docker commands should be executed from current directory, othewise build would fail.
* Once build is successful, try a test container
* You can always push the newly built image to your container registry (need credentials)

## Demo Steps

1.  Build the WAR file for Java project
2.  Create Dockerfile 
    ```
    from tomcat:8-jdk8-openjdk
    copy DemoApp-0.2.war /usr/local/tomcat/webapps/ROOT.war
    ```

3.  Build an image 'japp'
    
    > DO NOT FORGET DOT AT THE END

    `docker build -t japp . `

4.  Test Run a container and delete it

    ```
    $ docker run --name c1 -d -p 8080:8080 japp
    $ wget http://localhost:8080
    $ docker stop c1
    $ docker rm c1
    ```