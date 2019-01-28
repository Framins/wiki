# Migration

[官方說明](http://kejyun.github.io/Laravel-4-Documentation-Traditional-Chinese/docs/migrations/)

Migration 是資料庫的 VCS，記錄資料庫的修改過程。相同的概念也在 framework:ruby-on:rails: 裡有看過。

在多人開發時，常遇到的問題

* 開發者的開發階段不同，DB 的狀態也不同，雖然原始碼可以靠 VCS 合併整合，但 DB 沒辦法啊！
* 如果開發者更改 DB 沒有記錄，如果發生問題也無法還原

Migration 會做的事就是

* 對 DB 更改的動作，會寫對應的程式碼來完成
* 更改分成 up (前進) 和 down (後退)
* 開發者執行 `migrate` 後，每個人就會有相同的 DB 結構了
* 發生問題時，可以使用 rollback 回到 DB 之前的狀態

## Basic

建立 migration

    php artisan migrate:make create_users_table

產生的 migration 檔會放在 `app/database/migrations/` 目錄裡，檔名會有時間戳記，這樣 Laravel 才會知道執行的順序為何

執行 migrations

    php artisan migrate

復原 migrations

    php artisan migrate:rollback

重設 migration 記錄

    php artisan migrate:reset

重設並重新執行所有 migration

    php artisan migrate:refresh
