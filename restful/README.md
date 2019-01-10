# RESTful

## HTTP Method

| Method | Description |
| ------ | ----------- |
| GET | 讀取資源 (safe & idempotent)|
| PUT | 替換資源 (idempotent) |
| DELETE | 刪除資源 (idempotent) |
| POST | 新增資源；也作為萬用動詞，處理其它要求 |
| PATCH | 更新資源部份內容 |
| HEAD | 類似GET，但只回傳HTTP header (safe & idempotent) |

> 可參考 [wiki](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods)

## [HTTP/1.1][] Method Definitions

* Safe : 請求不會產生資源更動 (not modify resources)
* Idempotent : 不管執行幾次，結果都跟只有執行一次一樣。

| Method | Safe | Idempotent |
| ------ | ---- | ---- |
| GET | Y |	Y |
| POST | N | N |
| PATCH |	N |	N |
| PUT |	N | Y |
| DELETE | N | Y |

> Safe 特性會影響是否可以快取。而 Idempotent 特性則是會影響可否 Retry (重試，反正結果一樣)。

## Reference

* [簡明RESTful API設計要點](https://tw.twincl.com/@arthurtw/*641y)
* [淺談 REST 軟體架構風格 (Part.I) - 從了解 REST 到設計 RESTful！](http://blog.toright.com/posts/725)
* [淺談 REST 軟體架構風格 (Part.II) - 如何設計 RESTful Web Service？](http://blog.toright.com/posts/1399)
* [什麼是REST跟RESTful?](https://ihower.tw/blog/archives/1542)
* [理解RESTful架构](http://www.ruanyifeng.com/blog/2011/09/restful.html)

[HTTP/1.1]: https://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html
