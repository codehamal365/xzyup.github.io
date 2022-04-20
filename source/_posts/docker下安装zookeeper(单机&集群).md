---
title: docker安装zookeeper
tags:
  - docker
  - zookeeper
abbrlink: c5fb
---

## docker下安装zookeeper

启动docker后，先查看zookeeper有哪些选择。

```bash
docker search zookeeper	
```

![](https://raw.githubusercontent.com/xzyup/image/master/202203191704919.png)

选择官方版本，下载

~~~bash
docker pull zookeeper
~~~

查看镜像

~~~bash
docker images

REPOSITORY                  TAG                 IMAGE ID            CREATED             SIZE
docker.io/tomcat            latest              bb832de23021        2 days ago          680 MB
docker.io/vernemq/vernemq   latest              9ff6861690a3        3 days ago          159 MB
docker.io/zookeeper         latest              2a33b1a1e11a        12 days ago         278 MB
~~~

`docker inspect zookeeper`查看镜像详情

~~~bash
[
    {
        "Id": "sha256:2a33b1a1e11ad0f64eba1364828fcbd4f60dd0b140e1d32b23c4f22e4c2df31d",
        "RepoTags": [
            "docker.io/zookeeper:latest"
        ],
        "RepoDigests": [
            "docker.io/zookeeper@sha256:61463427d81ec53585711fbce35ffea147b52f6c81b9283a67bff82efe9ae202"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2021-09-04T14:31:04.949531564Z",
        "Container": "a4d61f2a3bb7f0a594218851b0215132ea195f57df5d3e1b3a3c78d5d4da4b56",
        "ContainerConfig": {
            "Hostname": "a4d61f2a3bb7",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "2181/tcp": {},
                "2888/tcp": {},
                "3888/tcp": {},
                "8080/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/openjdk-11/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/apache-zookeeper-3.7.0-bin/bin",
                "JAVA_HOME=/usr/local/openjdk-11",
                "LANG=C.UTF-8",
                "JAVA_VERSION=11.0.12",
                "ZOO_CONF_DIR=/conf",
                "ZOO_DATA_DIR=/data",
                "ZOO_DATA_LOG_DIR=/datalog",
                "ZOO_LOG_DIR=/logs",
                "ZOO_TICK_TIME=2000",
                "ZOO_INIT_LIMIT=5",
                "ZOO_SYNC_LIMIT=2",
                "ZOO_AUTOPURGE_PURGEINTERVAL=0",
                "ZOO_AUTOPURGE_SNAPRETAINCOUNT=3",
                "ZOO_MAX_CLIENT_CNXNS=60",
                "ZOO_STANDALONE_ENABLED=true",
                "ZOO_ADMINSERVER_ENABLED=true",
                "ZOOCFGDIR=/conf"
            ],
            "Cmd": [
                "/bin/sh",
                "-c",
                "#(nop) ",
                "CMD [\"zkServer.sh\" \"start-foreground\"]"
            ],
            "Image": "sha256:83871249bd21f7df0e3f9a25c365f2fe482cd839a62030a8cb819622a61757de",
            "Volumes": {
                "/data": {},
                "/datalog": {},
                "/logs": {}
            },
            "WorkingDir": "/apache-zookeeper-3.7.0-bin",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {}
        },
        "DockerVersion": "20.10.7",
        "Author": "",
        "Config": {
            "Hostname": "",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "2181/tcp": {},
                "2888/tcp": {},
                "3888/tcp": {},
                "8080/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/openjdk-11/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/apache-zookeeper-3.7.0-bin/bin",
                "JAVA_HOME=/usr/local/openjdk-11",
                "LANG=C.UTF-8",
                "JAVA_VERSION=11.0.12",
                "ZOO_CONF_DIR=/conf",
                "ZOO_DATA_DIR=/data",
                "ZOO_DATA_LOG_DIR=/datalog",
                "ZOO_LOG_DIR=/logs",
                "ZOO_TICK_TIME=2000",
                "ZOO_INIT_LIMIT=5",
                "ZOO_SYNC_LIMIT=2",
                "ZOO_AUTOPURGE_PURGEINTERVAL=0",
                "ZOO_AUTOPURGE_SNAPRETAINCOUNT=3",
                "ZOO_MAX_CLIENT_CNXNS=60",
                "ZOO_STANDALONE_ENABLED=true",
                "ZOO_ADMINSERVER_ENABLED=true",
                "ZOOCFGDIR=/conf"
            ],
            "Cmd": [
                "zkServer.sh",
                "start-foreground"
            ],
            "Image": "sha256:83871249bd21f7df0e3f9a25c365f2fe482cd839a62030a8cb819622a61757de",
            "Volumes": {
                "/data": {},
                "/datalog": {},
                "/logs": {}
            },
            "WorkingDir": "/apache-zookeeper-3.7.0-bin",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": null
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 277857721,
        "VirtualSize": 277857721,
        "GraphDriver": {
            "Name": "overlay2",
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/c23c13970f98f9607674f41df40d0ae9631e3f733beb7f43b534b399903bdb6e/diff:/var/lib/docker/overlay2/edba8275449661a08f98aa8358acccda09f636ff63b62745cf032baaac6a83b6/diff:/var/lib/docker/overlay2/053a067737b9474d966509e0bd2bad945a8783d4b391f68aa250e37d986ca82c/diff:/var/lib/docker/overlay2/60dce72476a90d10650946e1ade294d09f0042dff3600acc0a71b3d0c790672d/diff:/var/lib/docker/overlay2/85c7adba7770d95daed846466aac57e2a5fa73df83387fd5d1edfaf4f2c2247a/diff:/var/lib/docker/overlay2/941d4279fc8ad098fa272415524753d5eae149f1b65dae1c58f358b0dcb25a36/diff:/var/lib/docker/overlay2/6a98f2f2f557a9cacf6487844baad942da9af5fb86263c7640106763ace7f8a7/diff",
                "MergedDir": "/var/lib/docker/overlay2/72999c7c2abd5117ef5a8c75bd1091e3f0919b10aaf19cb8706c9431e07f24a5/merged",
                "UpperDir": "/var/lib/docker/overlay2/72999c7c2abd5117ef5a8c75bd1091e3f0919b10aaf19cb8706c9431e07f24a5/diff",
                "WorkDir": "/var/lib/docker/overlay2/72999c7c2abd5117ef5a8c75bd1091e3f0919b10aaf19cb8706c9431e07f24a5/work"
            }
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:ba5a5fe4330168081f2a7e46f72c7552456d4d604ad27feadbe76ec86598587e",
                "sha256:2605f54a59eca936809baec0b33d9333bc5d3cdc57a9ea6c395abb766bea73ee",
                "sha256:9be53ed84a753f72f253cd789dd306a611d183b306ae265a8b4d7bbd167bac8a",
                "sha256:27947c0376868058509877698b397812424ee477f7fbc3cf76b547777c048410",
                "sha256:f290b03f22dda15089551b9c9b7f43f5e239da5c3c3098c1da84b2e67aa204ee",
                "sha256:9439b4444bd0ad670d99026cdce9c06602863bc37910a0a62a0b9d5f414155b5",
                "sha256:02a354ce9185f87185662d788cc1fcfc16b960bba27aa10d7729db37c395ea58",
                "sha256:662510598bd9d6b1166da778021b98007900dd4313ceed887d8ae0a8f8ff6ae2"
            ]
        }
    }
]
~~~

