# Rancher Service

*Service* 是一個或一群 container，可以提供特定服務或是執行特定任務

多個 service 連接起來，可以組合成 [Stack](stack.md) 完成一個更完整或更多樣的服務

## Add Service

在 Rancher 裡，service 需要指定在特定的 stack 下，先點選 `Add Service`，接著會出現建立 service 的基本設定，下面還有進階設定可以打開。

常玩 [Docker][] 和 [Docker Compose][] 的話，對這頁的設定一定不陌生。但 Rancher 是在多台 host 下執行，跟平常 Docker / Docker Compose 單機執行情況有點不一樣，以下提出幾點特別的地方：

* **Scale:** 跟 Docker Compose 一樣，不過它有另一個選項是在「每個 host 都 run 一個 container」
* **Sidekick:** 是 Rancher 獨有的，它會用在當 scale 的時候想兩個 container 一起 scale 的情境下
* **Volume From:** 需要兩個 service 都指定同一個特定 host 才能使用
* **Health Check:** 可以固定執行連線，確認 service 還活著。**Docker 1.12 也開始支援 Health Check 了**
* **Security/Host:** 可以限制 container 存取主機資源
* **Lable:** 可為 service 標記，可供 Scheduling 用
* **Scheduling:** 可以定義 container 安排的規則

## Usage

大部分的需求，只要定義好 service name 和 link 就能用得很開心了。比方說 [Wordpress](https://hub.docker.com/_/wordpress/) 可以參考文件的 `docker-compose.yml`，建立 mysql container 並設好 root 密碼，然後再建 wordpress container 去連結它就可以開始用了

目前個人遇到比較特別的是 nginx + php-fpm，因為需要設定 *Volume From*，就必須指定 container 要在哪台主機

另外如果是自己寫的程式，比方說 nodejs 程式要上 Rancher 的話，可以選擇 build 好再上；或是用 *Volume From* 一個可以 ssh 的 container，然後去更新 code 即可

[Docker]: https://www.docker.com/
[Docker Compose]: https://docs.docker.com/compose/
