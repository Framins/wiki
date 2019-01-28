# Rancher Host

*Host* 是一個網路可連接，且可以放 Docker Container 的空間

這空間可以是實體機器，也可以是 VM，只要網路可以連接的到就行了

> P.S.: 要能提供一個 IP 讓 Rancher 能連線，有試過躲在 NAT server 後面是不行的

最重要的是，這空間要能夠執行 Docker

## Add Host

剛安裝好，打開主頁會提醒你要新增 Host 和 Service，加 Host 會提醒你

> 加 Service 之前，至少要準備一個支援 Docker 1.6 版以上的 Linux server，而且要能透過 HTTP 連線到 Rancher Server。

點下 `Add Host` 會要求你註冊 host

Warning: Host 要能連線到這個 URL，接下來才能正常地被偵測到

接著可以看到 Rancher 列出了它支援的雲端主機商

先前提過，有 Docker 就能用，所以其實也可以用自己架的 host 來用，選 `Custom`

這裡有很清楚的 step by step

1. 準備一台裝好 Docker 的 Linux 主機
2. 確定防火牆有打開 500 /4500 UDP，這是 IPsec networking
3. 為主機加 Label，這可以用來做自動規劃用，不過事後也可以加，可以先跳過
4. 這裡有一串指令，只要把這串指令 copy 到步驟一的主機上執行即可
5. 差不多要等2分鐘 (下載 agent + 啟動 agent + 連線)

網路連線如果都正常的話，到 `Infrastructure` 就可以看到你的 host 了

有了 host 之後，就可以開始新增 *container* / *service* / *stack* 了
