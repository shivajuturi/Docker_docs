
- install docker

- /lib/systemd/system/containerd.service
- /lib/systemd/system/docker.socket
- /var/run/docker.sock
- /usr/lib/systemd/system/docker.service  ( in Volumes we will add external volume)

- /var/lib/docker
```
shiva@shivadocker:~$ sudo apt install docker.io
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  bridge-utils containerd dns-root-data dnsmasq-base pigz runc ubuntu-fan
Suggested packages:
  ifupdown aufs-tools cgroupfs-mount | cgroup-lite debootstrap docker-doc rinse zfs-fuse | zfsutils
The following NEW packages will be installed:
  bridge-utils containerd dns-root-data dnsmasq-base docker.io pigz runc ubuntu-fan
0 upgraded, 8 newly installed, 0 to remove and 38 not upgraded.
Need to get 75.5 MB of archives.
After this operation, 284 MB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://in.archive.ubuntu.com/ubuntu jammy/universe amd64 pigz amd64 2.6-1 [63.6 kB]
Get:2 http://in.archive.ubuntu.com/ubuntu jammy/main amd64 bridge-utils amd64 1.7-1ubuntu3 [34.4 kB]
Get:3 http://in.archive.ubuntu.com/ubuntu jammy-updates/main amd64 runc amd64 1.1.12-0ubuntu2~22.04.1 [8,405 kB]
Get:4 http://in.archive.ubuntu.com/ubuntu jammy-updates/main amd64 containerd amd64 1.7.12-0ubuntu2~22.04.1 [37.8 MB]
Get:5 http://in.archive.ubuntu.com/ubuntu jammy-updates/main amd64 dns-root-data all 2023112702~ubuntu0.22.04.1 [5,136 B]
Get:6 http://in.archive.ubuntu.com/ubuntu jammy-updates/main amd64 dnsmasq-base amd64 2.90-0ubuntu0.22.04.1 [374 kB]
Get:7 http://in.archive.ubuntu.com/ubuntu jammy-updates/universe amd64 docker.io amd64 24.0.7-0ubuntu2~22.04.1 [28.8 MB]
Get:8 http://in.archive.ubuntu.com/ubuntu jammy/universe amd64 ubuntu-fan all 0.12.16 [35.2 kB]
Fetched 75.5 MB in 9s (8,689 kB/s)
Preconfiguring packages ...
Selecting previously unselected package pigz.
(Reading database ... 74664 files and directories currently installed.)
Preparing to unpack .../0-pigz_2.6-1_amd64.deb ...
Unpacking pigz (2.6-1) ...
Selecting previously unselected package bridge-utils.
Preparing to unpack .../1-bridge-utils_1.7-1ubuntu3_amd64.deb ...
Unpacking bridge-utils (1.7-1ubuntu3) ...
Selecting previously unselected package runc.
Preparing to unpack .../2-runc_1.1.12-0ubuntu2~22.04.1_amd64.deb ...
Unpacking runc (1.1.12-0ubuntu2~22.04.1) ...
Selecting previously unselected package containerd.
Preparing to unpack .../3-containerd_1.7.12-0ubuntu2~22.04.1_amd64.deb ...
Unpacking containerd (1.7.12-0ubuntu2~22.04.1) ...
Selecting previously unselected package dns-root-data.
Preparing to unpack .../4-dns-root-data_2023112702~ubuntu0.22.04.1_all.deb ...
Unpacking dns-root-data (2023112702~ubuntu0.22.04.1) ...
Selecting previously unselected package dnsmasq-base.
Preparing to unpack .../5-dnsmasq-base_2.90-0ubuntu0.22.04.1_amd64.deb ...
Unpacking dnsmasq-base (2.90-0ubuntu0.22.04.1) ...
Selecting previously unselected package docker.io.
Preparing to unpack .../6-docker.io_24.0.7-0ubuntu2~22.04.1_amd64.deb ...
Unpacking docker.io (24.0.7-0ubuntu2~22.04.1) ...
Selecting previously unselected package ubuntu-fan.
Preparing to unpack .../7-ubuntu-fan_0.12.16_all.deb ...
Unpacking ubuntu-fan (0.12.16) ...
Setting up dnsmasq-base (2.90-0ubuntu0.22.04.1) ...
Setting up runc (1.1.12-0ubuntu2~22.04.1) ...
Setting up dns-root-data (2023112702~ubuntu0.22.04.1) ...
Setting up bridge-utils (1.7-1ubuntu3) ...
Setting up pigz (2.6-1) ...
Setting up containerd (1.7.12-0ubuntu2~22.04.1) ...
Created symlink /etc/systemd/system/multi-user.target.wants/containerd.service → /lib/systemd/system/containerd.service.
Setting up ubuntu-fan (0.12.16) ...
Created symlink /etc/systemd/system/multi-user.target.wants/ubuntu-fan.service → /lib/systemd/system/ubuntu-fan.service.
Setting up docker.io (24.0.7-0ubuntu2~22.04.1) ...
Adding group `docker' (GID 119) ...
Done.
Created symlink /etc/systemd/system/multi-user.target.wants/docker.service → /lib/systemd/system/docker.service.
Created symlink /etc/systemd/system/sockets.target.wants/docker.socket → /lib/systemd/system/docker.socket.
Processing triggers for dbus (1.12.20-2ubuntu4.1) ...
Processing triggers for man-db (2.10.2-1) ...
Scanning processes...
Scanning linux images...

