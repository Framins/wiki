# Docker Swarm

[Docker Swarm][] 是 Docker 官方出的容器調度系統

## Setup

### [Docker Machine](machine.md) + [VirtualBox][]

先建機器

    docker-machine create -d virtualbox node1
    docker-machine create -d virtualbox node2
    docker-machine create -d virtualbox node3

接著選定一台當做 Manager ，比方說是 `node1` 。接著切換到 node1 上初始化 Swarm

```
$ eval $(docker-machine env node1)
$ docker swarm init --advertise-addr 192.168.99.100  # 因為 VirtualBox 預設會起兩個網路介面
Swarm initialized: current node (8o4fxwxu8e4zqhxn4vco7rguj) is now a manager.

To add a worker to this swarm, run the following command:

    docker swarm join \
    --token SWMTKN-1-3dmqscpgn6jwxk5o7zlmum5i2655um6bv1lgmtcztp48h4fh4n-bgmembhgaok4lhjzo2adxwsho \
    192.168.99.100:2377

To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
```

上面會提示 Worker 要下的指令，接著切換到 `node2` `node3` 下指令

```
$ eval $(docker-machine env node2)
$ docker swarm join --token SWMTKN-1-3dmqscpgn6jwxk5o7zlmum5i2655um6bv1lgmtcztp48h4fh4n-bgmembhgaok4lhjzo2adxwsho 192.168.99.100:2377
This node joined a swarm as a worker.
$ eval $(docker-machine env node3)
$ docker swarm join --token SWMTKN-1-3dmqscpgn6jwxk5o7zlmum5i2655um6bv1lgmtcztp48h4fh4n-bgmembhgaok4lhjzo2adxwsho 192.168.99.100:2377
This node joined a swarm as a worker.
```

到此， Swarm 的環境已算初始化完成了，接著到 Manager 開始啟動 Service

```
$ docker service create --name web -p 8000:80 nginx:alpine
4r0x9rts2adklf3tt9816av50
```

Scaling

```
$ docker service scale web=30
web scaled to 30
```

Update

```
$ docker service update --image nginx:latest web
web
```

在操作上很像是在單機操作，但這些操作都會同步到所有 worker 。

## References

* [Install and Create a Docker Swarm](https://docs.docker.com/swarm/install-w-machine/)
* [Docker Swarm 控制多網路區域的 Docker](http://www.ithome.com.tw/guest-post/99967)

[Docker Swarm]: https://docs.docker.com/swarm/
[VirtualBox]: https://www.virtualbox.org
