# Docker Swarm

## Swarm Demo 1

1.  Visit the docker-playground `https://labs.play-with-docker.com`
2.  Login with your Docker Hub ID
3.  Click `Start` button to launch the lab environment.
4.  Click `Add new Instance` button TWICE.
5.  Click on `node1` and following commands :

    ```
    $ docker info -f "{{json .Swarm}}"
    $ docker swarm init --advertise-addr [IP-ADDRESS-OF-NODE1]
    ### You should get the command to be run on WORKER NODE
    Swarm initialized: current node (7gtfn8aebtvsogyda7v54hvvb) is now a manager.

    To add a worker to this swarm, run the following command:

        docker swarm join --token SWMTKN-1-04hnzwjs6womzvogz8f04a70kxgcuz5x9by5pmkswe61twityh-e7omsuujntqaodyhaeks89j1k 192.168.0.33:2377

    To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
    ```

6.  Click on `node2` and use following commands:

    ```
    $ docker info -f "{{json .Swarm}}"
    ## USE COMMAND COPIED FROM node1
    docker swarm join --token SWMTKN-1-04hnzwjs6womzvogz8f04a70kxgcuz5x9by5pmkswe61twityh-e7omsuujntqaodyhaeks89j1k 192.168.0.33:2377
    $ docker info 
    ```