SQLite
======

[SQLite](http://www.sqlite.org/) 的特色就是小。 Library 容量小、 Memory 佔用小、適用的裝置也是小。

以下筆記以 SQLite 3 為主。

* DataType

Create
------

建立資料庫，只要下這行命令即可：


    sqlite dbname

下完之後，會自動開啟資料庫，並進入 SQLite 的命令提示字元，再來就可以建立資料表了：

```sql
CREATE TABLE nestedSet (
  id INT AUTO_INCREMENT PRIMARY KEY,
  name VARCHAR(20) NOT NULL,
  lft INT NOT NULL,
  rgt INT NOT NULL
);
```

Import
------

匯入資料庫，通常都是從 `.sql` 檔做匯入：

    sqlite> .read db.sql

或是直接從 shell 下：

    cat db.sql | sqlite3 database.db

> 記得 SQL 檔裡的每個 SQL 命令結尾都必須加上分號 `;`

Reference
---------

* http://mybeauty.pixnet.net/blog/post/26492636-sqlite%E7%B0%A1%E4%BB%8B
* http://www.tutorialspoint.com/sqlite/
* https://ariejan.net/2006/10/13/migrate-sqlite3-to-mysql-easily/
* http://stackoverflow.com/questions/18671/quick-easy-way-to-migrate-sqlite3-to-mysql
