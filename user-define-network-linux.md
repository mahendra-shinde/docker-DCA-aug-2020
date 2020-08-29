## User defined networks (Linux mode)

- User defined network CANNOT be created for NULL driver type.
- User defined network CANNOT be created for HOST driver type.
- User defined network CAN be created for BRIDGE driver type.
- Docker has lots of THIRD PART network driver types. 

## Create a new BRIDGE network "net1" with IP Range "18.0.0.0/16"

```
## create a network
$ docker network create net1 -d bridge --subnet 18.0.0.0/16
## Create a container inside network "net1"
$ docker run --name c1 -d --net net1 nginx
## Create a container in default "bridge" network
$ docker run --name c2 -d  nginx
## Enter inside "c2" and try accessing nginx web page
$ docker exec -it c2 bash
$ curl http://18.0.0.2/
####Expect LONG timeout or server error!
CTRL+C
$ exit
## Make "c2" also member of network "net1"
$ docker network connect net1 c2
## Verify Container "c2" is member of TWO networks
$ docker inspect c2
## Enter inside "c2" and try accessing nginx web page
$ docker exec -it c2 bash
$ curl http://18.0.0.2/
## Expected the Welcome to nginx page!!
$ exit
```

### Clean-Up

```
$ docker rm -f c1 c2
$ docker network rm net1
```