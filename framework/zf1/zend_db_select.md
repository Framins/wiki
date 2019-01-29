# Zend_Db_Select

使用物件提供的方法建構出 SQL 並查詢

`Zend_Db_Select` 與 `Zend_Db_Table_Select` 大同小異，只差在一個沒有指定 Table，一個有指定 Table。

所以，基本上 `Zend_Db_Table_Select` 是不需要使用 `from()` 的，以下用 `Zend_Db_Select` 做說明

## Initialization

`Zend_Db_Select` 取得方法

```php
// Database adapter
$db;

$select = $db->select();
```

`Zend_Db_Table_Select` 取得方法

```php
// DbTable
$table;

$select = $table->select();
```

DEBUG 方法

```php
// 顯示產生出來的SQL
echo $select->__toString();
```

Reset

```php
// 清除特定的部分
$select->reset(Zend_Db_Select::ORDER);
// 全部清除
$select->reset();
```

## Basic

### FROM statement

    from(array|string|\Zend_Db_Expr $name, array|string|\Zend_Db_Expr $cols = '*', string $schema = null)  

參數

* $name 資料表名稱，array 是要取別名用的: array('別名' => '資料表名')
* $col 該資料表裡的欄位名稱，欄位名稱也可以是 expression，一樣可以使用 `Zend_Db_Expr`，array 範例:  array('別名' => '欄位名', '欄位名')
* $schema Schema名稱

```php
$select->from(
    array('t' => 'table'),
    array('sum' => new Zend_Db_Expr('SUM(num)')),
    'database'
);
// SELECT SUM(num) AS `sum`
// FROM `database`.`table` AS `t`
```

### COLUMN statement

    columns(array| string|\Zend_Db_Expr $cols = '*', string $correlationName = null)

參數

* $cols 欄位名，或array: array('別名' => '欄位名或 expression')
* $correlationName 別名

```php
$select->from('table', `)
    ->columns(array('n' => 'number'))
;
// SELECT `table`.*, `table`.`number` AS `n`
// FROM `table`
```

### JOIN statement

    join(array|string|\Zend_Db_Expr $name, string $cond, array|string $cols = self::SQL_WILDCARD, string $schema = null)

參數

* $name 資料表名稱，用法同 from()
* $cond join的條件式
* $cols 欄位名，用法同 from()

> join 預設是 joinInner，其他 join 的格式都一樣：

* joinLeft
* joinRight
* joinFull

joinCross 與 joinNatural 不需要 $cond

```php
$select->from(array('t' => 'table'))
    ->join(array('o' => 'out'),
           't.id = o.fk_id',
           array())
;
// SELECT `t`.*
// FROM `table` AS `t`
// INNER JOIN `out` AS `o` ON t.id = o.fk_id
```

### WHERE Statement

範例

```php
$select->from('products')
    ->where('price > 100.00')
;
// SELECT `products`.*
// FROM `products`
// WHERE (price > 100.00)

$select->from('products')
    ->where('price > ?', $price)
;
// SELECT `products`.*
// FROM `products`
// WHERE (price > 100.00)

$select->from('products')
    ->where('price IN(?)', array(1, 2, 3))
;
// SELECT `products`.*
// FROM `products`
// WHERE (price IN(1, 2, 3))

$select->from('products')
    ->where('price > ?', 100)
    ->where('price < ?', 200)
;
// SELECT `products`.*
// FROM `products`
// WHERE (price > 100) AND (price < 200)

$select->from('products')
    ->where('price < ?', 100)
    ->orWhere('price > ?', 200)
;
// SELECT `products`.*
// FROM `products`
// WHERE (price < 100) OR (price > 200)
```

### GROUP BY

範例

```php
$select->group(array('a', 'b'));

// GROUP BY `a`, `b`
```

### HAVING

```php
$select->having('sum > ?', 10);
// HAVING (sum > 10)
```

### ORDER BY

範例

```php
$select->order(array(
    'col1',            // `col1` ASC
    'col2 ASC',        // `col2` ASC
    'col3 DESC'        // `col3` DESC
))
;

// ORDER BY `col1` ASC, `col2` ASC, `col3` DESC
```

#### LIMIT

範例

```php
$select->limit(20);
// LIMIT 20

$select->limit(20, 10);
// LIMIT 20 OFFSET 10

$select->limitPage(2, 10);
// LIMIT 20 OFFSET 10
// 第一個參數指的是頁數，第二個參數指的是一頁幾筆
```

#### DISTINCT

```php
$select->distinct();
```

#### UNION

## Executing Select Queries

#### Zend_Db_Select

`$db->query()` 會回傳 Statement 物件

```php
$stmt = $db->query($select);
$result = $stmt->fetchAll();
```

#### Zend_Db_Table_Select

```php
$select = $table->select();

// 取得多筆
$rows = $table->fetchAll($select);
// 或取得單筆
$row = $table->fetchRow($select);
```

## Executing Custom Queries

#### Zend_Db_Select

範例

```php
$sql = "SELECT * FROM `table`";

$db->fetchAll($sql);
$db->fetchAssoc($sql);
$db->fetchRow($sql);
$db->fetchCol($sql);
$db->fetchOne($sql);
$db->fetchPairs($sql);
```

#### Zend_Db_Table_Select

範例

```php
$sql = "SELECT * FROM `table`";

$db->fetchAll($sql);
$db->fetchRow($sql);
```
