# Auth

> 與身分驗證（Authentication）或授權（Authorization）相關的說明，皆放在此分類下。

## Terms

### Assertion

指的是一包資訊，允許跨網域的情況下，分享身分與安全資訊

### Issuer

引用 [RFC 7521](https://tools.ietf.org/html/rfc7521#section-3) 的描述

> The entity that creates and signs or integrity-protects the assertion is typically known as the "Issuer"


建立和簽署或保護 *Assertion* 的實體或服務，稱為 *Issuer*

### Relying Party

引用 [RFC 7521](https://tools.ietf.org/html/rfc7521#section-3) 的描述

> The entity that consumes the assertion and relies on its information is typically known as the "Relying Party"

需要使用 Assertion 並依賴裡面的資訊的實體或服務，稱為 *Relying Party*

### MAC - Message Authentication Code

[Message authentication code](https://zh.wikipedia.org/wiki/%E8%A8%8A%E6%81%AF%E9%91%91%E5%88%A5%E7%A2%BC)，參考 wiki ：這在密碼學中，是指一小段資訊。它可以用特定演算法，從原有的一包資訊來產生，目的是確定原本的資訊沒有被更改過。
