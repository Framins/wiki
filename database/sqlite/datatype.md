DataType
========

一般 SQL 資料庫使用靜態的欄位型態，而 SQLite 是使用動態的欄位型態。靜態的欄位型態是在定義資料庫時，就決定了它的欄位只能存何種資料了。動態的欄位型態是決定於資料本身的型態，不僅可相容靜態欄位型態，還能做出很多靜態欄位型態無法實現的功能。

Class
-----

SQLite 支援五種類型和資料型態 ([SQLite 官方說明](http://www.sqlite.org/datatype3.html))

* `NULL` 空值
* `INTEGER` 整數
* `REAL` 實數，也就是浮點數。
* `TEXT` 文字資料，編碼會依照資料庫的編碼。
* `BLOB` 二進位資料。

Type
----

SQLite 並不支援 Boolean 儲存類型，但可以使用 `INTEGER 0` (false) 或是 `INTEGER 1` (true) 來代替。

SQLite 也不支援日期或時間的類型，此類型的資料會依 SQLite 內建的日期時間函數，轉存成 `TEXT` / `REAL` / `INTEGER` 。

* `TEXT` ISO8601 字串 `YYYY-MM-DD HH:MM:SS.SSS` 。
* `REAL` 儒略曆時間，計算開始時間依據公曆，格林威治時間，西元前 4714 年 11 月 24 日中午 12 點起。
* `INTEGER` Unix 時間，以秒為單位，起始時間 `1970-01-01 00:00:00 UTC` 。

Type Affinity
-------------

SQLite 為了相容其他資料庫，它有個特別的概念是**相似性型態**。它是一個存在欄位裡資料的建議資料型態，只是建議而非必需，任何欄位一樣可以儲存任何型態的資料。

* `TEXT` 使用 NULL , TEXT, BOLB 類別。數值資料會先被轉成字串後才存入。
* `NUMERIC` 使用所有類別。字串如果可以無誤差轉成數值再無誤差轉回字串時，則字串會轉成 INTEGER / REAL ；如果沒辦法做到無誤差轉換時，則存成 TEXT ； NULL 和 BLOB 不轉換直接存入。
* `INTEGER` 同 NUMERIC ，只是不會有浮點數。
* `REAL` 同 NUMERIC ，只是會強制轉換成浮點數。
* `NONE` 不轉換

欄位型態相容性的計算，是有規則與順序的。

- 型態名稱包含字串 "INT" 會被指定成 "INTEGER"。
- 型態名稱包含字串 "CAHR", "CLOB", "TEXT" 都會指定成 "TEXT"。
- 型態名稱包含字串 "BLOB" 或沒有名稱則指定成 "NONE"。
- 型態名稱包含字串 "REAL", "FLOA", "DOUB" 都會指定成 "REAL"。
- 其它則都指定成 "NUMERIC"。

需要注意的是順序性，比方說， "FLOATING POINT" 會被指定成 "INTEGER" ，因為字尾的 INT 符合第一條規則，所以第四條規則就不被採用了。

Comparison Expressions
----------------------

再來這部分就比較需要探討了，因為可以欄位型態是動態的，所以不同的型態該如何比較？

先了解 SQLite 有哪些比較運算子："=", "<", "<=", ">=", "!=", "IN", "BETWEEN", "IS"。再來規則如下：

1. NULL 是最小的
2. INTEGER / REAL 比 TEXT / BLOB 小。而 INTEGER / REAL 互相比較時，則使用數值比較方式。
3. TEXT 比 BLOB 小，TEXT 互相比較時，會採用適當的排序方法。
4. BLOB 比較時，依據 memcmp() 來比較。

SQLite 可能會在 INTEGER, REAL, TEXT 互相比較時，轉換成相同的儲存類別。規則請參考原文。

Reference
---------

* [SQLite語法表](http://jimmy0222.pixnet.net/blog/post/37025726-sqlite%E8%AA%9E%E6%B3%95%E8%A1%A8) @ [吉米.NET](http://jimmy0222.pixnet.net/blog)
* [SQLite Query Language: Datatypes In SQLite](http://jyhshin.pixnet.net/blog/post/31988011-sqlite-query-language%3A-datatypes-in-sqlite) @ [邱小新の工作筆記](http://jyhshin.pixnet.net/blog)
