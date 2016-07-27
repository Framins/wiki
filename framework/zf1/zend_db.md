# Zend_Db

application.ini 設定多台 DB

```ini
// Main DB
resources.multidb.main.adapter = PDO_MYSQL
resources.multidb.main.host = localhost
resources.multidb.main.username = root
resources.multidb.main.password =
resources.multidb.main.dbname = main
resources.multidb.main.charset = utf8
 
// Sub DB
resources.multidb.sub.adapter = PDO_MYSQL
resources.multidb.sub.host = localhost
resources.multidb.sub.username = root
resources.multidb.sub.password =
resources.multidb.sub.dbname = sub
resources.multidb.sub.charset = utf8
```