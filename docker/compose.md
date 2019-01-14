# Docker Compose

如果想建立一個複雜的 Docker 環境的話，別懷疑，用 [Docker Compose][] 就對了！

它使用 YAML 格式定義環境所需要的 Container ，只需一行指令就可以啟動並執行相關初始化或聯結

因為是從 [fig][] 過來的，所以也可以參考 fig 指令

## Installation

[GitHub](https://github.com/docker/compose/releases) 上隨時會有更新，可以參考上面的說明安裝

## Command

所有指令以 `docker-compose` 開頭，後面接想做的操作

### docker-compose up

建立 container 並執行，預設讀取 `docker-compose.yml` 檔，並執行裡面所描述的建置。

加上 `-d` 參數後， container 會在背景執行

    # docker-compose up -d
    Creating dockerfile_web_1...
    Creating dockerfile_redis_1...
    Creating dockerfile_mysql_1...

有趣的是，如果已經 create 過的話，再下 up 指令，它會有重新建立的訊息，但實際上會有點像重開機

    # docker-compose up -d
    Recreating dockerfile_web_1...
    Recreating dockerfile_redis_1...
    Recreating dockerfile_mysql_1...

up 時，會查看當下有無此 image，有會直接使用此 image，沒有則 build image 

### docker-compose start/stop/restart

啟動或停止 container

    # docker-compose start
    Starting dockerfile_web_1...
    Starting dockerfile_redis_1...
    Starting dockerfile_mysql_1...

    # docker-compose stop
    Stopping dockerfile_mysql_1...
    Stopping dockerfile_redis_1...
    Stopping dockerfile_web_1...

    # docker-compose restart
    Restarting dockerfile_web_1...
    Restarting dockerfile_redis_1...
    Restarting dockerfile_mysql_1...

### docker-compose rm

刪除 container ，這指令只會刪除已停止的 container

    # docker-compose rm
    Going to remove dockerfile_mysql_1, dockerfile_redis_1, dockerfile_web_1
    Are you sure? [yN] y
    Removing dockerfile_web_1...
    Removing dockerfile_redis_1...
    Removing dockerfile_mysql_1...

### docker-compose scale

調整執行實體數量，如果有綁定 port 的 service 不能調整

    # docker-compose scale mysql=3
    Creating dockerfile_mysql_2...
    Creating dockerfile_mysql_3...
    Starting dockerfile_mysql_2...
    Starting dockerfile_mysql_3...

### docker-compose ps

觀看目前 container 的運行狀況

    # docker-compose ps
           Name                    Command             State                     Ports                   
    ----------------------------------------------------------------------------------------------------
    dockerfile_mysql_1   /entrypoint.sh redis-server   Up      3306/tcp, 6379/tcp                        
    dockerfile_redis_1   /entrypoint.sh redis-server   Up      6379/tcp                                  
    dockerfile_web_1     apache2 -DFOREGROUND          Up      0.0.0.0:10022->22/tcp, 0.0.0.0:80->80/tcp

## YAML Define

以下為一個範例

```yaml
# Service 名稱
web:
  # 用 Dockerfile 建置 service ，後面接的是目錄路徑
  build: .
  # 定義對外開放的 port，等同 docker run -p 的參數
  ports:    
    - "8080:80"
    - "422:22"
  # 掛載host目錄到容器裡
  volumes:
    - .:/app
  # 與其他 container 做連結
  links:
    - "mysql:mysql"
  # 定義環境變數
  environment:
    PDO_DRIVER: mysql
    PDO_HOST: mysql
    PDO_USER: root
    PDO_PASSWORD: root
    PDO_PORT: "3306"
    PDO_DBNAME: datastore

# 另一個 service
mysql:
  # 使用 Docker 的映像檔
  image: mysql
  # 使用 expose 讓其他 container 可以連結到此 service ，而 host 無法連結
  expose:
    - "3306"
  environment:
    MYSQL_ROOT_PASSWORD: root
    MYSQL_DATABASE: datastore
```

[fig]: http://www.fig.sh/
[Docker Compose]: https://docs.docker.com/compose/
