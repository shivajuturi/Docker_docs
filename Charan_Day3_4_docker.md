

```
root@shivadocker:~# docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
nginx        latest    5ef79149e0ec   2 weeks ago     188MB
busybox      latest    65ad0d468eb1   15 months ago   4.26MB
root@shivadocker:~# docker run -d --name web01 nginx
8a81c83712ca3698c8c8b1d6935ce610d4440bd935c277f964899b37be5a2bc5
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS                        PORTS                                   NAMES
8a81c83712ca   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes                  80/tcp                                  web01

root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS     NAMES
8a81c83712ca   nginx     "/docker-entrypoint.…"   3 minutes ago   Up 3 minutes   80/tcp    web01
root@shivadocker:~#

```

- (-dit) means -d means detach mode -it means while create container with os images entry point will run inside container  
- if i pass -it container will up (for os images , like ubuntu , busybox)

```

root@shivadocker:~# docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
nginx        latest    5ef79149e0ec   2 weeks ago     188MB
busybox      latest    65ad0d468eb1   15 months ago   4.26MB
root@shivadocker:~# docker run -d --name bb01 busybox
52acc06216004702d94863584a4fa45be38ede1f4f26c2d3474a204c00943a1e
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS                     PORTS     NAMES
52acc0621600   busybox   "sh"      10 seconds ago   Exited (0) 9 seconds ago             bb01
root@shivadocker:~# docker run -dit  --name bb02 busybox
e8d4ee26774bd8f4523d7635502449d67e9e0abcf7f0144aeaab7cc6b98b6d3c
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND   CREATED          STATUS                      PORTS     NAMES
e8d4ee26774b   busybox   "sh"      3 seconds ago    Up 2 seconds                          bb02
52acc0621600   busybox   "sh"      31 seconds ago   Exited (0) 30 seconds ago             bb01
root@shivadocker:~#



```

- top output 1 is root session it created with -it option, 8 session is created due to docker exec -it   

```
root@shivadocker:~# docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
nginx        latest    5ef79149e0ec   2 weeks ago     188MB
ubuntu       latest    edbfe74c41f8   4 weeks ago     78.1MB
busybox      latest    65ad0d468eb1   15 months ago   4.26MB
root@shivadocker:~# docker run -dit --name myubuntu ubuntu
ac5303fe56b22b50aef722b73af77ccb1cee3fb09b053ca4a1324415734ade47
root@shivadocker:~# docker run -d  --name myubuntu1  ubuntu
c177cf70e2a075394382f626ee6a8612d032cf9c6b4f7a6af839451cf7cd31dd
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND       CREATED          STATUS                     PORTS     NAMES
c177cf70e2a0   ubuntu    "/bin/bash"   7 seconds ago    Exited (0) 6 seconds ago             myubuntu1
ac5303fe56b2   ubuntu    "/bin/bash"   18 seconds ago   Up 17 seconds                        myubuntu
root@shivadocker:~# docker exec -it myubuntu /bin/bash
root@ac5303fe56b2:/# top
top - 04:45:56 up 39 min,  0 user,  load average: 1.02, 0.47, 0.28
Tasks:   3 total,   1 running,   2 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   3875.9 total,   2779.5 free,    727.7 used,    608.2 buff/cache
MiB Swap:   2795.0 total,   2795.0 free,      0.0 used.   3148.1 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0    4588   3920   3412 S   0.0   0.1   0:00.02 bash
      8 root      20   0    4588   3808   3304 S   0.0   0.1   0:00.01 bash
     16 root      20   0    8848   5184   3056 R   0.0   0.1   0:00.00 top


```
- docker attach  will connect to entrypoint session if i gave exit in that container container will stop ,

- docker attach will not use
```
root@shivadocker:~# docker attach   myubuntu
root@ac5303fe56b2:/# top
top - 04:49:50 up 43 min,  0 user,  load average: 0.17, 0.29, 0.25
Tasks:   2 total,   1 running,   1 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.2 us,  0.2 sy,  0.0 ni, 99.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   3875.9 total,   2787.7 free,    719.2 used,    608.6 buff/cache
MiB Swap:   2795.0 total,   2795.0 free,      0.0 used.   3156.7 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0    4588   3920   3412 S   0.0   0.1   0:00.02 bash
     18 root      20   0    8848   5156   3016 R   0.0   0.1   0:00.00 top


     root@ac5303fe56b2:/#
     root@ac5303fe56b2:/#
     root@ac5303fe56b2:/# exit
     exit
     root@shivadocker:~# docker ps -a
     CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS                     PORTS     NAMES
     c177cf70e2a0   ubuntu    "/bin/bash"   6 minutes ago   Exited (0) 6 minutes ago             myubuntu1
     ac5303fe56b2   ubuntu    "/bin/bash"   6 minutes ago   Exited (0) 2 seconds ago             myubuntu
     root@shivadocker:~#



```
- docker events ( events will capture from session 2  )

