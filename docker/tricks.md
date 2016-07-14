Tricks
======

停止所有容器：

```bash
docker stop $(docker ps -a -q) 
```

刪除所有容器

```bash
docker rm $(docker ps -a -q)
```

Official docker installation script :

```bash
curl -fsSL https://get.docker.com/ | sh
```

Remove all stopped containers :

```bash
docker rm $(docker ps -a -q)
```

> You can add -f param to force delete all containers

Remove all images

```bash
docker rmi $(docker images -q)
```

> You can add -f param to force delete all images, too

Remove all images without tag

```bash
docker rmi $(docker images | grep "^<none>" | awk "{print $3}")
```

Remove all volumes

```bash
docker volume rm $(docker volume ls -qf dangling=true)
```

Show latest started container

```bash
docker ps -l
docker ps -n X
```

> `-l` display only one container  
> `-n` display X latest containers

Show container logs

```bash
docker logs -f <CONTAINER_ID|CONTAINER_NAME>
```

> `-f` param to follow the upcoming log messages. When you are done, hit CTRL+C  
> `-t` param display timestamp

Show container stats

```bash
docker stats [CONTAINER_ID|CONTAINER_NAME]
```

> Without options, stats display all running containers  
> `-a`, `--all` display all containers

Enter in a container

```bash
docker exec -it [CONTAINER_ID|CONTAINER_NAME] bash
```

Docker 直接對應 app 的指令懶人包

```bash
# Docker Alias
alias composer="docker run -i -t --rm -v \$PWD:/app composer/composer:1.1-alpine"
alias npm="docker run -i -t --rm -v \$PWD:/usr/src/app -w /usr/src/app node:6.3-slim npm"
alias go="docker run -i -t --rm -v \$PWD:/usr/src/app -w /usr/src/app golang:1.6-alpine go"
```

References
----------

* [10 Tips & Tricks with Docker](https://mercurenews.com/en/10-tips-tricks-with-docker/)
* [docker随手记](http://knktc.com/2014/08/09/docker-cheat-sheet/)
