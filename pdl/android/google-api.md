# Google API

Google 有提供一個網頁叫[Developers Console](https://console.developers.google.com/) ，可供開發人員管理 API 的啟動和付費等。

* APIs - 可以知道目前啟動了哪些服務
* Credentials - 在這裡就可以決定哪些裝置可以存取上面APIs啟動的服務
  * OAuth - 還不會實作，不過安全性顯然比較高。
  * Public API access - 可以產生四種裝置的 Key ，並允許該裝置存取 API ；因為是公開的 API Key ，所以必需要過濾不明的存取來源，才能保證 Services 的安全。
    * Server - 使用 Server 端的 IP 當作過濾條件
    * Browser - 使用被瀏覽的網站的網址當作過濾條件
    * Android - 使用金鑰的憑證指紋(SHA1)和 Package 名稱當作過濾條件。
    * iOS - 使用 bundle identifier 當作過濾條件。
* Consent screen
* Push

## Android Key

Android Key的申請方式大概如下：

1. 取得 SHA1
2. 建立 API Project
3. APIs -> 選擇服務
4. Credentials -> Add Android Key
5. 輸入 SHA1 + 分號(;) + package name ，再按 create ；如果正確的話，就會出現 API key 了
6. 安裝 Google Play services SDK
7. 設定 App 權限

References
----------

* http://www.moke.tw/wordpress/computer/advanced/410