```
session 1:

root@shivadocker:~# docker events
2024-08-31T04:54:47.638517103Z container create 2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4 (image=nginx, maintainer=NGINX Docker Maintainers <docker-maint@nginx.com>, name=mynginx)
2024-08-31T04:54:47.684960176Z network connect b3abc16a280a680e27206b1844cf174a24a27509ce5c4cb2284fe7c7fb9991bd (container=2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4, name=bridge, type=bridge)
2024-08-31T04:54:48.201417773Z container start 2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4 (image=nginx, maintainer=NGINX Docker Maintainers <docker-maint@nginx.com>, name=mynginx)
2024-08-31T04:55:28.412791680Z container exec_create: /bin/bash  2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4 (execID=44eda4f4097ecc825aa382f56229171bf161d449294b2e3ff2560c8e29bafde4, image=nginx, maintainer=NGINX Docker Maintainers <docker-maint@nginx.com>, name=mynginx)
2024-08-31T04:55:28.413902767Z container exec_start: /bin/bash  2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4 (execID=44eda4f4097ecc825aa382f56229171bf161d449294b2e3ff2560c8e29bafde4, image=nginx, maintainer=NGINX Docker Maintainers <docker-maint@nginx.com>, name=mynginx)
2024-08-31T04:55:38.158641292Z container exec_die 2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4 (execID=44eda4f4097ecc825aa382f56229171bf161d449294b2e3ff2560c8e29bafde4, exitCode=127, image=nginx, maintainer=NGINX Docker Maintainers <docker-maint@nginx.com>, name=mynginx)
2024-08-31T04:55:48.209683298Z container kill 2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4 (image=nginx, maintainer=NGINX Docker Maintainers <docker-maint@nginx.com>, name=mynginx, signal=3)
2024-08-31T04:55:48.362360011Z network disconnect b3abc16a280a680e27206b1844cf174a24a27509ce5c4cb2284fe7c7fb9991bd (container=2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4, name=bridge, type=bridge)
2024-08-31T04:55:48.372755402Z container stop 2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4 (image=nginx, maintainer=NGINX Docker Maintainers <docker-maint@nginx.com>, name=mynginx)
2024-08-31T04:55:48.375962521Z container die 2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4 (execDuration=60, exitCode=0, image=nginx, maintainer=NGINX Docker Maintainers <docker-maint@nginx.com>, name=mynginx)

session 2:

we need to execute commands

root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND       CREATED         STATUS              PORTS     NAMES
ac5303fe56b2   ubuntu    "/bin/bash"   8 minutes ago   Up About a minute             myubuntu
root@shivadocker:~# docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
nginx        latest    5ef79149e0ec   2 weeks ago     188MB
ubuntu       latest    edbfe74c41f8   4 weeks ago     78.1MB
busybox      latest    65ad0d468eb1   15 months ago   4.26MB
root@shivadocker:~# docker run -d --name mynginx nginx
2a199b15b8d610b43d1dc37e9af4b23a974fd89adfbad4e5b3ebbb1d2b0716a4
root@shivadocker:~# docker exec -it nginx /bin/bash
Error response from daemon: No such container: nginx
root@shivadocker:~# docker exec -it mynginx /bin/bash
root@2a199b15b8d6:/# top
bash: top: command not found
root@2a199b15b8d6:/# exit
exit
root@shivadocker:~# docker stop  mynginx
mynginx
root@shivadocker:~#



```

- create docker images via running container

