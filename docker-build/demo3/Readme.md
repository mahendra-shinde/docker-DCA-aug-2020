# ASP.NET CORE WebApplication

## Notes

* Docker build process cannot access files & directories OUTSIDE current context (directory which contains Dockerfile)
* Avoid un-necessary files in current context
* All docker commands should be executed from current directory, othewise build would fail.
* Once build is successful, try a test container
* You can always push the newly built image to your container registry (need credentials)

## Demo Steps

1.  Build the dotnet core project using Visual Studio
    And publish to folder.
2.  Create Dockerfile 
    ```
    FROM mcr.microsoft.com/dotnet/core/aspnet:2.1
    WORKDIR /app
    # Copy the entire publish folder to inside container
    COPY publish/ /app/

    CMD ["dotnet", "/app/MyApp03.dll"]
    ```

3.  Build an image 'aspapp'
    
    > DO NOT FORGET DOT AT THE END

    `docker build -t aspapp . `

4.  Test Run a container and delete it

    ```
    $ docker run --name c1 -d -p 8080:80 aspapp
    $ wget http://localhost:8080
    $ docker stop c1
    $ docker rm c1
    ```