# Database

Rails 新專案預設使用 SQLite 資料庫，預設的設定檔在 `config/database.yml`

```yaml
default: &default
  adapter: sqlite3
  pool: 5
  timeout: 5000

development:
  <<: *default
  database: db/development.sqlite3

test:
  <<: *default
  database: db/test.sqlite3

production:
  <<: *default
  database: db/production.sqlite3
```

> test 會有段註解跟你說，不要把 test 資料庫跟 production 和 development 設成同一個

這裡可以看到，`database.yml` 定義了三個不同的環境設定

* `development` 開發模式，用在平常開發
* `test` 測試模式，用在單元自動化測試
* `production` 正式上線

如果要建立資料庫的話，可以執行下面這指令：

    rake db:create

如果資料庫結構有變更的時候（如新增 Model)，執行下面這個指令：

    rake db:migrate
