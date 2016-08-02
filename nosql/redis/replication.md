Replication
===========

*Replication* 在 Server 領域的解釋比較接近「自我複製」

簡單來說，是把自己的資料複製一份出來給其他人

## Context

最近工作有個需求：有台 service 會定期寫資料進一台 Redis ，僅僅一台 Redis

如果其他 client 單純是讀取的話，是沒問題的。問題在於其他 client 也需要寫入，而寫入資料又會因為各 client 環境不同而有所不同，接著就會發生「 A 寫入資料， B 沒做什麼事卻突然壞掉」的怪事，可是有資料的 Redis 又只有一台，無法每個人都分一台

## Analytics

一個可以參考的方向是： Redis 存放的是原始資料。資料來源是 service ，應該要以它所提供的服務目的為主，所以其實這台 Redis 可能不適合讓其他 client 存取 。

如果 client 可以寫入，代表 service 跟 client 的目的是一樣的；目的一樣，代表可以寫在同一個 service/client 裡的；無法寫在同一包的話，很有可能是因為目的不一樣， 那 client 就不應該有直接存取原始資料的方法。

這個結果非常鬼打牆，不過這也表示 service / redis / client 之間分層非常不明確，因此也就容易發生「改 A 壞 B 」的狀況

> 可以參考 單一職責原則 和 最小知識原則(迪米特原則)

## Solution

以下解決方案會以「不讓其他 Client 寫入 Redis」為主

### Service API

在這個框架裡， service 具備了寫入功能，其實也可以提供讀取 API 讓 Client 使用。這樣做的目的只有一個：使用 API 包裝原始資料，也就是物件導向提到的**封裝**

調整完後，架構應該會是：

    Client <-> Service <-> Redis

Client 需透過 service 取得資料，無法直接存取 Redis ，而 client 如果有別的儲存需求，可以另開 Redis 解決

這是個人認為最麻煩、同時也是最佳解：**自己的 Redis 自己管**

### Redis Replication

開發時間很有限，產品沒辦法立即完成的話，除非是逼不得已，不然上述方案是架構要大改，通常都不會接受。

因此另一個折中的方法就是本篇主題， *Redis Replication*

Replication 可以把原始的 Redis 資料複製出來，轉存到其他台 Radis 。原始 Redis 會被稱之為 *Master* ，轉存的 Redis 則稱為 *Slave* 。第一次會做完全複製，之後 Master 只要一有更新， Slave 就會更新。

接著把 service 資料存到 Master 上，然後每個 client 配一個 Slave 。 client 可以取得資料，也可以寫入資料。雖然有點奇怪，但也是一個可行方案。

這個架構要注意的是：如果 service 和 client 要靠 Redis 溝通的話，是無法達成的。

> BTW ， 如果要溝通的話，用 API 會更直接簡單...

以下說明簡單的做法，詳細實作方法可以參考[官網](http://redis.io/topics/replication)

#### Use runtime configuration

首先， Master 是不需要調整設定的，只要 Slave 設定好即可

使用 `redis-cli` 進入 Redis 然後下指令：

```bash
# 設定 slave
redis 127.0.0.1:6379> slaveof <master-redis-host> <port>
# 如果 master 要驗證的話
redis 127.0.0.1:6379> masterauth <password>
# 預設 slave 會是唯讀的，如果要開啟寫入的話
redis 127.0.0.1:6379> slave-read-only no
```

這個方法只要重開機後， Slave 的監聽功能就會失效。如果是固定設定的話，可以考慮寫設定檔

#### Use configuration file

如果知道 `CONFIG SET` 和 `redis.conf` 之間的關係的話，就會知道 `redis.conf` 設定會長這樣：

```conf
# 設定 slave
slaveof <master-redis-host> <port>
# 如果 master 要驗證的話
masterauth <password>
# 預設 slave 會是唯讀的，如果要開啟寫入的話
slave-read-only no
```

#### Use parameter

*Parameter* 是啟動 Redis 指令的後面的參數，如果知道 parameter 和 `redis.conf` 之間的關係的話，就會知道啟動指令要這樣下：

```bash
redis-server \
  --slaveof <master-redis-host> <port> \
  --masterauth <password> \
  --slave-read-only no
```

## Conclusion

首先要注意一點：其實 Replication 是用來解決分流問題的，並不是用來解決 Context 的的問題。只是這個 Context 剛好想到這個解法，所以就順便記錄起來了。

會研究這麼多設定方法，最主要是因為 Rancher 在使用設定檔，或 runtime 調整都是很麻煩的事；使用 parameter 配合 Docker 的 CMD ，相對就很適合在 Rancher 上執行，並能很快速的建立起一群 Slave 和 Load Balancer

## Reference

* [Single responsibility principle](https://en.wikipedia.org/wiki/Single_responsibility_principle)
* [最小知識原則(迪米特原則)](http://ithelp.ithome.com.tw/question/10101265)
* [Replication - Redis](http://redis.io/topics/replication)
