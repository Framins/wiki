Docker
======

* [Docker 首頁](https://www.docker.com/)
* [Command Line 語法](https://docs.docker.com/reference/commandline/cli/)
* [如何把資料傳到 docker container](https://docs.docker.com/userguide/dockervolumes/)
* [Docker —— 從入門到實踐](http://philipzheng.gitbooks.io/docker_practice/)
* [Command](command.md)

Docker Orchestration Tools
--------------------------

* [Machine](https://docs.docker.com/machine/) - 從零到有幫你佈署 Docker 環境
* [Swarm](https://docs.docker.com/swarm/) - 用 Docker 建立 cluster 應用
* Compose - 定義並執行複雜的 Docker 應用

Why Docker
----------

* 啟動速度快
* 系統資源使用率高
* 可以同時執行更多 AP

Terms
-----

* *Image* 映像檔 - 可以稱之為一個 read-only template ，如 ubuntu + apache ，映像檔可以建立容器。
* *Container* 容器 - 執行應用，它可以被啟動、開始、停止、刪除，每個容器都是互相隔離的。
* *Repository* 倉庫 - 集中存放映像檔的地方，公開的如 [Docker Hub](https://hub.docker.com/)

> 映像檔是唯讀的，容器是在映像檔上多加一層可寫層

FAQ
---

### 時區問題

建 image 時執行這個指令：

```dockerfile
RUN echo "Asia/Taipei" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
```

或是 container 直接執行也可以：

```bash
docker exec -ti containerID echo "Asia/Taipei" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
```

### 對所有容器做一樣的操作

參考： http://knktc.com/2014/08/09/docker-cheat-sheet/

停止所有容器：

```bash
docker stop $(docker ps -a -q) 
```

刪除所有容器

```bash
docker rm $(docker ps -a -q)
```