```

root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS     NAMES
2a199b15b8d6   nginx     "/docker-entrypoint.…"   7 minutes ago    Exited (0) 6 minutes ago              mynginx
c177cf70e2a0   ubuntu    "/bin/bash"              16 minutes ago   Exited (0) 16 minutes ago             myubuntu1
ac5303fe56b2   ubuntu    "/bin/bash"              17 minutes ago   Up 9 minutes                          myubuntu
root@shivadocker:~#
root@shivadocker:~#
root@shivadocker:~# docker commit myubuntu
sha256:c99d864fa2cb091cb73cab0022cb695f40a69c770dfa5bd017aa221374e787c5
root@shivadocker:~# docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
<none>       <none>    c99d864fa2cb   9 seconds ago   78.1MB
nginx        latest    5ef79149e0ec   2 weeks ago     188MB
ubuntu       latest    edbfe74c41f8   4 weeks ago     78.1MB
busybox      latest    65ad0d468eb1   15 months ago   4.26MB
root@shivadocker:~# docker commit myubuntu  custome_image
sha256:a9d4d4a8af461c0f6fceea6995bed60315c7c533a8cc9c749eccb9a65314c2da
root@shivadocker:~# docker images
REPOSITORY      TAG       IMAGE ID       CREATED              SIZE
custome_image   latest    a9d4d4a8af46   2 seconds ago        78.1MB
<none>          <none>    c99d864fa2cb   About a minute ago   78.1MB
nginx           latest    5ef79149e0ec   2 weeks ago          188MB
ubuntu          latest    edbfe74c41f8   4 weeks ago          78.1MB
busybox         latest    65ad0d468eb1   15 months ago        4.26MB
root@shivadocker:~#


```

- how it was created that images we can see

```
root@shivadocker:~# docker images
REPOSITORY      TAG       IMAGE ID       CREATED              SIZE
custome_image   latest    a9d4d4a8af46   2 seconds ago        78.1MB
<none>          <none>    c99d864fa2cb   About a minute ago   78.1MB
nginx           latest    5ef79149e0ec   2 weeks ago          188MB
ubuntu          latest    edbfe74c41f8   4 weeks ago          78.1MB
busybox         latest    65ad0d468eb1   15 months ago        4.26MB
root@shivadocker:~# docker history a9d4d4a8af46
IMAGE          CREATED         CREATED BY                                      SIZE      COMMENT
a9d4d4a8af46   2 minutes ago   /bin/bash                                       23B
edbfe74c41f8   4 weeks ago     /bin/sh -c #(nop)  CMD ["/bin/bash"]            0B
<missing>      4 weeks ago     /bin/sh -c #(nop) ADD file:c2e78eb585ec4e503…   78.1MB
<missing>      4 weeks ago     /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B
<missing>      4 weeks ago     /bin/sh -c #(nop)  LABEL org.opencontainers.…   0B
<missing>      4 weeks ago     /bin/sh -c #(nop)  ARG LAUNCHPAD_BUILD_ARCH     0B
<missing>      4 weeks ago     /bin/sh -c #(nop)  ARG RELEASE                  0B
root@shivadocker:~#


```


```
root@shivadocker:~# docker search mongo
NAME                                       DESCRIPTION                                     STARS     OFFICIAL   AUTOMATED
mongo                                      MongoDB document databases provide high avai…   10364     [OK]
circleci/mongo                             CircleCI images for MongoDB                     13                   [OK]
corpusops/mongo                            https://github.com/corpusops/docker-images/     0
litmuschaos/mongo                                                                          1
uselagoon/mongo                                                                            0
noenv/mongo                                MongoDB Docker Image                            0
drud/mongo                                                                                 0
elestio/bigcapital-mongo                   Bigcapital-mongo, verified and packaged by E…   0
lintoai/linto-platform-mongodb-migration   Handles mingrations for LinTO Platform Mongo…   0
camicroscope/imageloader                   Image Loader for loading image metadata into…   0                    [OK]
camicroscope/uaimdataloader                uAIMDataloader for loading image segmentatio…   0                    [OK]
itzg/mongo-backups                         A very simplistic container to perform perio…   0                    [OK]
rimamartur/mongo                           mongo                                           0
cyrilcyril70/mongo                         mongo                                           0
robsonsimonassi/mongo                      mongo                                           0                    [OK]
korawichtawan/mongo                        mongo                                           0
radityaarief/mongo                         mongo                                           0
mohankumarreddysiddavatm/mongo             mongo                                           0
mateuszdyminski/mongo                      Mongo                                           0
mwhutchinson/mongo                         mongo                                           0
caijiajia/mongo                            mongo                                           0
1127129489/mongo                           mongo                                           0
khaddour503/mongo                          mongo                                           0
ckeyer/mongo                               Mongo                                           0
mike007i/mongo                             mongo                                           0
root@shivadocker:~#

```


