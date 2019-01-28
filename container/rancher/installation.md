# Installation

有了 *Docker*，可以開始建立自己的貨櫃 (Images)

有了 *Docker Compose*，可以開始建立自己的戰艦 (Application/Stack)

而有了 *Rancher* 之後，就可以開始建造你的艦隊 (Cluster)

不同的 container os 有不同的調度工具，RancherOS 使用 [Rancher](http://rancher.com/rancher/) 做為它的調度工具，個人認為 Rancher 的特色如下：

* 它被打包成 Docker Image 來執行，意味著只要有 Docker 的執行環境，即可 run Rancher
* 它可以使用網頁介面去管理各個功能：如 *容器管理監控*、*Scaling*、*Load Balancer*、*DNS*、 *Health check* 等
* Host 間的 Networking 設定非常簡單。HostA 的容器 1 連線到 HostB 的容器 2，跟 Local 設定 A link B 幾乎是一樣，VPN 加密設定也是自動完成的。
* 承上，不管基礎設施怎麼變動，連結依然能正確的設定
* 讓 Rancher 自動佈署規劃容器的設定方法非常簡單，只要使用標籤和定義規則即可
* 使用 Volume 設定來備份資料也非常簡單

講這麼多，來看看 Rancher 如何安裝：

1. 安裝好 Docker，確定 Docker 環境能執行
2. 執行 `docker run -d --name rancher --restart=always -p 8080:8080 rancher/server` 這行指令，等它初始化約 1 分鐘左右
3. 打開 Browser，輸入網址 http://localhost:8080/ 即可看到 Rancher 的主頁

以上是官方提供的最簡易安裝法，還有很多環境設定可以調整可以參考[官方網站](http://docs.rancher.com/rancher/installing-rancher/installing-server/)。以下測試是先開三台機器 (VM)：

* Nginx proxy
* Single Node
* MySQL

會這樣做的原因是，官方是有提供 [Multi Node](http://docs.rancher.com/rancher/installing-rancher/installing-server/multi-nodes/) 做法，雖然不會用 HA，但還是有大略看了一下，發現 MySQL 的機器另外開，之後不夠用要轉 Multi Node 才不會很痛苦吧

接著就可以開始設定 Host
