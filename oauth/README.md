OAuth
=====

Context
-------

有一個美圖軟體，功能是可以把 Facebook 上的照片修圖。使用者要用這個服務的話，就必須讓這個美圖軟體能讀取使用者儲存在 Facebook 上的照片。

當然，一定要使用者授權， Facebook 才會同意美圖軟體讀取使用者的照片。那美圖軟體讓如何得到使用者的授權？

最直覺最簡單的方法：使用者把 Facebook 的帳號密碼給美圖軟體，這樣就可以讀取使用者的照片了。只是這樣做會有下面的缺點：

* 美圖軟體需要保存密碼才能繼續它的服務
* 美圖軟體有了使用者在 Facebook 的所有權力，使用者沒辦法限制範圍和期限
* 使用者只有改密碼才能回收權力，但其他使用者授權的第三方應用程式全部都會失效
* 只要有一個第三方應用程式被駭客入侵了，就會導致使用者密碼外泄，包括在 Facebook 所有資料都外泄

OAuth 是為了解決上面問題而產生的。

Terms
-----

* Third-party application - 第三方應用程式，也稱 client ，即上例的「美圖軟體」。
* Resource Owner - 資源所有者，即「使用者」。
* Service - 服務提供者，即上例的「Facebook」。
* Authorization Server - 認證伺服器，服務提供者專門用來處理認證的伺服器
* Resource Server - 資源伺服器，服務提供者用來存放使用者受保護資源的伺服器。

Concept
-------

OAuth 在 client 與 service 之間設置了一個 authorization layer ， client 不能直接登入 service ，只能登入 authorization layer ，用這樣的方法把 user 和 client 區分開來。 client  登入 authorization layer 用的 token 會跟 user 的密碼不同。 user 可以指令 authorization layer 的權限範圍和有效期限。

client 登入後， service 會依 token 的權限範圍和有效期限，向 client 開放 user 儲存的資料。

Basic Flow
----------

下圖源自 [RFC 6749 1.2](https://tools.ietf.org/html/rfc6749#section-1.2)

![](http://plantuml.com/plantuml/png/Syx9JCqhKT2rKmXABSulBKfEzI_FIosoKj0mr5HmB2t9o2_Ah4eioSpF0oeeB4qjBk52KQYW2zJg33O4gCS8NOzxKM9U2PSpt18KsU3KeZAmLSROjM5HZ6gT2L1VSd9gSR52I7vsQXwIFJ0tmgqmHLEAgW3LM3DDXO2Y_9BKv9BK5BX90000)

PlantUML code

```uml
@startuml
Client -> ResourceOwner: (1) Authorization Request
ResourceOwner --> Client: (2) Authorization Grant
Client -> AuthorizationServer: (3) Authorization Grant
AuthorizationServer --> Client: (4) Access Token
Client -> ResourceServer: (5) Access Token
ResourceServer --> Client: (6) Protected Resource
@enduml
```

* User 打開 clinet 後， client 要求 user 給予授權
* User 同意授權
* Client 使用上一步獲得的授權，向 authorization server 申請 token
* Authorization server 認證後，發放 token
* Client 使用 token 向 resource server 要受保護的資源
* Resource server 確認 token 無誤，同意向 client 開發資源

可以看得出，上例的 2 是關鍵： user 該如何給 client 授權。

Authorization Types
-------------------

授權的模式有四種，源自 [RFC 6749 1.3](https://tools.ietf.org/html/rfc6749#section-1.3)

* Authorization code
* Implicit
* Resource owner password credentials
* Client credentials

Reference
---------

* http://oauth.net/2/
* http://www.ruanyifeng.com/blog/2014/05/oauth_2_0.html
* https://backstage.forgerock.com/#!/docs/openam/10.1.0/admin-guide/chap-oauth2
* [OAuth 2.0 筆記 (1) 世界觀](http://blog.yorkxin.org/posts/2013/09/30/oauth2-1-introduction/)
* [OAuth 2.0 Authorization Protocol](https://malalanayake.wordpress.com/2013/01/17/oauth-2-0-authorization-protocol/)
