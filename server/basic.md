# Basic

架 server 的基礎

## Check

服務啟動了，該怎麼確認是否開啟成功，比方說，開了一個 mysqld，該怎麼知道它真的是在那邊運作了呢？

* 最直接的方法就是連線下去就對了，連成功就是有，連失敗就是死。
* 直接查程序是否有在執行： `ps -aux | grep mysqld`，但必須要知道這個服務的程序名稱。
* 通常服務開啟後，會監聽在某個 port，所以也可以查 port 是否正在被監聽： `netstat -tnlp | grep 3306`，一樣必須要知道這個服務預設的監聽 port。

## 自動校時

先執行 `crontab -e`，然後加入以下內容

```
* */1 * * * (/usr/sbin/ntpdate 118.163.81.61 && /sbin/hwclock -w) &> /dev/null
0 5 * * * ntpdate tick.stdtime.gov.tw
```

## Tools

* [tmux](/linux/tmux.md) - 多工終端機
* [Mosh](http://blog.longwin.com.tw/2012/11/mosh-replcae-ssh-2012/)
* [ClusterSSH](http://os.51cto.com/art/201103/250014.htm)

## apt

* http://pangomi.blogspot.tw/2013/06/apt-get-notes-ubuntu-1204lts.html
* http://wiki.linuxdeepin.com/index.php?title=%E8%BD%AF%E4%BB%B6%E5%8C%85%E7%AE%A1%E7%90%86
