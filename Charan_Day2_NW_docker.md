###  Docker NETWORK

```
(https://www.redhat.com/sysadmin/7-linux-namespaces)[namespace]  

Process isolation (PID namespace): each session is isolated  
A PID, or process ID helps a system track a specific task on a computer. When you launch Firefox on your computer, it will have a PID associated with it.

Network interfaces (net namespace): for create network cards also isolated

Cgroup:  CPU, RAM, block I/O are isolated
cgroups are a mechanism for controlling system resources. When a cgroup is active, it can control the amount of CPU, RAM, block I/O, and some other facets which a process may consume. By default, cgroups are created in the virtual filesystem /sys/fs/cgroup.
```
- container life cycle

```
docker create
docker pull
docker start
docker rm
```

- Before create custom network below are the network interface   
```
root@shivadocker:~# docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
b3e3d377767e   bridge    bridge    local
1c37a4637ce8   host      host      local
5f30dcabf519   none      null      local
root@shivadocker:~# ifconfig
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:5aff:fe5f:b367  prefixlen 64  scopeid 0x20<link>
        ether 02:42:5a:5f:b3:67  txqueuelen 0  (Ethernet)
        RX packets 92  bytes 6323 (6.3 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 94  bytes 8564 (8.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.29.26  netmask 255.255.255.0  broadcast 192.168.29.255
        inet6 fe80::20c:29ff:feab:9638  prefixlen 64  scopeid 0x20<link>
        inet6 2405:201:c00a:7884:20c:29ff:feab:9638  prefixlen 64  scopeid 0x0<global>
        ether 00:0c:29:ab:96:38  txqueuelen 1000  (Ethernet)
        RX packets 344889  bytes 451264198 (451.2 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 84449  bytes 9001199 (9.0 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 502  bytes 52235 (52.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 502  bytes 52235 (52.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@shivadocker:~#

```

 - After create custom network below are the network interface  (br-e917bd3fde52)

```

root@shivadocker:~# docker network create my_network --driver bridge
e917bd3fde5295ce8561876605e3571d11178b1eb3d698afdde3377e8500ac9d
root@shivadocker:~# docker network ls
NETWORK ID     NAME         DRIVER    SCOPE
b3e3d377767e   bridge       bridge    local
1c37a4637ce8   host         host      local
e917bd3fde52   my_network   bridge    local
5f30dcabf519   none         null      local
root@shivadocker:~# ifconfig
br-e917bd3fde52: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.20.0.1  netmask 255.255.0.0  broadcast 172.20.255.255
        ether 02:42:a2:5a:64:de  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:5aff:fe5f:b367  prefixlen 64  scopeid 0x20<link>
        ether 02:42:5a:5f:b3:67  txqueuelen 0  (Ethernet)
        RX packets 92  bytes 6323 (6.3 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 94  bytes 8564 (8.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.29.26  netmask 255.255.255.0  broadcast 192.168.29.255
        inet6 fe80::20c:29ff:feab:9638  prefixlen 64  scopeid 0x20<link>
        inet6 2405:201:c00a:7884:20c:29ff:feab:9638  prefixlen 64  scopeid 0x0<global>
        ether 00:0c:29:ab:96:38  txqueuelen 1000  (Ethernet)
        RX packets 345331  bytes 451297858 (451.2 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 84679  bytes 9021593 (9.0 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 502  bytes 52235 (52.2 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 502  bytes 52235 (52.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

root@shivadocker:~#

root@shivadocker:~# docker network inspect my_network
[
    {
        "Name": "my_network",
        "Id": "e917bd3fde5295ce8561876605e3571d11178b1eb3d698afdde3377e8500ac9d",
        "Created": "2024-08-27T09:20:29.799011869Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.20.0.0/16",
                    "Gateway": "172.20.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]


```


- Custom NETWORK will ping host ( DNS and NAT)

