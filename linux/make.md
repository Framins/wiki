# make

make 是 Unix-like 環境下，一個功能強大的輔助編譯工具

參考網頁：

* http://maxubuntu.blogspot.tw/2010/02/makefile.html
* http://wiki.ubuntu.org.cn/index.php?title=%E8%B7%9F%E6%88%91%E4%B8%80%E8%B5%B7%E5%86%99Makefile:%E4%BD%BF%E7%94%A8%E5%87%BD%E6%95%B0&variant=zh-hant
* http://forum.slime.com.tw/thread122483.html
* http://dywang.csie.cyut.edu.tw/moodle23/dywang/linuxProgram/node39.html
* http://stackoverflow.com/questions/3275449/can-a-makefile-have-a-directory-as-a-target
* http://lalakiwe.sg1006.myweb.hinet.net/Documents/Makefile/MakefileTotal.pdf
* http://tetralet.luna.com.tw/index.php?op=ViewArticle&articleId=185

## SUFFIXS & PHONY

* `.SUFFIXS` 是跟 make 說，有哪些副檔名要加入隱含規則中。
* `PHONY` 相反，它是跟 make 說，哪些東西是標記，而不是檔案。
* `$@` 代表 target 本身
* `$<` 代表第一個 dependency

## if statement

make 可以根據條件不同，執行不同的分支。

語法如下：

```
[conditional-directive]
[text-if-true]
else
<text-if-false>
endif
```

第一個 [conditional-directive] 表示判斷條件的關鍵字，有四個：

```
ifeq (a, b)   # 比較 a, b 是否相同
ifneq (a, b)  # 比較 a, b 是否不同
ifdef <var>   # 測試 var 是否有設定值
ifndef <var>  # 測試 var 是否沒有設定值
```
