# Docker

## Why Docker

* 啟動速度快
* 系統資源使用率高
* 可以同時執行更多 AP

## Docker Tools

* **[Docker Machine](machine.md):** 從零到有幫你佈署 Docker 環境
* **[Docker Swarm](swarm.md):** 用 Docker 建立 cluster 應用
* **[Docker Compose](compose.md):** 定義並執行複雜的 Docker 應用

## Terms

* **Image:** 映像檔，可以稱之為一個 read-only template ，如 ubuntu + apache ，映像檔可以建立容器
* **Container:** 容器，執行應用，它可以被啟動、開始、停止、刪除，每個容器都是互相隔離的
* **Repository:** 倉庫，集中存放映像檔的地方，公開的如 [Docker Hub][]

Note: 映像檔是唯讀的，容器是在映像檔上多加一層可寫層

## Usage

* [Command](command.md)
* [Dockerfile](dockerfile.md)
* [Tricks](tricks.md)
* [Docker in Docker](dind.md)
* [Windows solutions](windows.md)

## FAQ

### 時區問題

建 image 時執行這個指令：

```dockerfile
RUN echo "Asia/Taipei" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
```

或是 container 直接執行也可以：

```bash
docker exec -ti containerID echo "Asia/Taipei" > /etc/timezone && dpkg-reconfigure -f noninteractive tzdata
```

### Docker 「進容器」的方法

開啟的時候直接打開 bash shell

```bash
docker run -it --name=some-php php:7.0-apache bash
```

一般離開是直接打 `exit` ，但同時會把容器關閉，如果不想關掉的話，可以按 `Ctrl + P + Q` 回到 host 上

Warning: 這快速鍵好像是 bash 獨有的，不是很確定

要再回去執行 bash 的容器裡的指令

```bash
docker attach some-php
```

### Docker 為容器命名的規則

https://github.com/docker/docker/blob/master/pkg/namesgenerator/names-generator.go

基本上就是形容詞對人名，但最後面有個很有趣的限外規則

## References

* [Docker](https://www.docker.com/)
* [Docker —— 從入門到實踐](http://philipzheng.gitbooks.io/docker_practice/)
* [Cheat Sheet](http://zeroturnaround.com/wp-content/uploads/2016/03/Docker-cheat-sheet-by-RebelLabs.png)
* [Docker 導入：障礙與對策](http://www.slideshare.net/williamyeh/docker-66222654)

[Docker Hub]: https://hub.docker.com/
