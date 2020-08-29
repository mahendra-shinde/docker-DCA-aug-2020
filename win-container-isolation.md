## HyperV vs Process Isolation (for Windows Containers)

- Process Isolation:
    The processes inside containers are accessible outside container from the host system.

- HyperV Isolation:
    The processes inside containers are not accessible from outside container.
    Host system uses a "headless" hyperv vm to wrap all the container processes.

## Windows 10 PRO or Windows Server 2016/2019 with Docker

1. Try HyperV Isolation (Default)
    Replace ":1809" with ":1909" if your windows build is 1909!

```pwsh
$ docker pull mcr.microsoft.com/windows/nanoserver:1809
$ docker run --name c1 -it  --isolation hyperv mcr.microsoft.com/windows/nanoserver:1809 ping -t google.com
```

2.  Open One additional powershell 

```
# List all processes from container 'c1'
$ docker top c1
# Note the process-id of "ping", lets assume it's 1200
$ get-process -Id 1200
### YOU MUST GET AN ERROR!
$ docker rm -f c1
```

1. Try Process Isolation
    Replace ":1809" with ":1909" if your windows build is 1909!

```pwsh
$ docker pull mcr.microsoft.com/windows/nanoserver:1809
$ docker run --name c2 -it  --isolation process mcr.microsoft.com/windows/nanoserver:1809 ping -t google.com
```

2.  Open One additional powershell 

```
# List all processes from container 'c1'
$ docker top c2
# Note the process-id of "ping", lets assume it's 1200
$ get-process -Id 1200
### YOU SHOULD GET THE PROCESS DETAILS
$ kill-process -Id 1200
$ docker rm -f c2
```