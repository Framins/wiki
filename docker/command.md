# Command

* https://github.com/wsargent/docker-cheat-sheet
* [Docker 實用指令及 Best Practices Cheat Sheet 圖表](https://blog.wu-boy.com/2016/03/docker-commands-and-best-practices-cheat-sheet/)

## docker pull

取得映像檔

    docker pull ubuntu:12.04

## docker images

顯示本機已有的映像檔

    # docker images
    REPOSITORY          TAG                 IMAGE ID            CREATED             VIRTUAL SIZE
    ubuntu              14.04               5ba9dab47459        6 days ago          188.3 MB
    ubuntu              12.04               69c02692b0c1        6 days ago          131.3 MB
    mysql               latest              aca96d9e6b5c        7 days ago          282.7 MB

可用參數

* `-q` : quiet

裡面幾個 terms ：

* *REPOSITORY* 來自哪個倉庫
* *TAG* 標記，或稱之為版本
* *IMAGE ID* 唯一 ID，有點像 hash code
* *CREATED* 建立時間
* *VIRTUAL SIZE* 映像檔大小

## docker run

建立容器

    docker run \
      -p <host port>:<container port> \
      --name <container name> \
      --hostname <hostname> \
      -d <image name>

* `-d` Run container in background

建立容器 執行完即刪除

    docker run --rm -it <image name>

## docker exec

Run a command in a running container

    docker exec -it <container id/name> bash

## docker ps

List all containers

    docker ps -a

* `-a` : all
* `-q` : quiet

可以加上自定義的 template 比方說只想看到 port 被佔用的情況

    docker ps --format "{{.Names}}: {{.Ports}}"

Hint: template 的用法可以下 `man docker-ps` 參考線上說明文件

## docker stop

    docker stop <constianer Id/name>

## docker rm

Remove container

    docker rm -vf <container Id/name>

* `-v` : 刪除 volume
* `-f` : Force

Remove **ALL** container

    docker rm -vf $(docker ps -a -q)

## docker rmi

Remove image

    # rm all IMAGE
    docker rmi -f $(docker images -q)

## docker commit

提交對 images 做的修改

    docker commit -m "Added json gem" -a "Docker Newbee" 0b2616b0e5a8 ouruser/sinatra:v2

* `-m` 指定提交的說明訊息
* `-a` 指定更新使用者訊息
* `0b2616b0e5a8` 是映像檔容器的 ID
* `ouruser/sinatra:v2` 指定新映像檔的名稱和 tag

成功後會出現新映像檔的 ID

## docker build

使用 Dockerfile 建立新的映像檔

    docker build -t="ouruser/sinatra:v2" .