```
root@shivadocker:~# docker image prune
WARNING! This will remove all dangling images.
Are you sure you want to continue? [y/N] yes
Total reclaimed space: 0B
root@shivadocker:~#

```
 - to find container running ports
```
root@shivadocker:~# docker images
REPOSITORY      TAG       IMAGE ID       CREATED          SIZE
custome_image   latest    a9d4d4a8af46   18 minutes ago   78.1MB
<none>          <none>    c99d864fa2cb   19 minutes ago   78.1MB
nginx           latest    5ef79149e0ec   2 weeks ago      188MB
ubuntu          latest    edbfe74c41f8   4 weeks ago      78.1MB
busybox         latest    65ad0d468eb1   15 months ago    4.26MB
root@shivadocker:~# docker run -dit --name samba -p 8001:80 nginx
35b25f9840ad58ad6b8471a2bd05c70226aa0357fb9c5916bec052d5cff8c7c4
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   4 seconds ago    Up 3 seconds    0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba
ac5303fe56b2   ubuntu    "/bin/bash"              37 minutes ago   Up 29 minutes                                           myubuntu
root@shivadocker:~# docker ports samba
docker: 'ports' is not a docker command.
See 'docker --help'
root@shivadocker:~# docker port samba
80/tcp -> 0.0.0.0:8001
80/tcp -> [::]:8001
root@shivadocker:~#

```
- file copy to container and container to outside

```
root@shivadocker:~# touch sample.txt
root@shivadocker:~# l s-lrt
ls: cannot access 's-lrt': No such file or directory
root@shivadocker:~# ls -lrt
total 4
drwx------ 3 root root 4096 Aug 26 09:00 snap
-rw-r--r-- 1 root root    0 Aug 31 05:25 sample.txt
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   3 minutes ago    Up 3 minutes    0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba
ac5303fe56b2   ubuntu    "/bin/bash"              40 minutes ago   Up 33 minutes                                           myubuntu
root@shivadocker:~# docker cp sample.txt samba:/home
Successfully copied 1.54kB to samba:/home
root@shivadocker:~# docker exec -it samba /bin/bash
root@35b25f9840ad:/# ls -lrt /home
total 0
-rw-r--r-- 1 root root 0 Aug 31 05:25 sample.txt
root@35b25f9840ad:/#

root@shivadocker:~# docker exec -it samba ls -la /home
total 8
drwxr-xr-x 1 root root 4096 Aug 31 05:26 .
drwxr-xr-x 1 root root 4096 Aug 31 05:26 ..
-rw-r--r-- 1 root root    0 Aug 31 05:25 sample.txt
root@shivadocker:~# docker exec -it samba touch  /home/a.txt
root@shivadocker:~# docker exec -it samba ls -la /home
total 8
drwxr-xr-x 1 root root 4096 Aug 31 05:29 .
drwxr-xr-x 1 root root 4096 Aug 31 05:26 ..
-rw-r--r-- 1 root root    0 Aug 31 05:29 a.txt
-rw-r--r-- 1 root root    0 Aug 31 05:25 sample.txt
root@shivadocker:~# docker cp samba:/home/a.txt .
Successfully copied 1.54kB to /root/.
root@shivadocker:~# ls -lrt
total 4
drwx------ 3 root root 4096 Aug 26 09:00 snap
-rw-r--r-- 1 root root    0 Aug 31 05:25 sample.txt
-rw-r--r-- 1 root root    0 Aug 31 05:29 a.txt
root@shivadocker:~#


```


- after creation container further what modification has done we can see

- it tell container data and image data difference  it shows   

```
root@shivadocker:~# docker diff samba
C /var
C /var/cache
C /var/cache/nginx
A /var/cache/nginx/fastcgi_temp
A /var/cache/nginx/proxy_temp
A /var/cache/nginx/scgi_temp
A /var/cache/nginx/uwsgi_temp
A /var/cache/nginx/client_temp
C /etc
C /etc/nginx
C /etc/nginx/conf.d
C /etc/nginx/conf.d/default.conf
C /run
A /run/nginx.pid
C /home
A /home/a.txt
A /home/sample.txt
C /root
A /root/.bash_history
root@shivadocker:~#

```


- for debug container

