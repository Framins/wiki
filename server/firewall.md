# Firewall

使用 Linux 的 `iptables` 指令實作防火牆

* Example

防火牆最基本的規則就是檔掉全部，只開放所需要的服務。實際的設定流程如下：

1. 清除所有規則
2. 設定預設政策
3. 信任本機
4. 回應封包
5. 信任用戶
6. 設定例外規則

通常都會寫成 shell script 來執行

## Show

最簡單的語法，看目前規則：

    # iptables -L -n

* `-t` 後面接 table，如 `net` / `filter`，如果沒加，會列出預設的 `filter`
* `-L` 列出目前的 table 規則
* `-n` 不進行 IP 與 HOSTNAME 的反查，速度會比較快
* `-v` 列出更多資訊

比方說，看 `filter` 的內容：

    # iptables -L -n
    Chain INPUT (policy ACCEPT)
    target     prot opt source               destination         

    Chain FORWARD (policy ACCEPT)
    target     prot opt source               destination         

    Chain OUTPUT (policy ACCEPT)
    target     prot opt source               destination  

* `target` 進行的動作，有 `ACCEPT` `REJECT` `DROP`
* `prot` 封包協定
* `opt` 額外的選項說明
* `source` 針對哪個來源 IP 進行限制
* `destination` 針對哪個目標 IP 進行限制

## Clear

清除規則要下三個指令

    # iptables -F
    # iptables -X
    # iptables -Z

* `-F` 清除所有的規則
* `-X` 清除所有自定的 chain / tables
* `-Z` 將所有計數與流量統計歸零

## Default Policy

使用 `-P` 選項，語法如下：

    # iptables [-t nat] -P [INPUT,OUTPUT,FORWARD] [ACCEPT,DROP]

一般都是 `INPUT` 預設會 `DROP`，如：

    # iptables -P INPUT   DROP
    # iptables -P OUTPUT  ACCEPT
    # iptables -P FORWARD ACCEPT

> 設定的時候要注意，如果預設設定成 `DROP` 又沒有特別設定哪個規則 `ACCEPT`，會被防火牆擋在外面，然後就等著準備重開電腦了。

## Example

```bash
#!/bin/bash
# 全域設定值
EXTIF="eth0"                          # 連上網路的網卡
OPEN_PORT="22 80"                     # 開啟的 port
OPEN_ICMP="0 3 3/4 4 11 12 14 16 18"  # 開啟的 icmp
export EXTIF

# 1. 設定核心網路功能
echo "1" > /proc/sys/net/ipv4/tcp_syncookies
echo "1" > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
for i in /proc/sys/net/ipv4/conf/*/{rp_filter,log_martians}; do
  echo "1" > $i
done

for i in /proc/sys/net/ipv4/conf/*/{accept_source_route,accept_redirects,send_redirects}; do
  echo "0" > $i
done

# 2. 清除規則
PATH=/sbin:/usr/sbin:/bin:/usr/bin:/usr/local/sbin:/usr/local/bin; export PATH
iptables -F
iptables -X
iptables -Z

# 3. 預設政策
iptables -P INPUT   DROP
iptables -P OUTPUT  ACCEPT
iptables -P FORWARD ACCEPT

# 4. 開放 lo 與相關的設定值
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m state --state RELATED,ESTABLISHED -j ACCEPT

# 5. 啟動額外的防火牆 script 模組
if [ -f /usr/local/virus/iptables/iptables.deny ]; then
  sh /usr/local/virus/iptables/iptables.deny
fi
if [ -f /usr/local/virus/iptables/iptables.allow ]; then
  sh /usr/local/virus/iptables/iptables.allow
fi
if [ -f /usr/local/virus/httpd-err/iptables.http ]; then
  sh /usr/local/virus/httpd-err/iptables.http
fi

# 6. 允許某些類型的 ICMP 封包進入
for tyicmp in $OPEN_ICMP
do
  iptables -A INPUT -i $EXTIF -p icmp --icmp-type $tyicmp -j ACCEPT
done

# 7. 允許的服務
for port in $OPEN_PORT
do
  iptables -A INPUT -p TCP -i $EXTIF --dport $port -j ACCEPT
done
```

## Reference

* [鳥哥的 Firewall](http://linux.vbird.org/linux_server/0250simple_firewall.php)
* http://s2.naes.tn.edu.tw/~kv/iptables.htm
* https://wiki.debian.org/iptables
* http://linux.vbird.org/linux_server/0250simple_firewall.php#local_script
