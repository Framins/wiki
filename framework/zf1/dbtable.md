# DbTable

DbTable 是一個抽象化物件，可以透過此抽象化物件，來對資料庫的資料表做存取。

## Setup

既然是跟資料庫相關的話，當然免不了要先安裝資料庫相關的軟體和設定配置等前置動作。

如果想用 [SQLite][] 的話，必須先安裝後再重開 httpd 伺服器才會生效：

    apt-get install php5-sqlite
    service apache2 restart

## Configuration

在 `application.ini` 設定，以 MySQL 為例：

```ini
resources.db.adapter = PDO_MYSQL
resources.db.params.host = localhost
resources.db.params.username = username
resources.db.params.password = password
resources.db.params.dbname = database
```

如果是 SQLite ：

```ini
resources.db.adapter = PDO_SQLITE
resources.db.params.dbname = APPLICATION_PATH "/../data/db/database.db"
```

[SQLite]: /database/sqlite