```

root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   16 minutes ago   Up 16 minutes               0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba
2a199b15b8d6   nginx     "/docker-entrypoint.…"   43 minutes ago   Exited (0) 42 minutes ago                                           mynginx
c177cf70e2a0   ubuntu    "/bin/bash"              53 minutes ago   Exited (0) 53 minutes ago                                           myubuntu1
ac5303fe56b2   ubuntu    "/bin/bash"              53 minutes ago   Up 46 minutes                                                       myubuntu
root@shivadocker:~# docker logs mynginx
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/08/31 04:54:48 [notice] 1#1: using the "epoll" event method
2024/08/31 04:54:48 [notice] 1#1: nginx/1.27.1
2024/08/31 04:54:48 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/08/31 04:54:48 [notice] 1#1: OS: Linux 5.15.0-119-generic
2024/08/31 04:54:48 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2024/08/31 04:54:48 [notice] 1#1: start worker processes
2024/08/31 04:54:48 [notice] 1#1: start worker process 28
2024/08/31 04:54:48 [notice] 1#1: start worker process 29
2024/08/31 04:55:48 [notice] 1#1: signal 3 (SIGQUIT) received, shutting down
2024/08/31 04:55:48 [notice] 28#28: gracefully shutting down
2024/08/31 04:55:48 [notice] 28#28: exiting
2024/08/31 04:55:48 [notice] 29#29: gracefully shutting down
2024/08/31 04:55:48 [notice] 29#29: exiting
2024/08/31 04:55:48 [notice] 28#28: exit
2024/08/31 04:55:48 [notice] 29#29: exit
2024/08/31 04:55:48 [notice] 1#1: signal 17 (SIGCHLD) received from 28
2024/08/31 04:55:48 [notice] 1#1: worker process 28 exited with code 0
2024/08/31 04:55:48 [notice] 1#1: signal 29 (SIGIO) received
2024/08/31 04:55:48 [notice] 1#1: signal 17 (SIGCHLD) received from 29
2024/08/31 04:55:48 [notice] 1#1: worker process 29 exited with code 0

```

- docker pause unpause restart

```
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   17 minutes ago   Up 17 minutes   0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba
ac5303fe56b2   ubuntu    "/bin/bash"              54 minutes ago   Up 47 minutes                                           myubuntu
root@shivadocker:~# docker pause samba
samba
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                   PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   17 minutes ago   Up 17 minutes (Paused)   0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba
ac5303fe56b2   ubuntu    "/bin/bash"              55 minutes ago   Up 47 minutes                                                    myubuntu
root@shivadocker:~#
root@shivadocker:~#
root@shivadocker:~# docker commit samba samba_own:latest
sha256:d2fb207acc49b8718afa78ffd66de43025141498508bc1919fb0e1fb5d94f33a
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                   PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   18 minutes ago   Up 18 minutes (Paused)   0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba
ac5303fe56b2   ubuntu    "/bin/bash"              55 minutes ago   Up 48 minutes                                                    myubuntu
root@shivadocker:~# docker unpause samba
samba
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   18 minutes ago   Up 18 minutes   0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba
ac5303fe56b2   ubuntu    "/bin/bash"              55 minutes ago   Up 48 minutes                                           myubuntu
root@shivadocker:~# docker restart samba
samba
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   19 minutes ago   Up 4 seconds    0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba
ac5303fe56b2   ubuntu    "/bin/bash"              56 minutes ago   Up 48 minutes                                           myubuntu
root@shivadocker:~#

```


```
root@shivadocker:~# docker rename samba samba2
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS              PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   20 minutes ago   Up About a minute   0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba2
ac5303fe56b2   ubuntu    "/bin/bash"              57 minutes ago   Up 50 minutes                                               myubuntu
root@shivadocker:~#

```


- docker top

```

root@shivadocker:~# docker top samba2
UID                 PID                 PPID                C                   STIME               TTY                 TIME                CMD
root                4759                4738                0                   05:41               pts/0               00:00:00            nginx: master process nginx -g daemon off;
systemd+            4799                4759                0                   05:41               pts/0               00:00:00            nginx: worker process
systemd+            4800                4759                0                   05:41               pts/0               00:00:00            nginx: worker process
root@shivadocker:~#


root@shivadocker:~# docker exec -it myubuntu /bin/bash
root@ac5303fe56b2:/# tops
bash: tops: command not found
root@ac5303fe56b2:/# top
top - 05:44:45 up  1:38,  0 user,  load average: 0.27, 0.18, 0.18
Tasks:   3 total,   1 running,   2 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   3875.9 total,   2740.8 free,    748.9 used,    635.0 buff/cache
MiB Swap:   2795.0 total,   2795.0 free,      0.0 used.   3127.0 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0    4588   3916   3408 S   0.0   0.1   0:00.01 bash
      8 root      20   0    4588   3916   3324 S   0.0   0.1   0:00.06 bash
     17 root      20   0    8848   5224   3096 R   0.0   0.1   0:00.01 top




```