Running kernel seems to be up-to-date.

No services need to be restarted.

No containers need to be restarted.

No user sessions are running outdated binaries.



```

- Docker Host network
- if container is created with network as host (container used docker server ip address ) if you check ip of container it will not display via docker inspect web02
- if container is created with network as host ( Port forward also will not work )
```
root@shivadocker:~# docker run -d --name web01 -p 8080:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
e4fff0779e6d: Pull complete
2a0cb278fd9f: Downloading [===============>                                   ]  12.79MB/41.88MB
2a0cb278fd9f: Pull complete
7045d6c32ae2: Pull complete
03de31afb035: Pull complete
0f17be8dcff2: Pull complete
14b7e5e8f394: Pull complete
23fa5a7b99a6: Pull complete
Digest: sha256:447a8665cc1dab95b1ca778e162215839ccbb9189104c79d7ec3a81e14577add
Status: Downloaded newer image for nginx:latest
32411c08ea5704ad729e087fe4c0676bd4ad9b125aa520bc7bcebb7eafe2d390
root@shivadocker:~#
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
32411c08ea57   nginx     "/docker-entrypoint.…"   36 seconds ago   Up 35 seconds   0.0.0.0:8080->80/tcp, :::8080->80/tcp   web01
root@shivadocker:~# docker run -d --name web02 --network host  nginx
c80c82ce8d00790181464eb685dfcc725f9b1e4f57716c7ca26683d18462fd23
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                   NAMES
c80c82ce8d00   nginx     "/docker-entrypoint.…"   3 seconds ago        Up 3 seconds                                                web02
32411c08ea57   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8080->80/tcp, :::8080->80/tcp   web01

root@shivadocker:~# docker run -d --name web03 --network host -p 8000:80 nginx
WARNING: Published ports are discarded when using host network mode
a441d81420c8c9a92a32acc310c6e01438ff8ac0927bfbd41f964f55ea9c8c96
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS                     PORTS                                   NAMES
a441d81420c8   nginx     "/docker-entrypoint.…"   9 seconds ago        Exited (1) 6 seconds ago                                           web03
c80c82ce8d00   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute                                                  web02
32411c08ea57   nginx     "/docker-entrypoint.…"   2 minutes ago        Up 2 minutes               0.0.0.0:8080->80/tcp, :::8080->80/tcp   web01

