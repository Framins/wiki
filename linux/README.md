# Linux

此地方只記錄常用的，其他的 Google 查一下就一堆資料了。

* [指令小技巧](command-tricks.md)
* Shell script 請參考 [/pdl/bash/README.md](/pdl/bash/README.md)
* Make 請參考 [/pdl/make/README.md](/pdl/make/README.md)

## Distributions

目前較知名的 Linux 發行版如下：

* [Debian](http://www.debian.org/)
* [Ubuntu](http://www.ubuntu.com/)
* [Fedora](https://fedoraproject.org/)
* [CentOS](http://www.centos.org/)
* [Slackware](http://www.slackware.com/)
* [SUSE](https://www.suse.com/)

想要查目前使用什麼版本的 Linux 可以下這個指令：

```bash
cat /etc/issue
# or
lsb_release -a
```

## Commands

* [cat](command/cat.md)
* [date](command/date.md)
* [getopt](command/getopt.md)
* [shuf](command/shuf.md)

## Network

[網路相關指令](command/network-commands.md)

> 網路基礎知識可以參考[這裡](/network/README.md)

## Topics

一些主題性的內容

* [fish](fish.md)
* [LVM](lvm.md)
* [tmux](tmux.md)
* [Powerline](powerline.md)
* [Wine](wine.md)

命令提示字元

* [終端機快捷鍵](terminal-shortkey.md)
* https://blog.gtwang.org/linux/how-to-make-a-fancy-and-useful-bash-prompt-in-linux-1/

## FAQs

* [SublimeText2 中文輸入問題解](http://samwlinux.blogspot.tw/2014/04/ubuntusublimetext2deb.html)

## 無蝦米

使用 fcitx，指令如下：

```
sudo apt-get install fcitx fcitx-table-boshiamy im-config

im-config # 選擇輸入法
```

試過可行的

* Ubuntu 14.04
* Linux Mint 18

[參考網頁](http://www.j4.com.tw/comp-qna/ubuntu-14-04-%E7%94%A8fcitx-%E8%A3%9D%E5%98%B8%E8%9D%A6%E7%B1%B3%E8%BC%B8%E5%85%A5%E6%B3%95/)

## References

* [鳥哥的Linux私房菜](http://linux.vbird.org/)
