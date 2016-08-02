Rancher
=======

*RancherOS* 是 2015 年 3 月，由 [Rancher Labs](http://rancher.com/) 開發的 Container OS 。

這是一套只純粹執行 Docker 的作業系統。

Rancher 則是管理一群 RancherOS / container Orchestration Tools

Why Rancher
-----------

研究 RancherOS 是有很漫長的前因後果，其實這也是工程師偷懶的過程...

### 使用實體機器建置環境

曾經做過 Linux 主機管理者。當時還很菜，主機死掉，抓不到錯也只能重灌。

### 使用虛擬技術建置環境

後來發現 [VirtualBox](https://www.virtualbox.org/) 執行虛擬機不一定會比直接架一台 server 慢，加上 VM 有 snapshot 功能，壞了可以還原上次使用狀態的特性，開始轉向使用 VM

### 方便地建置環境

VM 每次要架不同種類的 server ，如 LAMP for 開發， Web/DB  for 上線，這樣就要重新安裝三次系統，每次搞都快瘋了。

這時發現了 [Vagrant](https://www.vagrantup.com/) ，基底系統直接 Vagrantfile + vagrant up 就有了，想要不同的 service 只要配不同的 script 即可安裝完成，超方便。

而且 Vagrantfile / script 都是純文字檔，可以很方便的拷貝給其他人建置環境，利於多人多工開發。

### 快速地建置環境

Vagrant 每次要重安裝時， run script 都需要安裝很長的時間，雖然可以 export box ，但就會失去輕巧 portable 特性了。

這時發現了 [Docker](https://www.docker.com/) ，它的應用隔離和映像檔建立非常地特別。 Vagrant 只要任何一個服務壞掉，可能就需要全部 reinstall ，這也是重新建置時間長的主因。 Docker 允許特定服務重新建立，意味著壞哪修哪是可以辦到的，太神奇了。

### 快速地建置更多環境

Docker 實務使用上，是適合把各應用拆開來執行的，但管理上就不一定那麼方便了，試想每個應用都執行一台 VM ，而每台 VM 又都要去管理，豈不瘋掉。這時發現了 [Rancher](http://rancher.com/rancher/) ，它正是解決此問題的最佳工具！

Features
--------

Rancher 是管理 RancherOS 的工具，而 RancherOS 的特色如下：

(以下說明參考[此文章](http://www.ithome.com.tw/news/95756))

此作業系統會啟動兩個 Docker ，一個是 for 系統使用的 *System Docker*，另一個是使用者想執行的 *User Docker* 。系統 Docker 會執行一般 Linux 啟動所需要的服務，如 udev 、 console 、 DHCP 服務，而且是使用打包好的 Docker 來執行。使用者 Docker 服務則是視使用者需求，如 Web 可以執行 apache / nginx 。

此設計架構非常的有趣，在 Docker 隔離架構下，即使把 User Docker 的 container 刪光光，也不會影響 System Docker 。如果 Docker 可以執行 Windows 的話，壞了就重 run 一個超方便的。

理想上， Rancher 可以做到簡易的叢集管理，不但簡化 MIS 的工作，還可增加 RD 對機器使用上的信心。

Quick Start
-----------

先用 Docker 安裝 server

```bash
docker run -d --name rancher --restart=always -p 80:8080 rancher/server
docker logs -f rancher-server
```

這樣這台電腦就可以當成是管理端的 server 了，可以用 web 去開，裡面會要求加 host 。加 host 的方式也很簡單，只要上去下一行指令就行了

接著要建立他的代理 server ，執行 docker

```bash
docker run -d --privileged -v /var/run/docker.sock:/var/run/docker.sock rancher/agent:v0.7.10 http://192.168.30.206:8080/v1/scripts/<token>
```

官網也有建議加 IP 參數

```bash
docker run -e CATTLE_AGENT_IP=192.168.1.1 -d --privileged -v /var/run/docker.sock:/var/run/docker.sock rancher/agent:v0.7.10 http://172.17.0.3:8080/v1/scripts/<token>
```

Usage
-----

* [Installation](installation.md)
* [RancherOS](rancher-os.md)
* [Stack](stack.md)
* [Service](service.md)
