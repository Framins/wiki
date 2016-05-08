Regex
=====

全名為 [Regular Expressions][] ，大部分都簡稱為 *Regex* 

Example
-------

記錄目前常用到的範例

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
