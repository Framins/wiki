# git log

git log 最基本同時也是個強大的指令，[官方說明](http://git-scm.com/book/zh-tw/Git-%E5%9F%BA%E7%A4%8E-%E6%AA%A2%E8%A6%96%E6%8F%90%E4%BA%A4%E7%9A%84%E6%AD%B7%E5%8F%B2%E8%A8%98%E9%8C%84)

以下使用 [jquery repo](https://github.com/jquery/jquery) 做測試

## Basic Query

如果不加參數的話，就是單純把每個 commit 按照時間一筆一筆顯示

```
$ git log
commit da148f158f40b474841ad7a60cc39c5868cf420c
Author: Michał Gołębiowski <XXX@gmail.com>
Date:   Fri May 2 16:03:52 2014 +0200

    Core: Correct the number of expected tests

commit 69d4a48ff67188214bc28ec1a4d138c5997ce171
Author: Liang Peng <XXX@gmail.com>
Date:   Thu May 1 19:37:23 2014 +0800

    Core: Remove repeated test
    
    Closes gh-1570

...
```

加上 `--stat` 選項可以有比較詳細的內容，如哪些檔案被改、改了幾行等。

```
$ git log --stat
commit da148f158f40b474841ad7a60cc39c5868cf420c
Author: Michał Gołębiowski <m.goleb@gmail.com>
Date:   Fri May 2 16:03:52 2014 +0200

    Core: Correct the number of expected tests

 test/unit/core.js | 2 +-
 1 file changed, 1 insertion(+), 1 deletion(-)

commit 69d4a48ff67188214bc28ec1a4d138c5997ce171
Author: Liang Peng <poppinlp@gmail.com>
Date:   Thu May 1 19:37:23 2014 +0800

    Core: Remove repeated test
    
    Closes gh-1570

 test/unit/core.js | 1 -
 1 file changed, 1 deletion(-)
```

如果要看 commit 的詳細資訊，要使用 show 指令
