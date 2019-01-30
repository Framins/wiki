# Regex

全名為 [Regular Expressions][]，大部分都簡稱為 *Regex*。

## Learning

這東西有點難體會，直接從案例中學習或許是個比較好的做法。

### 找特定字串

下面這個可以找到 `word` 的字

```
/word/
```

### 找開頭是特定字串

下面這個可以找到開頭是 `prefix` 字串

```
/^prefix/
```

## Tools

* http://www.regexper.com/ - 將 Regex 圖示化
* http://www.regexr.com/ - 線上編輯驗證
* http://rubular.com/ - Ruby 格式專用

## Example

記錄目前常用到的範例

### 常用匹配

Username / Password 

    /^[a-z0-9_-]{$A,$B}$/

> $A: 至少要幾字元，$B: 最多不能超過幾個字元

Email 

    /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

URL

    /^(https?:\/\/)?([\da-z\.-]+)\.([a-z\.]{2,6})([\/\w \.-]*)*\/?$/
    /(https?|ftp|file):\/\/[-a-zA-Z0-9+&@#/%?=~_|!:,.;]*[-a-zA-Z0-9+&@#/%=~_|]/

HTML Tag

    /^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/

[Regular Expressions]: https://en.wikipedia.org/wiki/Regular_expression
