## Sample Container App with Custom Network and Volume

1.  Create a network for my container

```
$ docker network create net2 -d bridge --subnet 162.16.0.0/16
```

2.  Create Volume for my container

```
$ docker volume create db-data
```

3.  Create the container which uses 'net2' as network and 'db-data' as volume.

```
$ docker run --name db1 -d --net net2 -v db-data:/var/lib/mysql -e MYSQL_USER=mahendra -e MYSQL_PASSWORD=pass@12345 mahendrshinde/mysql-sample:employees
```

4.  Create another container in same network (SQL Client with Web Interface "adminer")

```
$ docker run --name c1 -d --net net2 -p 8081:8080 adminer
```

5.  Visit `http://localhost:8081/` and provide following connection details:

    ```yml
    Database: db1
    Username: mahendra
    Password: pass@12345
    ```

6.  Clean-Up

```
$ docker stop db1 c1
$ docker rm db1 c1
$ docker volume rm db-data
$ docker network net2
```


