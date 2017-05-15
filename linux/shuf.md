shuf
====

shuf 指令可以在原始文件中隨機找幾行，然後輸出。

Installation
------------

Mac 需要另外安裝，指令如下：

```bash
$ brew install coreutils
```

使用的時候要用 `gshuf` 而不是 `shuf`

Linux 試過 Docker 的 Alpine / Debian 都有內建

Usage
-----

最簡單的用法，這個命令可以在資料裡隨機找五行，並印出來：

```bash
$ shuf -n5 data.txt
```

References
----------

* https://apple.stackexchange.com/questions/142860/install-shuf-on-os-x
