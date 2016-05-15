Generate Key
============

產生 SSH Keys 的方法很簡單，在終端機下輸入下面指令即可：

    $ ssh-keygen -t rsa -C "youremail@example.com"
    Generating public/private rsa key pair.
    Enter file in which to save the key (/home/username/.ssh/id_rsa):     // 存放 key 的位置，使用預設的就好，除非很多不一樣的 key 要做管理....
    Created directory '/home/username/.ssh'.
    Enter passphrase (empty for no passphrase):                           // 打密碼，如果有打的話，下一個就是重復，也可以不用打。
    Enter same passphrase again:
    Your identification has been saved in /home/username/.ssh/id_rsa.
    Your public key has been saved in /home/username/.ssh/id_rsa.pub.
    The key fingerprint is:
    xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx:xx

以上例來說：

  * public key 會存在 `/home/username/.ssh/id_rsa.pub` (通常都存在使用者資料夾裡的 `.ssh/` 裡)
  * private key 則是在 `/home/username/.ssh/id_rsa`

這兩個是一對的，一個是要公開讓別人可以上的鎖，另一個是要解鎖的鑰匙。

> 這兩個的關係就像喇叭鎖一樣，任何人都能用公鑰上鎖，可是解鎖的私鑰在建立的人身上。