root@shivadocker:~# docker logs web03
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/08/26 10:24:57 [emerg] 1#1: bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
2024/08/26 10:24:57 [emerg] 1#1: bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
2024/08/26 10:24:57 [notice] 1#1: try again to bind() after 500ms
2024/08/26 10:24:57 [emerg] 1#1: bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
2024/08/26 10:24:57 [emerg] 1#1: bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
2024/08/26 10:24:57 [notice] 1#1: try again to bind() after 500ms
2024/08/26 10:24:57 [emerg] 1#1: bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
2024/08/26 10:24:57 [emerg] 1#1: bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
2024/08/26 10:24:57 [notice] 1#1: try again to bind() after 500ms
2024/08/26 10:24:57 [emerg] 1#1: bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
2024/08/26 10:24:57 [emerg] 1#1: bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
2024/08/26 10:24:57 [notice] 1#1: try again to bind() after 500ms
2024/08/26 10:24:57 [emerg] 1#1: bind() to 0.0.0.0:80 failed (98: Address already in use)
nginx: [emerg] bind() to 0.0.0.0:80 failed (98: Address already in use)
2024/08/26 10:24:57 [emerg] 1#1: bind() to [::]:80 failed (98: Address already in use)
nginx: [emerg] bind() to [::]:80 failed (98: Address already in use)
2024/08/26 10:24:57 [notice] 1#1: try again to bind() after 500ms
2024/08/26 10:24:57 [emerg] 1#1: still could not bind()
nginx: [emerg] still could not bind()
root@shivadocker:~#

```


```
root@shivadocker:~# docker inspect web01 | grep -i
root@shivadocker:~# docker inspect web01 | grep -i "IPAddress"
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",


root@shivadocker:~# docker inspect web02 | grep -i "IPAddress"
            "SecondaryIPAddresses": null,
            "IPAddress": "",
                    "IPAddress": "",
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS                                   NAMES
15425efc4f5c   nginx     "/docker-entrypoint.…"   2 minutes ago    Exited (1) 2 minutes ago                                            web04
a441d81420c8   nginx     "/docker-entrypoint.…"   11 minutes ago   Exited (1) 11 minutes ago                                           web03
c80c82ce8d00   nginx     "/docker-entrypoint.…"   12 minutes ago   Up 12 minutes                                                       web02
32411c08ea57   nginx     "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes               0.0.0.0:8080->80/tcp, :::8080->80/tcp   web01
root@shivadocker:~#

```
- web02 is network type is host .
- if i want to access web02  i need to use this ip in browser docker server ip/ docker host ip (192.168.29.26 )
- entire server only one host network container we can create .
- if we specify --network host  if we specify -p 8000:80 it wont take port forward

```
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS                      PORTS                                   NAMES
c80c82ce8d00   nginx     "/docker-entrypoint.…"   12 minutes ago   Up 12 minutes                                                       web02
32411c08ea57   nginx     "/docker-entrypoint.…"   14 minutes ago   Up 14 minutes               0.0.0.0:8080->80/tcp, :::8080->80/tcp   web01
root@shivadocker:~# ifconfig -a
docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:3fff:fec1:b707  prefixlen 64  scopeid 0x20<link>
        ether 02:42:3f:c1:b7:07  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 5  bytes 526 (526.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.29.26  netmask 255.255.255.0  broadcast 192.168.29.255
        inet6 2405:201:c00a:7884:20c:29ff:feab:9638  prefixlen 64  scopeid 0x0<global>
        inet6 fe80::20c:29ff:feab:9638  prefixlen 64  scopeid 0x20<link>
        ether 00:0c:29:ab:96:38  txqueuelen 1000  (Ethernet)
        RX packets 136820  bytes 188885405 (188.8 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 34916  bytes 3469157 (3.4 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 243  bytes 23915 (23.9 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 243  bytes 23915 (23.9 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth266598e: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::3810:77ff:feb0:ba37  prefixlen 64  scopeid 0x20<link>
        ether 3a:10:77:b0:ba:37  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 19  bytes 1602 (1.6 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@shivadocker:~#

```