默认拉取最新的版本是3.7.0，如果想拉取其他版本，可以指定tag。

### 单机

~~~bash
# 启动容器
docker run -d -p 2181:2181 --name standalone-zookeeper --restart always zookeeper

# 查看容器
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                  NAMES
d8b7def1982c        zookeeper           "/docker-entrypoin..."   28 minutes ago      Up 28 minutes       2888/tcp, 3888/tcp, 0.0.0.0:2181->2181/tcp, 8080/tcp   standalone-zookeeper
fbf17b466b4a        tomcat              "catalina.sh run"        12 hours ago        Up 12 hours         0.0.0.0:8080->8080/tcp                                 tomcat

# 进入容器交互模式
docker exec -it standalone-zookeeper bash

# 运行zk客户端
root@d8b7def1982c:/apache-zookeeper-3.7.0-bin# ./bin/zkCli.sh

[zk: localhost:2181(CONNECTED) 0] ls /
[zookeeper]
[zk: localhost:2181(CONNECTED) 1] quit

WATCHER::

WatchedEvent state:Closed type:None path:null
2021-09-16 22:35:23,414 [myid:] - INFO  [main:ZooKeeper@1232] - Session: 0x10002a3f7b70002 closed
2021-09-16 22:35:23,416 [myid:] - ERROR [main:ServiceUtils@42] - Exiting JVM with code 0
2021-09-16 22:35:23,420 [myid:] - INFO  [main-EventThread:ClientCnxn$EventThread@570] - EventThread shut down for session: 0x10002a3f7b70002
~~~

查看虚拟机ip

~~~bash
ifconfig

enp0s8: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.56.102  netmask 255.255.255.0  broadcast 192.168.56.255
        inet6 fe80::f449:6222:f3f0:156b  prefixlen 64  scopeid 0x20<link>
        ether 08:00:27:a3:2c:01  txqueuelen 1000  (Ethernet)
        RX packets 315193  bytes 24898970 (23.7 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 281868  bytes 59276159 (56.5 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
~~~

外部访问地址：192.168.56.102:2181



### 集群

**环境**：单台宿主机（`192.168.1.9`），启动三个zookeeper容器。

**这里涉及的问题，就是docker容器之前通信的问题，这个很重要。**

~~~bash
[root@localhost ~]# docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
f7b764ef3634        bridge              bridge              local
15e39185d267        host                host                local
fa65da9323b5        none                null                local
~~~

Docker有三种网络模式，bridge、host、none，在你创建容器的时候，不指定--network默认是bridge。

bridge：为每一个容器分配IP，并将容器连接到一个docker0虚拟网桥，通过docker0网桥与宿主机通信。也就是说，**此模式下，你不能用宿主机的IP+容器映射端口来进行Docker容器之间的通信。**

host：容器不会虚拟自己的网卡，配置自己的IP，而是使用宿主机的IP和端口。这样一来，**Docker容器之间的通信就可以用宿主机的IP+容器映射端口**

none：无网络。

---

现在本地创建目录：

~~~bash
[root@localhost admin]# mkdir /usr/local/zookeeper-cluster
[root@localhost admin]# mkdir /usr/local/zookeeper-cluster/node1
[root@localhost admin]# mkdir /usr/local/zookeeper-cluster/node2
[root@localhost admin]# mkdir /usr/local/zookeeper-cluster/node3
[root@localhost admin]# ll /usr/local/zookeeper-cluster/
total 0
drwxr-xr-x. 2 root root 6 Aug 28 23:02 node1
drwxr-xr-x. 2 root root 6 Aug 28 23:02 node2
drwxr-xr-x. 2 root root 6 Aug 28 23:02 node3
~~~

然后执行命令启动：

~~~bash
docker run -d -p 2181:2181 -p 2888:2888 -p 3888:3888 --name zookeeper_node1 --privileged --restart always \
-v /usr/local/zookeeper-cluster/node1/volumes/data:/data \
-v /usr/local/zookeeper-cluster/node1/volumes/datalog:/datalog \
-v /usr/local/zookeeper-cluster/node1/volumes/logs:/logs \
-e ZOO_MY_ID=1 \
-e "ZOO_SERVERS=server.1=192.168.1.9:2888:3888;2181 server.2=192.168.1.9:2889:3889;2182 server.3=192.168.1.9:2890:3890;2183" zookeeper

docker run -d -p 2182:2181 -p 2889:2888 -p 3889:3888 --name zookeeper_node2 --privileged --restart always \
-v /usr/local/zookeeper-cluster/node2/volumes/data:/data \
-v /usr/local/zookeeper-cluster/node2/volumes/datalog:/datalog \
-v /usr/local/zookeeper-cluster/node2/volumes/logs:/logs \
-e ZOO_MY_ID=2 \
-e "ZOO_SERVERS=server.1=192.168.1.9:2888:3888;2181 server.2=192.168.1.9:2889:3889;2182 server.3=192.168.1.9:2890:3890;2183" zookeeper

docker run -d -p 2183:2181 -p 2890:2888 -p 3890:3888 --name zookeeper_node3 --privileged --restart always \
-v /usr/local/zookeeper-cluster/node3/volumes/data:/data \
-v /usr/local/zookeeper-cluster/node3/volumes/datalog:/datalog \
-v /usr/local/zookeeper-cluster/node3/volumes/logs:/logs \
-e ZOO_MY_ID=3 \
-e "ZOO_SERVERS=server.1=192.168.1.9:2888:3888;2181 server.2=192.168.1.9:2889:3889;2182 server.3=192.168.1.9:2890:3890;2183" zookeeper
~~~

查看容器启动情况

~~~bash
[root@localhost admin]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                                              NAMES
6dabae1d92f0        3487af26dee9        "/docker-entrypoin..."   31 seconds ago      Up 29 seconds       8080/tcp, 0.0.0.0:2183->2181/tcp, 0.0.0.0:2890->2888/tcp, 0.0.0.0:3890->3888/tcp   zookeeper_node3
dbb7f1f323a0        3487af26dee9        "/docker-entrypoin..."   36 seconds ago      Up 35 seconds       8080/tcp, 0.0.0.0:2182->2181/tcp, 0.0.0.0:2889->2888/tcp, 0.0.0.0:3889->3888/tcp   zookeeper_node2
4bfa6bbeb936        3487af26dee9        "/docker-entrypoin..."   46 seconds ago      Up 45 seconds       0.0.0.0:2181->2181/tcp, 0.0.0.0:2888->2888/tcp, 0.0.0.0:3888->3888/tcp, 8080/tcp   zookeeper_node1
~~~

我们看下节点1的启动日志

~~~bash
[root@localhost admin]# docker logs -f zookeeper_node1
ZooKeeper JMX enabled by default

...

2019-08-29 09:20:22,665 [myid:1] - WARN  [WorkerSender[myid=1]:QuorumCnxManager@677] - Cannot open channel to 2 at election address /192.168.1.9:3889
java.net.ConnectException: Connection refused (Connection refused)
    at java.net.PlainSocketImpl.socketConnect(Native Method)
    at java.net.AbstractPlainSocketImpl.doConnect(AbstractPlainSocketImpl.java:350)
    at java.net.AbstractPlainSocketImpl.connectToAddress(AbstractPlainSocketImpl.java:206)
    at java.net.AbstractPlainSocketImpl.connect(AbstractPlainSocketImpl.java:188)
    at java.net.SocksSocketImpl.connect(SocksSocketImpl.java:392)
    at java.net.Socket.connect(Socket.java:589)
    at org.apache.zookeeper.server.quorum.QuorumCnxManager.connectOne(QuorumCnxManager.java:648)
    at org.apache.zookeeper.server.quorum.QuorumCnxManager.connectOne(QuorumCnxManager.java:705)
    at org.apache.zookeeper.server.quorum.QuorumCnxManager.toSend(QuorumCnxManager.java:618)
    at org.apache.zookeeper.server.quorum.FastLeaderElection$Messenger$WorkerSender.process(FastLeaderElection.java:477)
    at org.apache.zookeeper.server.quorum.FastLeaderElection$Messenger$WorkerSender.run(FastLeaderElection.java:456)
    at java.lang.Thread.run(Thread.java:748)
2019-08-29 09:20:22,666 [myid:1] - WARN  [WorkerSender[myid=1]:QuorumCnxManager@677] - Cannot open channel to 3 at election address /192.168.192.128:3890
java.net.ConnectException: Connection refused (Connection refused)
    at java.net.PlainSocketImpl.socketConnect(Native Method)
    at java.net.AbstractPlainSocketImpl.doConnect(AbstractPlainSocketImpl.java:350)
    at java.net.AbstractPlainSocketImpl.connectToAddress(AbstractPlainSocketImpl.java:206)
    at java.net.AbstractPlainSocketImpl.connect(AbstractPlainSocketImpl.java:188)
    at java.net.SocksSocketImpl.connect(SocksSocketImpl.java:392)
    at java.net.Socket.connect(Socket.java:589)
    at org.apache.zookeeper.server.quorum.QuorumCnxManager.connectOne(QuorumCnxManager.java:648)
    at org.apache.zookeeper.server.quorum.QuorumCnxManager.connectOne(QuorumCnxManager.java:705)
    at org.apache.zookeeper.server.quorum.QuorumCnxManager.toSend(QuorumCnxManager.java:618)
    at org.apache.zookeeper.server.quorum.FastLeaderElection$Messenger$WorkerSender.process(FastLeaderElection.java:477)
    at org.apache.zookeeper.server.quorum.FastLeaderElection$Messenger$WorkerSender.run(FastLeaderElection.java:456)
    at java.lang.Thread.run(Thread.java:748)
~~~

连接不上2 和 3，为什么呢，因为在默认的Docker网络模式下，通过宿主机的IP+映射端口，根本找不到啊！他们有自己的IP啊！如下：

~~~bash
[root@localhost admin]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                                              NAMES
6dabae1d92f0        3487af26dee9        "/docker-entrypoin..."   31 seconds ago      Up 29 seconds       8080/tcp, 0.0.0.0:2183->2181/tcp, 0.0.0.0:2890->2888/tcp, 0.0.0.0:3890->3888/tcp   zookeeper_node3
dbb7f1f323a0        3487af26dee9        "/docker-entrypoin..."   36 seconds ago      Up 35 seconds       8080/tcp, 0.0.0.0:2182->2181/tcp, 0.0.0.0:2889->2888/tcp, 0.0.0.0:3889->3888/tcp   zookeeper_node2
4bfa6bbeb936        3487af26dee9        "/docker-entrypoin..."   46 seconds ago      Up 45 seconds       0.0.0.0:2181->2181/tcp, 0.0.0.0:2888->2888/tcp, 0.0.0.0:3888->3888/tcp, 8080/tcp   zookeeper_node1

[root@localhost ~]# docker inspect zookeeper_node1
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "f7b764ef3634342a04146929ae261dcc759001b312f5400a3639c9d66dcccc7e",
                    "EndpointID": "dd9bb88a24375814008903b056447ae85dc5ccc934eb69d80c3dcc71da8b424f",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03"
                }
            }
        }
    }
]

