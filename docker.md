Docker
======

* [Docker 首頁](https://www.docker.com/)
* [Command Line 語法](https://docs.docker.com/reference/commandline/cli/)
* [如何把資料傳到 docker container](https://docs.docker.com/userguide/dockervolumes/)
* [Docker —— 從入門到實踐](http://philipzheng.gitbooks.io/docker_practice/)

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
