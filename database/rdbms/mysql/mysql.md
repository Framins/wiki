MySQL
=====

改密碼的方法：

http://emn178.pixnet.net/blog/post/87659567-mysql%E4%BF%AE%E6%94%B9%E5%AF%86%E7%A2%BC%E8%88%87%E5%BF%98%E8%A8%98%E5%AF%86%E7%A2%BC%E9%87%8D%E8%A8%AD

基本語法：

http://mail.hmes.kh.edu.tw/~jona/redhat/mysqlphp/mysqlsyntax.htm

Basic
-----

建立資料庫

```sql
CREATE DATABASE db_name;
```

使用資料庫

```sql
USE db_name;
```

刪除資料庫

```sql
DROP DATABASE [IF EXISTS] db_name;
```

建立資料表

```sql
CREATE TABLE table_name (
  column1 data_type,
  column2 data_type,
  ...
);
```

ZEROFILL屬性：

在定義數字類型的欄位時，有時會希望左邊要補 0 ，如 `INT(3)` 在資料是 1 時，輸出會是 `001` 。這時只要屬性加入 ZEROFILL 即可。而加入 ZEROFILL 屬性時， `UNSIGNED` 也會強制被加入。

```sql
CREATE TABLE test (
  test_id INT(3) UNSIGNED ZEROFILL
)
```

> `ZEROFILL` 好像是 MySQL 專屬功能，其他資料庫只能個別實作了。
