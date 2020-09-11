## Docker-Compose demo

1.  Create a new directory `C:\compose-demo2`

2.  Create or Download [docker-compose.yml](./docker-compose.yml) 

2.  Use following command to deploy the application.

    ```
    $ cd \compose-demo2
    ## Kill all other containers
    $ docker rm -f $(docker ps -aq)
    ## delete the existing network net1, net2, net3
    $ docker network rm net1 net2 net3
    ## Validate YAML file
    $ docker-compose config
    ## Deploy
    $ docker-compose up -d
    ## Check service status
    $ docker-compose ps
    ```

3.  Visit URL `http://localhost:8081`

    Connection Properties:
    
    ```yml
    System: MSSQL
    Servername: db1
    Username: SA
    Password: Password@1234
    ```

4.  Cleap-Up

    ```
    $ docker-compose down
    ```