# Config

Laravel 的設定檔都放在 `app/config/` 裡，並依照 HTTP Host 來決定讀取哪一個設定檔，如測試主機和正式主機的資料庫設定是不一樣的。

設定環境預設的名稱如下：

* `app/config/` - Production 設定
* `app/config/local/` - Local 端，也就是 development 設定
* `app/config/testing/` - Unit Testing 設定

在開始寫程式前，需要先修改在 `app/config/app.php` 裡的 `Encryption Key` 。可以用 Artisan 自動產生：

    $ php artisan key:generate