[root@localhost ~]# docker inspect zookeeper_node2
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "f7b764ef3634342a04146929ae261dcc759001b312f5400a3639c9d66dcccc7e",
                    "EndpointID": "dd9bb88a24375814008903b056447ae85dc5ccc934eb69d80c3dcc71da8b424f",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.4",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03"
                }
            }
        }
    }
]

[root@localhost ~]# docker inspect zookeeper_node3
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "f7b764ef3634342a04146929ae261dcc759001b312f5400a3639c9d66dcccc7e",
                    "EndpointID": "dd9bb88a24375814008903b056447ae85dc5ccc934eb69d80c3dcc71da8b424f",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.5",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03"
                }
            }
        }
    }
]
~~~

node1---172.17.0.3
node2---172.17.0.4
node3---172.17.0.5

既然我们知道了它有自己的IP，那又出现另一个问题了，就是它的ip是动态的，启动之前我们无法得知。**有个解决办法就是创建自己的bridge网络，然后创建容器的时候指定ip。**

**【正确方式开始】**

~~~bash
[root@localhost ~]# docker network create --driver bridge --subnet=172.18.0.0/16 --gateway=172.18.0.1 zoonet
7ca91b6fa816f91b43f04529b74bcd9fa5aadef41cd3b9df7371beb44e83663b
[root@localhost ~]# docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
f7b764ef3634        bridge              bridge              local
15e39185d267        host                host                local
fa65da9323b5        none                null                local
7ca91b6fa816        zoonet              bridge              local
[root@localhost ~]# docker network inspect zoonet
[
    {
        "Name": "zoonet",
        "Id": "7ca91b6fa816f91b43f04529b74bcd9fa5aadef41cd3b9df7371beb44e83663b",
        "Created": "2021-09-17T07:15:33.177645556+08:00",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
~~~

然后我们修改一下zookeeper容器的创建命令。【正确命令】

~~~bash
docker run -d -p 2181:2181 --name zookeeper_node1 --privileged --restart always --network zoonet --ip 172.18.0.2 \
-v /usr/local/zookeeper-cluster/node1/volumes/data:/data \
-v /usr/local/zookeeper-cluster/node1/volumes/datalog:/datalog \
-v /usr/local/zookeeper-cluster/node1/volumes/logs:/logs \
-e ZOO_MY_ID=1 \
-e "ZOO_SERVERS=server.1=172.18.0.2:2888:3888;2181 server.2=172.18.0.3:2888:3888;2181 server.3=172.18.0.4:2888:3888;2181" zookeeper

docker run -d -p 2182:2181 --name zookeeper_node2 --privileged --restart always --network zoonet --ip 172.18.0.3 \
-v /usr/local/zookeeper-cluster/node2/volumes/data:/data \
-v /usr/local/zookeeper-cluster/node2/volumes/datalog:/datalog \
-v /usr/local/zookeeper-cluster/node2/volumes/logs:/logs \
-e ZOO_MY_ID=2 \
-e "ZOO_SERVERS=server.1=172.18.0.2:2888:3888;2181 server.2=172.18.0.3:2888:3888;2181 server.3=172.18.0.4:2888:3888;2181" zookeeper

docker run -d -p 2183:2181 --name zookeeper_node3 --privileged --restart always --network zoonet --ip 172.18.0.4 \
-v /usr/local/zookeeper-cluster/node3/volumes/data:/data \
-v /usr/local/zookeeper-cluster/node3/volumes/datalog:/datalog \
-v /usr/local/zookeeper-cluster/node3/volumes/logs:/logs \
-e ZOO_MY_ID=3 \
-e "ZOO_SERVERS=server.1=172.18.0.2:2888:3888;2181 server.2=172.18.0.3:2888:3888;2181 server.3=172.18.0.4:2888:3888;2181" zookeeper


[root@localhost ~]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                  NAMES
5f35bdd41916        zookeeper           "/docker-entrypoin..."   3 minutes ago       Up 3 minutes        2888/tcp, 3888/tcp, 8080/tcp, 0.0.0.0:2183->2181/tcp   zookeeper_node3
c311e63820af        zookeeper           "/docker-entrypoin..."   4 minutes ago       Up 4 minutes        2888/tcp, 3888/tcp, 8080/tcp, 0.0.0.0:2182->2181/tcp   zookeeper_node2
249fa3c091cd        zookeeper           "/docker-entrypoin..."   4 minutes ago       Up 4 minutes        2888/tcp, 3888/tcp, 0.0.0.0:2181->2181/tcp, 8080/tcp   zookeeper_node1
fbf17b466b4a        tomcat              "catalina.sh run"        12 hours ago        Up 12 hours         0.0.0.0:8080->8080/tcp                                 tomcat
~~~

进入容器内部验证一下：

~~~bash
[root@localhost ~]# docker exec -it  zookeeper_node1 bash
root@249fa3c091cd:/apache-zookeeper-3.7.0-bin# ./bin/zkServer.sh status
ZooKeeper JMX enabled by default
Using config: /conf/zoo.cfg
Client port found: 2181. Client address: localhost. Client SSL: false.
Mode: follower
root@249fa3c091cd:/apache-zookeeper-3.7.0-bin# exit
exit
[root@localhost ~]# docker exec -it  zookeeper_node2 bash
root@c311e63820af:/apache-zookeeper-3.7.0-bin# ./bin/zkServer.sh status
ZooKeeper JMX enabled by default
Using config: /conf/zoo.cfg
Client port found: 2181. Client address: localhost. Client SSL: false.
Mode: leader
root@c311e63820af:/apache-zookeeper-3.7.0-bin# exit
exit
[root@localhost ~]# docker exec -it  zookeeper_node3 bash
root@5f35bdd41916:/apache-zookeeper-3.7.0-bin# ./bin/zkServer.sh status
ZooKeeper JMX enabled by default
Using config: /conf/zoo.cfg
Client port found: 2181. Client address: localhost. Client SSL: false.
Mode: follower
~~~

在验证一下创建节点：

~~~bash
# node3
root@5f35bdd41916:/apache-zookeeper-3.7.0-bin# ./bin/zkCli.sh 
Connecting to localhost:2181
2021-09-16 23:32:52,624 [myid:] - INFO  [main:Environment@98] - Client environment:zookeeper.version=3.7.0-e3704b390a6697bfdf4b0bef79e3da7a4f6bac4b, built on 2021-03-17 09:46 UTC
2021-09-16 23:32:52,629 [myid:] - INFO  [main:Environment@98] - Client environment:host.name=5f35bdd41916
2021-09-16 23:32:52,724 [myid:] - INFO  [main:Environment@98] - Client environment:java.version=11.0.12
2021-09-16 23:32:52,727 [myid:] - INFO  [main:Environment@98] - Client environment:java.vendor=Oracle Corporation
2021-09-16 23:32:52,728 [myid:] - INFO  [main:Environment@98] - Client environment:java.home=/usr/local/openjdk-11
2021-09-16 23:32:52,728 [myid:] - INFO  [main:Environment@98] - Client environment:java.class.path=/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/classes:/apache-zookeeper-3.7.0-bin/bin/../build/classes:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/lib/*.jar:/apache-zookeeper-3.7.0-bin/bin/../build/lib/*.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-prometheus-metrics-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-jute-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/snappy-java-1.1.7.7.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-log4j12-1.7.30.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-api-1.7.30.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_servlet-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_hotspot-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_common-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-unix-common-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-epoll-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-resolver-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-handler-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-common-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-codec-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-buffer-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/metrics-core-4.1.12.1.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/log4j-1.2.17.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jline-2.14.6.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-ajax-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-servlet-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-server-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-security-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-io-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-http-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/javax.servlet-api-3.1.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-databind-2.10.5.1.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-core-2.10.5.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-annotations-2.10.5.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/commons-cli-1.4.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/audience-annotations-0.12.0.jar:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-*.jar:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/src/main/resources/lib/*.jar:/conf:
2021-09-16 23:32:52,728 [myid:] - INFO  [main:Environment@98] - Client environment:java.library.path=/usr/java/packages/lib:/usr/lib64:/lib64:/lib:/usr/lib
2021-09-16 23:32:52,728 [myid:] - INFO  [main:Environment@98] - Client environment:java.io.tmpdir=/tmp
2021-09-16 23:32:52,728 [myid:] - INFO  [main:Environment@98] - Client environment:java.compiler=<NA>
2021-09-16 23:32:52,729 [myid:] - INFO  [main:Environment@98] - Client environment:os.name=Linux
2021-09-16 23:32:52,729 [myid:] - INFO  [main:Environment@98] - Client environment:os.arch=amd64
2021-09-16 23:32:52,729 [myid:] - INFO  [main:Environment@98] - Client environment:os.version=3.10.0-1062.el7.x86_64
2021-09-16 23:32:52,729 [myid:] - INFO  [main:Environment@98] - Client environment:user.name=root
2021-09-16 23:32:52,729 [myid:] - INFO  [main:Environment@98] - Client environment:user.home=/root
2021-09-16 23:32:52,729 [myid:] - INFO  [main:Environment@98] - Client environment:user.dir=/apache-zookeeper-3.7.0-bin
2021-09-16 23:32:52,729 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.free=10MB
2021-09-16 23:32:52,736 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.max=247MB
2021-09-16 23:32:52,736 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.total=15MB
2021-09-16 23:32:52,783 [myid:] - INFO  [main:ZooKeeper@637] - Initiating client connection, connectString=localhost:2181 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@4c70fda8
2021-09-16 23:32:52,788 [myid:] - INFO  [main:X509Util@77] - Setting -D jdk.tls.rejectClientInitiatedRenegotiation=true to disable client-initiated TLS renegotiation
2021-09-16 23:32:52,901 [myid:] - INFO  [main:ClientCnxnSocket@239] - jute.maxbuffer value is 1048575 Bytes
2021-09-16 23:32:53,214 [myid:] - INFO  [main:ClientCnxn@1726] - zookeeper.request.timeout value is 0. feature enabled=false
Welcome to ZooKeeper!
JLine support is enabled
2021-09-16 23:32:53,976 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1171] - Opening socket connection to server localhost/0:0:0:0:0:0:0:1:2181.
2021-09-16 23:32:53,979 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1173] - SASL config status: Will not attempt to authenticate using SASL (unknown error)
2021-09-16 23:32:54,145 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1005] - Socket connection established, initiating session, client: /0:0:0:0:0:0:0:1:55044, server: localhost/0:0:0:0:0:0:0:1:2181
2021-09-16 23:32:55,005 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1438] - Session establishment complete on server localhost/0:0:0:0:0:0:0:1:2181, session id = 0x30002ebbd490000, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null
[zk: localhost:2181(CONNECTED) 0] ls /
[zookeeper]
[zk: localhost:2181(CONNECTED) 1] create /hello
Created /hello
[zk: localhost:2181(CONNECTED) 2] 


# node1
[root@localhost ~]# docker exec -it  zookeeper_node1 bash
root@249fa3c091cd:/apache-zookeeper-3.7.0-bin# ./bin/zkCli.sh
Connecting to localhost:2181
2021-09-16 23:35:28,681 [myid:] - INFO  [main:Environment@98] - Client environment:zookeeper.version=3.7.0-e3704b390a6697bfdf4b0bef79e3da7a4f6bac4b, built on 2021-03-17 09:46 UTC
2021-09-16 23:35:28,783 [myid:] - INFO  [main:Environment@98] - Client environment:host.name=249fa3c091cd
2021-09-16 23:35:28,783 [myid:] - INFO  [main:Environment@98] - Client environment:java.version=11.0.12
2021-09-16 23:35:28,785 [myid:] - INFO  [main:Environment@98] - Client environment:java.vendor=Oracle Corporation
2021-09-16 23:35:28,785 [myid:] - INFO  [main:Environment@98] - Client environment:java.home=/usr/local/openjdk-11
2021-09-16 23:35:28,785 [myid:] - INFO  [main:Environment@98] - Client environment:java.class.path=/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/classes:/apache-zookeeper-3.7.0-bin/bin/../build/classes:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/lib/*.jar:/apache-zookeeper-3.7.0-bin/bin/../build/lib/*.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-prometheus-metrics-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-jute-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/snappy-java-1.1.7.7.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-log4j12-1.7.30.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-api-1.7.30.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_servlet-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_hotspot-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_common-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-unix-common-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-epoll-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-resolver-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-handler-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-common-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-codec-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-buffer-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/metrics-core-4.1.12.1.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/log4j-1.2.17.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jline-2.14.6.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-ajax-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-servlet-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-server-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-security-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-io-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-http-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/javax.servlet-api-3.1.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-databind-2.10.5.1.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-core-2.10.5.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-annotations-2.10.5.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/commons-cli-1.4.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/audience-annotations-0.12.0.jar:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-*.jar:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/src/main/resources/lib/*.jar:/conf:
2021-09-16 23:35:28,785 [myid:] - INFO  [main:Environment@98] - Client environment:java.library.path=/usr/java/packages/lib:/usr/lib64:/lib64:/lib:/usr/lib
2021-09-16 23:35:28,786 [myid:] - INFO  [main:Environment@98] - Client environment:java.io.tmpdir=/tmp
2021-09-16 23:35:28,786 [myid:] - INFO  [main:Environment@98] - Client environment:java.compiler=<NA>
2021-09-16 23:35:28,786 [myid:] - INFO  [main:Environment@98] - Client environment:os.name=Linux
2021-09-16 23:35:28,786 [myid:] - INFO  [main:Environment@98] - Client environment:os.arch=amd64
2021-09-16 23:35:28,786 [myid:] - INFO  [main:Environment@98] - Client environment:os.version=3.10.0-1062.el7.x86_64
2021-09-16 23:35:28,787 [myid:] - INFO  [main:Environment@98] - Client environment:user.name=root
2021-09-16 23:35:28,787 [myid:] - INFO  [main:Environment@98] - Client environment:user.home=/root
2021-09-16 23:35:28,787 [myid:] - INFO  [main:Environment@98] - Client environment:user.dir=/apache-zookeeper-3.7.0-bin
2021-09-16 23:35:28,787 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.free=10MB
2021-09-16 23:35:28,790 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.max=247MB
2021-09-16 23:35:28,790 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.total=15MB
2021-09-16 23:35:28,896 [myid:] - INFO  [main:ZooKeeper@637] - Initiating client connection, connectString=localhost:2181 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@4c70fda8
2021-09-16 23:35:28,950 [myid:] - INFO  [main:X509Util@77] - Setting -D jdk.tls.rejectClientInitiatedRenegotiation=true to disable client-initiated TLS renegotiation
2021-09-16 23:35:29,052 [myid:] - INFO  [main:ClientCnxnSocket@239] - jute.maxbuffer value is 1048575 Bytes
2021-09-16 23:35:29,110 [myid:] - INFO  [main:ClientCnxn@1726] - zookeeper.request.timeout value is 0. feature enabled=false
Welcome to ZooKeeper!
2021-09-16 23:35:29,483 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1171] - Opening socket connection to server localhost/0:0:0:0:0:0:0:1:2181.
2021-09-16 23:35:29,489 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1173] - SASL config status: Will not attempt to authenticate using SASL (unknown error)
2021-09-16 23:35:29,655 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1005] - Socket connection established, initiating session, client: /0:0:0:0:0:0:0:1:55046, server: localhost/0:0:0:0:0:0:0:1:2181
JLine support is enabled
2021-09-16 23:35:30,522 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1438] - Session establishment complete on server localhost/0:0:0:0:0:0:0:1:2181, session id = 0x10002eb88340000, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null
[zk: localhost:2181(CONNECTED) 0] ls /
[hello, zookeeper]
[zk: localhost:2181(CONNECTED) 1] 
~~~

**开启防火墙，以供外部访问**

~~~bash
firewall-cmd --zone=public --add-port=2181/tcp --permanent
firewall-cmd --zone=public --add-port=2182/tcp --permanent
firewall-cmd --zone=public --add-port=2183/tcp --permanent
systemctl restart firewalld
firewall-cmd --list-all
~~~

Mac下载zookeeper,地址:https://www.apache.org/dyn/closer.lua/zookeeper/zookeeper-3.7.0/apache-zookeeper-3.7.0-bin.tar.gz

解压后进入bin目录，执行`sh zkCli.sh -server 192.168.56.102:2181,192.168.56.102:2182,192.168.56.102:2183`

~~~bash
# 连接server
bin sh zkCli.sh -server 192.168.56.102:2181,192.168.56.102:2182,192.168.56.102:2183

Connecting to 192.168.56.102:2181,192.168.56.102:2182,192.168.56.102:2183
2021-09-17 23:26:53,552 [myid:] - INFO  [main:Environment@98] - Client environment:zookeeper.version=3.7.0-e3704b390a6697bfdf4b0bef79e3da7a4f6bac4b, built on 2021-03-17 09:46 UTC
2021-09-17 23:26:53,558 [myid:] - INFO  [main:Environment@98] - Client environment:host.name=192.168.1.9
2021-09-17 23:26:53,558 [myid:] - INFO  [main:Environment@98] - Client environment:java.version=1.8.0_202
2021-09-17 23:26:53,561 [myid:] - INFO  [main:Environment@98] - Client environment:java.vendor=Oracle Corporation
2021-09-17 23:26:53,561 [myid:] - INFO  [main:Environment@98] - Client environment:java.home=/Library/Java/JavaVirtualMachines/jdk1.8.0_202.jdk/Contents/Home/jre
2021-09-17 23:26:53,561 [myid:] - INFO  [main:Environment@98] - Client environment:java.class.path=/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/classes:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../build/classes:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/lib/*.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../build/lib/*.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-prometheus-metrics-3.7.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-jute-3.7.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-3.7.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/snappy-java-1.1.7.7.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-log4j12-1.7.30.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-api-1.7.30.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_servlet-0.9.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_hotspot-0.9.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_common-0.9.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient-0.9.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-unix-common-4.1.59.Final.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-epoll-4.1.59.Final.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-4.1.59.Final.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/netty-resolver-4.1.59.Final.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/netty-handler-4.1.59.Final.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/netty-common-4.1.59.Final.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/netty-codec-4.1.59.Final.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/netty-buffer-4.1.59.Final.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/metrics-core-4.1.12.1.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/log4j-1.2.17.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jline-2.14.6.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-ajax-9.4.38.v20210224.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-9.4.38.v20210224.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-servlet-9.4.38.v20210224.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-server-9.4.38.v20210224.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-security-9.4.38.v20210224.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-io-9.4.38.v20210224.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-http-9.4.38.v20210224.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/javax.servlet-api-3.1.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-databind-2.10.5.1.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-core-2.10.5.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-annotations-2.10.5.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/commons-cli-1.4.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../lib/audience-annotations-0.12.0.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../zookeeper-*.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/src/main/resources/lib/*.jar:/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin/../conf:
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:java.library.path=/Users/xiewei/Library/Java/Extensions:/Library/Java/Extensions:/Network/Library/Java/Extensions:/System/Library/Java/Extensions:/usr/lib/java:.
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:java.io.tmpdir=/var/folders/b4/9d7gh64s3937fcp3wwd9hvgm0000gn/T/
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:java.compiler=<NA>
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:os.name=Mac OS X
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:os.arch=x86_64
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:os.version=10.16
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:user.name=xiewei
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:user.home=/Users/xiewei
2021-09-17 23:26:53,567 [myid:] - INFO  [main:Environment@98] - Client environment:user.dir=/Users/xiewei/tools/apache-zookeeper-3.7.0-bin/bin
2021-09-17 23:26:53,568 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.free=236MB
2021-09-17 23:26:53,569 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.max=245MB
2021-09-17 23:26:53,569 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.total=245MB
2021-09-17 23:26:53,575 [myid:] - INFO  [main:ZooKeeper@637] - Initiating client connection, connectString=192.168.56.102:2181,192.168.56.102:2182,192.168.56.102:2183 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@768debd
2021-09-17 23:26:53,586 [myid:] - INFO  [main:X509Util@77] - Setting -D jdk.tls.rejectClientInitiatedRenegotiation=true to disable client-initiated TLS renegotiation
2021-09-17 23:26:53,600 [myid:] - INFO  [main:ClientCnxnSocket@239] - jute.maxbuffer value is 1048575 Bytes
2021-09-17 23:26:53,614 [myid:] - INFO  [main:ClientCnxn@1726] - zookeeper.request.timeout value is 0. feature enabled=false
Welcome to ZooKeeper!
JLine support is enabled
2021-09-17 23:26:53,639 [myid:192.168.56.102:2181] - INFO  [main-SendThread(192.168.56.102:2181):ClientCnxn$SendThread@1171] - Opening socket connection to server 192.168.56.102/192.168.56.102:2181.
2021-09-17 23:26:53,639 [myid:192.168.56.102:2181] - INFO  [main-SendThread(192.168.56.102:2181):ClientCnxn$SendThread@1173] - SASL config status: Will not attempt to authenticate using SASL (unknown error)
2021-09-17 23:26:53,676 [myid:192.168.56.102:2181] - INFO  [main-SendThread(192.168.56.102:2181):ClientCnxn$SendThread@1005] - Socket connection established, initiating session, client: /192.168.56.1:60556, server: 192.168.56.102/192.168.56.102:2181
2021-09-17 23:26:53,733 [myid:192.168.56.102:2181] - INFO  [main-SendThread(192.168.56.102:2181):ClientCnxn$SendThread@1438] - Session establishment complete on server 192.168.56.102/192.168.56.102:2181, session id = 0x10002eb88340001, negotiated timeout = 30000
[zk: 192.168.56.102:2181,192.168.56.102:2182,192.168.56.102:2183(CONNECTING) 0]
WATCHER::

WatchedEvent state:SyncConnected type:None path:null
ls /
[hello, zookeeper]
[zk: 192.168.56.102:2181,192.168.56.102:2182,192.168.56.102:2183(CONNECTED) 1]
~~~



集群安装方式二：通过docker-compose安装

先安装docker-compose:

~~~bash
[root@localhost admin]# curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   617    0   617    0     0    145      0 --:--:--  0:00:04 --:--:--   145
100 15.4M  100 15.4M    0     0   131k      0  0:02:00  0:02:00 --:--:--  136k


[root@localhost admin]# chmod +x /usr/local/bin/docker-compose
~~~

检查版本（验证是否安装成功):

~~~bash
[root@localhost admin]# docker-compose --version
docker-compose version 1.24.1, build 4667896b
~~~

卸载的话：

~~~bash
rm /usr/local/bin/docker-compose
~~~

开始配置，新建三个挂载目录：

~~~bash
[root@localhost zookeeper-cluster]# mkdir /usr/local/zookeeper-cluster/node4
[root@localhost zookeeper-cluster]# mkdir /usr/local/zookeeper-cluster/node5
[root@localhost zookeeper-cluster]# mkdir /usr/local/zookeeper-cluster/node6
~~~

新建任意目录，然后在里面新建一个文件：

~~~bash
[root@localhost local]# cd /usr/local
[root@localhost local]# mkdir DockerComposeFolder
[root@localhost local]# cd DockerComposeFolder

[root@localhost DockerComposeFolder]# vim docker-compose.yml
~~~

`docker-compose.yml`文件内容如下

~~~yml
version: '3.1'

services:
  zoo1:
    image: zookeeper
    restart: always
    privileged: true
    hostname: zoo1
    ports:
      - 2181:2181
    volumes: # 挂载数据
      - /usr/local/zookeeper-cluster/node4/data:/data
      - /usr/local/zookeeper-cluster/node4/datalog:/datalog
    environment:
      ZOO_MY_ID: 4
      ZOO_SERVERS: server.4=0.0.0.0:2888:3888;2181 server.5=zoo2:2888:3888;2181 server.6=zoo3:2888:3888;2181
    networks:
      default:
        ipv4_address: 172.18.0.14

  zoo2:
    image: zookeeper
    restart: always
    privileged: true
    hostname: zoo2
    ports:
      - 2182:2181
    volumes: # 挂载数据
      - /usr/local/zookeeper-cluster/node5/data:/data
      - /usr/local/zookeeper-cluster/node5/datalog:/datalog
    environment:
      ZOO_MY_ID: 5
      ZOO_SERVERS: server.4=zoo1:2888:3888;2181 server.5=0.0.0.0:2888:3888;2181 server.6=zoo3:2888:3888;2181
    networks:
      default:
        ipv4_address: 172.18.0.15

  zoo3:
    image: zookeeper
    restart: always
    privileged: true
    hostname: zoo3
    ports:
      - 2183:2181
    volumes: # 挂载数据
      - /usr/local/zookeeper-cluster/node6/data:/data
      - /usr/local/zookeeper-cluster/node6/datalog:/datalog
    environment:
      ZOO_MY_ID: 6
      ZOO_SERVERS: server.4=zoo1:2888:3888;2181 server.5=zoo2:2888:3888;2181 server.6=0.0.0.0:2888:3888;2181
    networks:
      default:
        ipv4_address: 172.18.0.16

networks: # 自定义网络
  default:
    external:
      name: zoonet
~~~

**注意yaml文件里不能有tab，只能有空格。**

关于version与Docker版本的关系如下：

![](https://github.com/lanbai1993/book/blob/master/zookeeper/images/docker-compose-file-format-compatibility.png?raw=true)

 然后执行（-d后台启动）`docker-compose -f docker-compose.yml up -d`

~~~bash
[root@localhost DockerComposeFolder]# docker-compose -f docker-compose.yml up -d
Creating dockercomposefolder_zoo2_1 ... done
Creating dockercomposefolder_zoo3_1 ... done
Creating dockercomposefolder_zoo1_1 ... done
~~~

查看已启动的容器

~~~bash
[root@localhost DockerComposeFolder]# docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                                  NAMES
c1e536397843        zookeeper           "/docker-entrypoin..."   21 minutes ago      Up 20 minutes       2888/tcp, 3888/tcp, 0.0.0.0:2181->2181/tcp, 8080/tcp   dockercomposefolder_zoo1_1
65ab984b726f        zookeeper           "/docker-entrypoin..."   21 minutes ago      Up 20 minutes       2888/tcp, 3888/tcp, 8080/tcp, 0.0.0.0:2182->2181/tcp   dockercomposefolder_zoo2_1
553a2e2bc10c        zookeeper           "/docker-entrypoin..."   21 minutes ago      Up 20 minutes       2888/tcp, 3888/tcp, 8080/tcp, 0.0.0.0:2183->2181/tcp   dockercomposefolder_zoo3_1
~~~

进入一个容器

~~~bash
[root@localhost DockerComposeFolder]# docker exec -it c1e536397843 bash
root@zoo1:/apache-zookeeper-3.7.0-bin# ./bin/zkCli.sh
Connecting to localhost:2181
2021-09-17 01:45:46,356 [myid:] - INFO  [main:Environment@98] - Client environment:zookeeper.version=3.7.0-e3704b390a6697bfdf4b0bef79e3da7a4f6bac4b, built on 2021-03-17 09:46 UTC
2021-09-17 01:45:46,360 [myid:] - INFO  [main:Environment@98] - Client environment:host.name=zoo1
2021-09-17 01:45:46,360 [myid:] - INFO  [main:Environment@98] - Client environment:java.version=11.0.12
2021-09-17 01:45:46,364 [myid:] - INFO  [main:Environment@98] - Client environment:java.vendor=Oracle Corporation
2021-09-17 01:45:46,364 [myid:] - INFO  [main:Environment@98] - Client environment:java.home=/usr/local/openjdk-11
2021-09-17 01:45:46,365 [myid:] - INFO  [main:Environment@98] - Client environment:java.class.path=/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/classes:/apache-zookeeper-3.7.0-bin/bin/../build/classes:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/lib/*.jar:/apache-zookeeper-3.7.0-bin/bin/../build/lib/*.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-prometheus-metrics-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-jute-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/snappy-java-1.1.7.7.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-log4j12-1.7.30.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-api-1.7.30.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_servlet-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_hotspot-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_common-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-unix-common-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-epoll-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-resolver-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-handler-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-common-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-codec-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-buffer-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/metrics-core-4.1.12.1.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/log4j-1.2.17.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jline-2.14.6.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-ajax-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-servlet-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-server-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-security-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-io-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-http-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/javax.servlet-api-3.1.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-databind-2.10.5.1.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-core-2.10.5.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-annotations-2.10.5.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/commons-cli-1.4.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/audience-annotations-0.12.0.jar:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-*.jar:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/src/main/resources/lib/*.jar:/conf:
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:java.library.path=/usr/java/packages/lib:/usr/lib64:/lib64:/lib:/usr/lib
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:java.io.tmpdir=/tmp
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:java.compiler=<NA>
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:os.name=Linux
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:os.arch=amd64
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:os.version=3.10.0-1062.el7.x86_64
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:user.name=root
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:user.home=/root
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:user.dir=/apache-zookeeper-3.7.0-bin
2021-09-17 01:45:46,462 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.free=10MB
2021-09-17 01:45:46,465 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.max=247MB
2021-09-17 01:45:46,465 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.total=15MB
2021-09-17 01:45:46,470 [myid:] - INFO  [main:ZooKeeper@637] - Initiating client connection, connectString=localhost:2181 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@4c70fda8
2021-09-17 01:45:46,633 [myid:] - INFO  [main:X509Util@77] - Setting -D jdk.tls.rejectClientInitiatedRenegotiation=true to disable client-initiated TLS renegotiation
2021-09-17 01:45:46,737 [myid:] - INFO  [main:ClientCnxnSocket@239] - jute.maxbuffer value is 1048575 Bytes
2021-09-17 01:45:46,797 [myid:] - INFO  [main:ClientCnxn@1726] - zookeeper.request.timeout value is 0. feature enabled=false
Welcome to ZooKeeper!
JLine support is enabled
2021-09-17 01:45:47,171 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1171] - Opening socket connection to server localhost/0:0:0:0:0:0:0:1:2181.
2021-09-17 01:45:47,232 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1173] - SASL config status: Will not attempt to authenticate using SASL (unknown error)
2021-09-17 01:45:47,490 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1005] - Socket connection established, initiating session, client: /0:0:0:0:0:0:0:1:55114, server: localhost/0:0:0:0:0:0:0:1:2181
2021-09-17 01:45:47,773 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1438] - Session establishment complete on server localhost/0:0:0:0:0:0:0:1:2181, session id = 0x4000359a82b0000, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null
[zk: localhost:2181(CONNECTED) 0] ls /
[zookeeper]
[zk: localhost:2181(CONNECTED) 1] create /hi
Created /hi
[zk: localhost:2181(CONNECTED) 2] ls /
[hi, zookeeper]
~~~

进入另一个容器

~~~bash
[root@localhost DockerComposeFolder]# docker exec -it 65ab984b726f bash
root@zoo2:/apache-zookeeper-3.7.0-bin# ./bin/zkCli.sh
Connecting to localhost:2181
2021-09-17 01:48:04,861 [myid:] - INFO  [main:Environment@98] - Client environment:zookeeper.version=3.7.0-e3704b390a6697bfdf4b0bef79e3da7a4f6bac4b, built on 2021-03-17 09:46 UTC
2021-09-17 01:48:04,869 [myid:] - INFO  [main:Environment@98] - Client environment:host.name=zoo2
2021-09-17 01:48:04,870 [myid:] - INFO  [main:Environment@98] - Client environment:java.version=11.0.12
2021-09-17 01:48:04,919 [myid:] - INFO  [main:Environment@98] - Client environment:java.vendor=Oracle Corporation
2021-09-17 01:48:04,919 [myid:] - INFO  [main:Environment@98] - Client environment:java.home=/usr/local/openjdk-11
2021-09-17 01:48:04,919 [myid:] - INFO  [main:Environment@98] - Client environment:java.class.path=/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/classes:/apache-zookeeper-3.7.0-bin/bin/../build/classes:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/target/lib/*.jar:/apache-zookeeper-3.7.0-bin/bin/../build/lib/*.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-prometheus-metrics-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-jute-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/zookeeper-3.7.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/snappy-java-1.1.7.7.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-log4j12-1.7.30.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/slf4j-api-1.7.30.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_servlet-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_hotspot-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient_common-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/simpleclient-0.9.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-unix-common-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-native-epoll-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-transport-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-resolver-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-handler-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-common-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-codec-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/netty-buffer-4.1.59.Final.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/metrics-core-4.1.12.1.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/log4j-1.2.17.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jline-2.14.6.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-ajax-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-util-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-servlet-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-server-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-security-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-io-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jetty-http-9.4.38.v20210224.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/javax.servlet-api-3.1.0.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-databind-2.10.5.1.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-core-2.10.5.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/jackson-annotations-2.10.5.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/commons-cli-1.4.jar:/apache-zookeeper-3.7.0-bin/bin/../lib/audience-annotations-0.12.0.jar:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-*.jar:/apache-zookeeper-3.7.0-bin/bin/../zookeeper-server/src/main/resources/lib/*.jar:/conf:
2021-09-17 01:48:04,919 [myid:] - INFO  [main:Environment@98] - Client environment:java.library.path=/usr/java/packages/lib:/usr/lib64:/lib64:/lib:/usr/lib
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:java.io.tmpdir=/tmp
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:java.compiler=<NA>
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:os.name=Linux
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:os.arch=amd64
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:os.version=3.10.0-1062.el7.x86_64
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:user.name=root
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:user.home=/root
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:user.dir=/apache-zookeeper-3.7.0-bin
2021-09-17 01:48:04,920 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.free=10MB
2021-09-17 01:48:04,924 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.max=247MB
2021-09-17 01:48:04,924 [myid:] - INFO  [main:Environment@98] - Client environment:os.memory.total=15MB
2021-09-17 01:48:04,970 [myid:] - INFO  [main:ZooKeeper@637] - Initiating client connection, connectString=localhost:2181 sessionTimeout=30000 watcher=org.apache.zookeeper.ZooKeeperMain$MyWatcher@4c70fda8
2021-09-17 01:48:05,022 [myid:] - INFO  [main:X509Util@77] - Setting -D jdk.tls.rejectClientInitiatedRenegotiation=true to disable client-initiated TLS renegotiation
2021-09-17 01:48:05,027 [myid:] - INFO  [main:ClientCnxnSocket@239] - jute.maxbuffer value is 1048575 Bytes
2021-09-17 01:48:05,087 [myid:] - INFO  [main:ClientCnxn@1726] - zookeeper.request.timeout value is 0. feature enabled=false
Welcome to ZooKeeper!
2021-09-17 01:48:05,464 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1171] - Opening socket connection to server localhost/127.0.0.1:2181.
2021-09-17 01:48:05,465 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1173] - SASL config status: Will not attempt to authenticate using SASL (unknown error)
2021-09-17 01:48:05,622 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1005] - Socket connection established, initiating session, client: /127.0.0.1:53278, server: localhost/127.0.0.1:2181
JLine support is enabled
2021-09-17 01:48:06,168 [myid:localhost:2181] - INFO  [main-SendThread(localhost:2181):ClientCnxn$SendThread@1438] - Session establishment complete on server localhost/127.0.0.1:2181, session id = 0x5000359a80d0000, negotiated timeout = 30000

WATCHER::

WatchedEvent state:SyncConnected type:None path:null
[zk: localhost:2181(CONNECTED) 0] ls /
[hi, zookeeper]
~~~

本地客户端连接集群：

~~~bash
zkCli.cmd -server 192.168.192.128:2181,192.168.192.128:2182,192.168.192.128:2183
~~~

查看节点信息：

~~~bash
ls /
[hi, zookeeper]
[zk: 192.168.56.102:2181,192.168.56.102:2182,192.168.56.102:2183(CONNECTED) 1]
~~~

停止所有活动容器`docker-compose stop`

~~~bash
[root@localhost DockerComposeFolder]# docker-compose stop
Stopping dockercomposefolder_zoo1_1 ... done
Stopping dockercomposefolder_zoo2_1 ... done
Stopping dockercomposefolder_zoo3_1 ... done
~~~

删除所有已停止的容器

~~~bash
[root@localhost DockerComposeFolder]# docker-compose rm
Going to remove dockercomposefolder_zoo1_1, dockercomposefolder_zoo2_1, dockercomposefolder_zoo3_1
Are you sure? [yN] y
Removing dockercomposefolder_zoo1_1 ... done
Removing dockercomposefolder_zoo2_1 ... done
Removing dockercomposefolder_zoo3_1 ... done
~~~

更多docker-compose命令：`docker-compose --help`

~~~bash
[root@localhost DockerComposeFolder]# docker-compose --help
Define and run multi-container applications with Docker.

Usage:
  docker-compose [-f <arg>...] [options] [COMMAND] [ARGS...]
  docker-compose -h|--help

Options:
  -f, --file FILE             Specify an alternate compose file
                              (default: docker-compose.yml)
  -p, --project-name NAME     Specify an alternate project name
                              (default: directory name)
  --verbose                   Show more output
  --log-level LEVEL           Set log level (DEBUG, INFO, WARNING, ERROR, CRITICAL)
  --no-ansi                   Do not print ANSI control characters
  -v, --version               Print version and exit
  -H, --host HOST             Daemon socket to connect to

  --tls                       Use TLS; implied by --tlsverify
  --tlscacert CA_PATH         Trust certs signed only by this CA
  --tlscert CLIENT_CERT_PATH  Path to TLS certificate file
  --tlskey TLS_KEY_PATH       Path to TLS key file
  --tlsverify                 Use TLS and verify the remote
  --skip-hostname-check       Don't check the daemon's hostname against the
                              name specified in the client certificate
  --project-directory PATH    Specify an alternate working directory
                              (default: the path of the Compose file)
  --compatibility             If set, Compose will attempt to convert keys
                              in v3 files to their non-Swarm equivalent

Commands:
  build              Build or rebuild services
  bundle             Generate a Docker bundle from the Compose file
  config             Validate and view the Compose file
  create             Create services
  down               Stop and remove containers, networks, images, and volumes
  events             Receive real time events from containers
  exec               Execute a command in a running container
  help               Get help on a command
  images             List images
  kill               Kill containers
  logs               View output from containers
  pause              Pause services
  port               Print the public port for a port binding
  ps                 List containers
  pull               Pull service images
  push               Push service images
  restart            Restart services
  rm                 Remove stopped containers
  run                Run a one-off command
  scale              Set number of containers for a service
  start              Start services
  stop               Stop services
  top                Display the running processes
  unpause            Unpause services
  up                 Create and start containers
  version            Show the Docker-Compose version information
~~~



Reference:

> https://www.cnblogs.com/LUA123/p/11428113.html
>
> https://www.runoob.com/w3cnote/zookeeper-linux-cluster.html


---