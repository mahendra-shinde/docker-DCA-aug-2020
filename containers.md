## Running a Container

- Containers can be launched in THREE modes
- Non-Interactive mode, container run and display ALL logs directly in same terminal window. But does't allow to enter any input.

    $ docker run [IMAGE-NAME]

- Interactive mode, container run and display the log and allows INPUT in same terminal. When user CLOSES the terminal or stop the command ( either use 'exit' or CTRL+C) will result in container getting stopped.

    $ docker run -it [IMAGE-NAME] [COMMAND-AND-ARGs]

    ex:

    ```
    $ docker run -it busybox ping google.com
    CTRL+C
    $ docker ps -a
    # Container is STOPPED
    ```

-  Detached Mode, container run in 'background', doesn't show any LOG, and display `container-id`.

    $ docker run -d [IMAGE-NAME] 

- Containers SHOULD run in DETACHED mode, and use following commands:
    docker logs     : View the logs
    docker stop     : Stop the container
    docker top      : To view processes inside containers

