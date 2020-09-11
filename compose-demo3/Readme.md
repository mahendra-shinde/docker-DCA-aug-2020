## Using docker-compose.yml for deploying service instances/replicas on swarm cluster

1.  Connect to Swarm Master and Create a `docker-compose` file with `deploy` options

    ```yml
    version: "3.8"
    services:
      app:
        image: mahendrshinde/myweb
        ports:
          - 80
    ## The following SECTION is ONLY VALID for SWARM cluster
        deploy:
          replicas: 3
          resources:
            limits:
              cpus: 0.5
              memory: 250M
            reservations:
              cpus: 0.25
              memory: 100M
          placement:
            max_replicas_per_node: 2
            constraints:
              - "node.role==worker"            
    ```

2.  Following command to deployment

    ```
    $ docker stack deploy app1 --compose-file docker-compose.yml
    $ docker stack ls
    $ docker service ls
    $ docker service inspect app1_app
    ```

3.  If you are using Docker Playgroun lab, click on new port button `30000`