```
root@shivadocker:~# docker images
REPOSITORY   TAG       IMAGE ID       CREATED         SIZE
nginx        latest    5ef79149e0ec   12 days ago     188MB
busybox      latest    65ad0d468eb1   15 months ago   4.26MB
root@shivadocker:~# docker network ls
NETWORK ID     NAME         DRIVER    SCOPE
b3e3d377767e   bridge       bridge    local
1c37a4637ce8   host         host      local
e917bd3fde52   my_network   bridge    local
5f30dcabf519   none         null      local
root@shivadocker:~# docker run -d --name samba_ng -p 8900:80 --network my_network nginx
1c919a95964c7ee5942ef2369dc6fb0446e911147e4974158706a7838169be82
root@shivadocker:~# docker run -d --name dridge_ng -p 8100:80  nginx
6d6a82142b1cd674f2235abf7e8bff3080ffd4cd7a9109498e2567210ef2cab0
root@shivadocker:~# docker run -dit --name bb01 --network my_network busybox
e43768d4a77db8d95bbfbbbee24560c89a335f46971358d486c566335948937d
root@shivadocker:~# docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                   NAMES
e43768d4a77d   busybox   "sh"                     5 seconds ago        Up 4 seconds                                                bb01
6d6a82142b1c   nginx     "/docker-entrypoint.…"   45 seconds ago       Up 44 seconds       0.0.0.0:8100->80/tcp, :::8100->80/tcp   dridge_ng
1c919a95964c   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   0.0.0.0:8900->80/tcp, :::8900->80/tcp   samba_ng
root@shivadocker:~#
root@shivadocker:~#
root@shivadocker:~# docker exec -it bb01 ping dridge_ng
ping: bad address 'dridge_ng'
root@shivadocker:~# docker exec -it bb01 ping samba_ng
PING samba_ng (172.20.0.2): 56 data bytes
64 bytes from 172.20.0.2: seq=0 ttl=64 time=0.272 ms
64 bytes from 172.20.0.2: seq=1 ttl=64 time=0.069 ms
64 bytes from 172.20.0.2: seq=2 ttl=64 time=0.193 ms
^C


--- samba_ng ping statistics ---
3 packets transmitted, 3 packets received, 0% packet loss
round-trip min/avg/max = 0.069/0.178/0.272 ms
root@shivadocker:~# docker inspect dridge_ng | grep -i "IPAddress"
            "SecondaryIPAddresses": null,
            "IPAddress": "172.17.0.2",
                    "IPAddress": "172.17.0.2",
root@shivadocker:~# docker exec -it bb01 ping 172.17.0.2
PING 172.17.0.2 (172.17.0.2): 56 data bytes
^C
--- 172.17.0.2 ping statistics ---
9 packets transmitted, 0 packets received, 100% packet loss
root@shivadocker:~#
root@shivadocker:~# docker exec -it bb01 ping 172.17.0.2
PING 172.17.0.2 (172.17.0.2): 56 data bytes
^C
--- 172.17.0.2 ping statistics ---
10 packets transmitted, 0 packets received, 100% packet loss
root@shivadocker:~#
root@shivadocker:~#
root@shivadocker:~# docker inspect samba_ng | grep -i "IPAddress"
            "SecondaryIPAddresses": null,
            "IPAddress": "",
                    "IPAddress": "172.20.0.2",
root@shivadocker:~# docker exec -it bb01 ping 172.20.0.2
PING 172.20.0.2 (172.20.0.2): 56 data bytes
64 bytes from 172.20.0.2: seq=0 ttl=64 time=0.264 ms
64 bytes from 172.20.0.2: seq=1 ttl=64 time=0.192 ms
64 bytes from 172.20.0.2: seq=2 ttl=64 time=0.330 ms
64 bytes from 172.20.0.2: seq=3 ttl=64 time=0.191 ms
64 bytes from 172.20.0.2: seq=4 ttl=64 time=0.195 ms
^C
--- 172.20.0.2 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max = 0.191/0.234/0.330 ms
root@shivadocker:~#

```
- once container is stated  new  network interfaces will create  
- 3 container are created respective interface also created those are (veth1ffec58,veth5764d55,veth72463c0)
- if we stop 3 container interface also will remove

```
root@shivadocker:~# docker ps -a
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                   NAMES
e43768d4a77d   busybox   "sh"                     9 minutes ago    Up 9 minutes                                            bb01
6d6a82142b1c   nginx     "/docker-entrypoint.…"   9 minutes ago    Up 9 minutes    0.0.0.0:8100->80/tcp, :::8100->80/tcp   dridge_ng
1c919a95964c   nginx     "/docker-entrypoint.…"   10 minutes ago   Up 10 minutes   0.0.0.0:8900->80/tcp, :::8900->80/tcp   samba_ng
root@shivadocker:~# ifconfig -a
br-e917bd3fde52: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.20.0.1  netmask 255.255.0.0  broadcast 172.20.255.255
        inet6 fe80::42:a2ff:fe5a:64de  prefixlen 64  scopeid 0x20<link>
        ether 02:42:a2:5a:64:de  txqueuelen 0  (Ethernet)
        RX packets 22  bytes 1680 (1.6 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7  bytes 610 (610.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

docker0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        inet6 fe80::42:5aff:fe5f:b367  prefixlen 64  scopeid 0x20<link>
        ether 02:42:5a:5f:b3:67  txqueuelen 0  (Ethernet)
        RX packets 92  bytes 6323 (6.3 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 96  bytes 8784 (8.7 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

ens33: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.29.26  netmask 255.255.255.0  broadcast 192.168.29.255
        inet6 fe80::20c:29ff:feab:9638  prefixlen 64  scopeid 0x20<link>
        inet6 2405:201:c00a:7884:20c:29ff:feab:9638  prefixlen 64  scopeid 0x0<global>
        ether 00:0c:29:ab:96:38  txqueuelen 1000  (Ethernet)
        RX packets 347743  bytes 451484594 (451.4 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 85794  bytes 9120432 (9.1 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 510  bytes 52763 (52.7 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 510  bytes 52763 (52.7 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth1ffec58: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::600a:a4ff:fed7:77d3  prefixlen 64  scopeid 0x20<link>
        ether 62:0a:a4:d7:77:d3  txqueuelen 0  (Ethernet)
        RX packets 33  bytes 2898 (2.8 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 27  bytes 2042 (2.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth5764d55: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::b429:15ff:fe75:7ffe  prefixlen 64  scopeid 0x20<link>
        ether b6:29:15:75:7f:fe  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15  bytes 1226 (1.2 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

veth72463c0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet6 fe80::4419:75ff:fe9c:a581  prefixlen 64  scopeid 0x20<link>
        ether 46:19:75:9c:a5:81  txqueuelen 0  (Ethernet)
        RX packets 12  bytes 952 (952.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 31  bytes 2526 (2.5 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


```
