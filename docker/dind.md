Docker in Docker
================

在 Docker Container 裡面 run Docker

使用時機：

* 想用 Docker 又不想把 host 搞髒

Try it
------

使用官方 [Docker Image](https://hub.docker.com/_/docker/)

Docker 的設計是 Client/Server 架構，所以它拆成兩種 image (使用 tag 區分 ，以下用兩個 image 連接做範例

### Start Server

因為是 Client/Server 架構，所以 deamon 必須先啟動：

    docker run -d --name some-docker --privileged docker:dind

> `--privileged` 是必要參數，但它有風險，詳細參考[官方網站說明](https://docs.docker.com/engine/reference/run/#/runtime-privilege-and-linux-capabilities)

### Start Client

接著 Client 去連接即可使用：

    docker run --rm -it --link some-docker:docker docker ps

> 連接的時候，需要使用 `docker` 別名
