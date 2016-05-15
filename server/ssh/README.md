SSH
===

  * Generate Key
  * [免密碼登入](http://www.gtwang.org/2014/05/linux-ssh-public-key-authentication.html)

Debian 系列安裝：

    # apt-get install ssh

啟動/停止

    # service ssh start     # 啟動
    # service ssh stop      # 停止

監聽埠

    # netstat -tnlp | grep sshd
    tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      10825/sshd
    tcp6       0      0 :::22                   :::*                    LISTEN      10825/sshd

Configuration
-------------

設定檔在 ''/etc/ssh/sshd_config''

```conf
# 預設監聽的 port 是 22
Port 22

# 限制 root 不能登入，基本上這樣比較安全
PermitRootLogin no

# 限制能登入的使用者
# 使用空白鍵區隔使用者
AllowUsers user1 user2

# 使用密碼驗證身份
PasswordAuthentication yes

# Public key 的位置
# %h 代表登入使用者的家目錄位置
# %u 代表登入使用者的 username
# 記得 public key 的目錄和檔案要修改權限
AuthorizedKeysFile %h/.ssh/authorized_keys
```

改完設定記得重新讀取設定檔

    # service ssh reload

scp
---

scp 指令是複製兩台主機間的檔案，用法類似 cp 

scp 是靠 ssh 運作的，所以要先安裝好 ssh

基本用法：

    scp [-r] <from_host> <to_host>

`-r` 選項可以複製整個目錄

舉一個上傳的例子

    $ scp -r dirName miles@remote:/home/miles/

只要來源和目的地交換就會變成是下載

    $ scp -r miles@remote:/home/miles/dirName ./

Reference
---------

* [設定檔的完整說明](http://www.openbsd.org/cgi-bin/man.cgi/OpenBSD-current/man5/sshd_config.5?query=sshd_config)
* http://blog.udn.com/nigerchen/2262865
* https://sites.google.com/site/linuxcooltea/home/ubuntu-she-dingssh-yuan-duan-lian-xian-gong-neng
* http://city.shaform.com/blog/2014/06/21/fix-public-key-login-for-encrypted-home.html
