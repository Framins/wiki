# POST

POST請求的方法有四種。

前兩種方法也是大多數 Browser 支援的傳送方法，也是目前 form 唯二可以支持的方法。後兩種是 AJAX 流行後，所定義出來的新方法。

## application/x-www-form-urlencoded

Browser native form，它會依 `key1=val1&val2=val2.....` 的方式做 URL encode。

大部分 AJAX 也都是用這樣的方式在 post 資料的。

## multipart/form-data

當想上傳檔案時，就需要加入 `enctype="multipart/form-data"` ，以讓 form 可以傳送檔案，並做檔案的編碼。

## application/json

好處就是可以很方便的提交複雜的資料結構，特別是 RESTful 的 API 。只是服務器後端處理並不是每個語言都有支持這樣的寫法，像 php 就沒辦法透過 `$_POST` 取得內容。不過有的框架已經開始在做這些處理了。

## text/xml

XML-RPC 即是透過 HTTP 傳送 XML 並傳送命令的格式。

但一般還是用 JSON 就好了。
