## Docker-Compose demo

1.  Create a new directory `C:\compose-demo1`

2.  Create or Download [docker-compose.yml](./docker-compose.yml) 

2.  Use following command to deploy the application.

    ```
    $ cd \compose-demo1
    ## Kill all other containers
    $ docker rm -f $(docker ps -aq)
    ## delete the existing network net1, net2
    $ docker network rm net1 net2
    ## Validate YAML file
    $ docker-compose config
    ## Deploy
    $ docker-compose up -d
    ## Check service status
    $ docker-compose ps
    ```

3.  Visit URL `http://localhost:8081`

4.  Cleap-Up

    ```
    $ docker-compose down
    ```