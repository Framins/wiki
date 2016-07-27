# Zend_Db_Adapter

取得 `Zend_Db_Adapter` 物件的方法很簡單：

```php
$db = Zend_Db::factory('Pdo_Mysql', array(
    'host'     => 'localhost',
    'username' => 'user',
    'password' => 'pass',
    'dbname'   => 'db'
));
```

## quote()

會先對字串做 escape 後，再加上前後的引號。回傳值就可以直接代入 SQL statement 裡了

```php
$name = $db->quote("O'Reilly");
// 'O\'Reilly'

$sql = $db->query("SELECT * FROM table WHERE name = " .  $name);
```

## quoteInto()

```php
$sql = $db->quoteInto("SELECT * FROM table WHERE name = ?", "O'Reilly");
```

## quoteIdentifier()

```php

$tableName = $db->quoteIdentifier("table");
$sql = "SELECT * FROM $tableName";

echo $sql;
// SELECT * FROM `table`
```

## Insert

資料庫schema略。

```php
$data = array(
    'name' => 'test',
    'date' => new Zend_Db_Expr('Now()')  // 如果想用資料庫內建函式時，可以用Zend_Db_Expr類別
);
    	
$db->insert($table, $data);

// 取得 Generated ID
$id = $db->lastInsertId();
```

## Update

```php
$data = array(
    'name' => 'test',
    'date' => new Zend_Db_Expr('Now()')
);

$where[] = 'id = 1';
// 這樣也可以
// $where['id = ?'] = 1;
// 或是直接傳字串
// $where = 'id = 1';
 
$n = $db->update($table, $data, $where);
```

## Delete

```php
$n = $db->delete($table, 'id = 1');
// $n 代表被刪了幾筆
```

## Transaction

```php
try {
    // 現在開始一個交易
    $db->beginTransaction();

    // 執行動作
    $db->query("...");
    $db->query("...");
    $db->query("...");

    // 提交，若有錯誤，會拋出例外
    $db->commit();

} catch (Exception $e) {
    // 把db狀態復原，然後顯示訊息
    $db->rollBack();
    echo $e->getMessage();
}
```

## Column Descriptions

此 function 執行結果會跟 developer:framework:zend-framework:zend_db_table_abstract 所定義的 `protected $_cols;` 有關

```php
abstract public function describeTable($tableName, $schemaName = null);
```