Regex
=====

全名為 [Regular Expressions][] ，大部分都簡稱為 *Regex* 

Tools
-----

* http://www.regexper.com/ - 將Regex圖示化
* http://www.regexr.com/ - 線上編輯驗證
* http://rubular.com/ - Ruby格式專用

Example
-------

記錄目前常用到的範例

### 常用匹配

Username/Password 

    /^[a-z0-9_-]{%1,%2}$/

> %1: 至少要幾字元，%2: 最多不能超過幾個字元

Email 

    /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

URL

    /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
    /(https?|ftp|file):\/\/[-a-zA-Z0-9+&@#/%?=~_|!:,.;]*[-a-zA-Z0-9+&@#/%=~_|]/

HTML Tag

    /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/

### Dokuwiki Transfer

連結轉換：

```
[[http://example.com|Link]]  =>  [Link](http//example.com)
```

Pattern

```regex
\[\[([^|\]]*)\|([^\]]*)]]
```

Replace

```
[$2]($1)
```


[Regular Expressions]: https://en.wikipedia.org/wiki/Regular_expression