- to see how much RAM / CUP  is used container


```
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS          PORTS                                   NAMES
35b25f9840ad   nginx     "/docker-entrypoint.…"   24 minutes ago      Up 5 minutes    0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba2
ac5303fe56b2   ubuntu    "/bin/bash"              About an hour ago   Up 54 minutes                                           myubuntu
root@shivadocker:~# docker stats
CONTAINER ID   NAME       CPU %     MEM USAGE / LIMIT     MEM %     NET I/O       BLOCK I/O     PIDS
35b25f9840ad   samba2     0.00%     3.344MiB / 3.785GiB   0.09%     936B / 0B     0B / 8.19kB   3
ac5303fe56b2   myubuntu   0.00%     1.348MiB / 3.785GiB   0.03%     1.37kB / 0B   0B / 0B       1

```
# IMP   set the limit to cpu and memmory  to container (1024 cpu means 1 cpu )

```
root@shivadocker:~# docker run -dit --name samba_mem --cpu-shares  256 --memory 512m --memory-swap 1g nginx
a804d4a7fc8d1b3087dcd6b1566d94c809aaf4766a23f2af4ce98e557b164ccc
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                                   NAMES
a804d4a7fc8d   nginx     "/docker-entrypoint.…"   8 seconds ago       Up 7 seconds       80/tcp                                  samba_mem
35b25f9840ad   nginx     "/docker-entrypoint.…"   40 minutes ago      Up 21 minutes      0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba2
ac5303fe56b2   ubuntu    "/bin/bash"              About an hour ago   Up About an hour                                           myubuntu
root@shivadocker:~# docker stats
CONTAINER ID   NAME        CPU %     MEM USAGE / LIMIT     MEM %     NET I/O       BLOCK I/O     PIDS
a804d4a7fc8d   samba_mem   0.00%     3.508MiB / 512MiB     0.69%     656B / 0B     0B / 24.6kB   3
35b25f9840ad   samba2      0.00%     3.344MiB / 3.785GiB   0.09%     1.08kB / 0B   0B / 8.19kB   3
ac5303fe56b2   myubuntu    0.00%     1.348MiB / 3.785GiB   0.03%     1.44kB / 0B   0B / 0B       1

```
- to update running container
```
CONTAINER ID   NAME        CPU %     MEM USAGE / LIMIT     MEM %     NET I/O       BLOCK I/O     PIDS
a804d4a7fc8d   samba_mem   0.00%     3.508MiB / 512MiB     0.69%     656B / 0B     0B / 24.6kB   3
35b25f9840ad   samba2      0.00%     3.344MiB / 3.785GiB   0.09%     1.08kB / 0B   0B / 8.19kB   3
ac5303fe56b2   myubuntu    0.00%     1.348MiB / 3.785GiB   0.03%     1.44kB / 0B   0B / 0B       1

root@shivadocker:~#
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                                   NAMES
a804d4a7fc8d   nginx     "/docker-entrypoint.…"   2 minutes ago       Up 2 minutes       80/tcp                                  samba_mem
35b25f9840ad   nginx     "/docker-entrypoint.…"   42 minutes ago      Up 23 minutes      0.0.0.0:8001->80/tcp, :::8001->80/tcp   samba2
ac5303fe56b2   ubuntu    "/bin/bash"              About an hour ago   Up About an hour                                           myubuntu
root@shivadocker:~# docker update --memory 512m --memory-swap 1g samba2
samba2
root@shivadocker:~# docker stats
CONTAINER ID   NAME        CPU %     MEM USAGE / LIMIT     MEM %     NET I/O       BLOCK I/O     PIDS
a804d4a7fc8d   samba_mem   0.00%     3.508MiB / 512MiB     0.69%     866B / 0B     0B / 24.6kB   3
35b25f9840ad   samba2      0.00%     3.344MiB / 512MiB     0.65%     1.08kB / 0B   0B / 8.19kB   3
ac5303fe56b2   myubuntu    0.00%     1.348MiB / 3.785GiB   0.03%     1.44kB / 0B   0B / 0B       1

root@shivadocker:~#


```

- What we can do in running container
- 1st  we can rename 2nd  we can update assigned resource
