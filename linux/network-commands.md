Network Commands
================

以下分別使用 [alpine:3.4](https://hub.docker.com/_/alpine/) 和 [debian:jessie](https://hub.docker.com/_/debian/) 測試

Configuration Commands
----------------------

> Debian 需要下 `apt-get install net-tools` 安裝才能使用這些指令

#### ifconfig

直接執行會出現

    eth0      Link encap:Ethernet  HWaddr 02:42:ac:11:00:03
              inet addr:172.17.0.3  Bcast:0.0.0.0  Mask:255.255.0.0
              inet6 addr: fe80::42:acff:fe11:3/64 Scope:Link
              UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
              RX packets:7261 errors:0 dropped:0 overruns:0 frame:0
              TX packets:2729 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:0
              RX bytes:10599973 (10.1 MiB)  TX bytes:151347 (147.7 KiB)

相關名詞如下：

* **eth0** 網路卡代號
* **HWaddr** 也就是 MAC address
* **inet** IPv4 位址
* **Bcast** Broadcast
* **Mask** netmask
* **inet6** IVv6 位址
* **MTU** [參考鳥哥的 Linux](http://linux.vbird.org/linux_server/0110network_basic.php#tcpip_link_mtu)
* **RX** 接收的封包數，相對的 **TX** 是傳送的封包數
  + **errors** 封包發生錯誤的數量
  + **dropped** 封包因為有問題被丟棄的數量
  + **collisions** 封包碰撞的狀況
  + **txqueuelen** 傳送資料的 buffer 長度

從 errors 和 collisions 可以大概了解網路是否正常

#### route
#### ip

Debug Commands
--------------

#### ping
#### traceroute

> Debian 需要下 `apt-get install inetutils-traceroute` 安裝這個指令

#### netstat
#### host
#### nslookup
#### lsof 

find out which process occupies the port
``` bash
lsof -nP | grep LISTEN
```

References
----------

* [Linux 常用網路指令](http://linux.vbird.org/linux_server/0140networkcommand.php) @鳥哥的 Linux 私房菜
