# Rancher Stack

在 Rancher 裡，*Stack* 是一整套應用程式，由一組 *Service* 組合而成

而 Service 啟動的條件是，至少要有一個 *Container* 啟動

這些是使用 Rancher 的基本概念

## How to start

其實要開始並不難，如果有用過 [Docker Compose][] 的人會知道，這兩個是完全一樣的東西：

* Stack 等同於 Project name
* Service 定義是一樣的，一樣也具備 link 其他 service 的定義
* Container 定義也是一樣的，且一樣具有 scaling 的空間

## How to clone

新增一個空的 Stack 並沒有什麼問題，加入 Service 的過程才會比較困難。但完成了一個 Stack 後，就可以開始從這個 Stack 複製出更多個來。比方說上面有提到 Logger stack，所以我可以從現有的 Logger 再複製第二個出來。

首先其實 Stack 是可以跟 Docker Compose 互轉的，先從 Stack 轉成 Docker Compose，按選單鈕選 **View Config** ：

再來就會看到兩邊長長的 yaml，左邊是 Docker Compose 用，右邊是 Rancher Compose 要用的。

以下是 `docker-compose.yml` 範例

```yml
sentry:
  restart: always
  environment:
    DATABASE_URL: postgres://postgres:@postgres/postgres
    SECRET_KEY: random_value
    SENTRY_ADMIN_PASSWORD: password
    SENTRY_ADMIN_USERNAME: admin
    SENTRY_REDIS_HOST: redis
    SENTRY_URL_PREFIX: http://sentry.stage.com
  tty: true
  image: slafs/sentry
  links:
    - postgres:postgres
    - redis:redis
  stdin_open: true
redis:
  restart: always
  tty: true
  image: redis:2.8
  stdin_open: true
postgres:
  restart: always
  tty: true
  image: postgres:9.4
  stdin_open: true
```

再來點選新增 stack 貼到左邊 `docker-compose.yml` 區塊即可

Stack 對外的 port 要設定在 sentry service 上，它的設定是 `EXPOSE 9000`。可以加在 `docker-compose` 上，或是使用 *Load Balancer* 轉給它都可以。

最後就可以到選單中啟動 Stack 了！

## Notice

* Code 要上線到 Rancher 的 Stack 上，建議使用 build image &amp; pull image 的方式上線
* 因 Docker Container 基本性質是隔離的，所以在 Stack 裡的 container 建議不要直接對外

[Docker Compose]: /docker/compose.md
