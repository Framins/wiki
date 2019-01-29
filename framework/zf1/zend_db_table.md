# Zend_Db_Table

## Defining

可以直接用欄位繼承的方式來定義資料表

```php
class Table extends Zend_Db_Table_Abstract
{
    protected $_name = 'table'; // 資料表名稱
    protected $_primary = 'id'; // 主鍵名稱
    protected $_schema = null; // 資料庫名稱，null 表示是目前的。
    protected $_cols; // 資料表欄位名稱，可用 Zend_Db_Adapter_Abstract::describeTable() 輸出
    protected $_rowClass = 'Zend_Db_Table_Row'; // 在 fetchRow() 時，會用到此 class
    protected $_rowsetClass = 'Zend_Db_Table_Rowset'; // 在 fetchAll() 時，會用到此 class
}
```

繼承 `Zend_Db_Table_Abstract` 後，即可做 Active Record 的操作。

## Initial

`Zend_Db_Table` 要能正常執行，就必須要有一個 adapter 物件，傳入的方法如下

```php
// adapter 物件
$db;

// 使用系統預設
Zend_Db_Table_Abstract::setDefaultAdapter($db);
$table = new Table();

// 直接傳入
$table = new Table(array('db' => $db));

// 使用 Zend_Registry 的 key
Zend_Registry::set('my_db', $db);
$table = new Table(array('db' => 'my_db'));
```

## Quote

`Zend_Db_Table` 本身並沒有提供 quote 的方法，不過有取得 adapter 的方法，quote 方法參考 [Zend_Db_Adapter](zend_db_adapter.md#Quote)

```php
$adapter = $table->getAdapter();
$where = $adapter->quoteInto('id = ?', 3);
```

## Insert

跟 [Zend_Db_Adapter](zend_db_adapter.md#Insert) 的方法一樣，只是因為已經知道是哪個 Table 了，所以不需要傳入 Table 參數。

```php
$data = array(
    'name' => 'test',
    'date' => new Zend_Db_Expr('Now()')
);

$table->insert($data);

// 取得 Generated ID
$id = $db->lastInsertId();
```

## Update

跟 [Zend_Db_Adapter](zend_db_adapter.md#Update) 的方法差不多

```php
$data = array(
    'name' => 'test',
    'date' => new Zend_Db_Expr('Now()')
);

$where = $table->getAdapter()->quoteInto('id = ?', 1);

$table->update($data, $where);
```

## Delete

```php
$where = $table->getAdapter()->quoteInto('id = ?', 1);

$table->delete($where);
```

## Find

依 primary key 去找 record，Find 得到的都會是 Rowset 物件

```php
// 單筆
$rows = $table->find(1);

// 多筆
$rows = $table->find(array(1, 2));

// 主鍵是複合鍵時，可以傳入兩個以上的 key
$rows = $table->find(1, 'A');
```

## Query

取得 Zend_Db_Table_Select 物件

```php
$select = $table->select();
```

## Relationship

Zend_Db_Table_Abstract 可以設定 Table 與 Table 間的關聯：

```php
class Table extends Zend_Db_Table_Abstract
{
    // 參考的資料表
    protected $_referenceMap = array(
        'Product' => array( // 關聯的名稱
            'columns'           => array('product_id'), // 此 Class 參考的外鍵
            'refTableClass'     => 'Products', // 關聯的 Table Class
            'refColumns'        => array('product_id'), // refTable 參考的欄位，通常為主鍵
            'onDelete'          => self::CASCADE, // 有關聯的記錄都會一起動作（此欄位是刪除，所以會一起刪除）
            'onUpdate'          => self::RESTRICT // 禁止父資料表動作（此欄位是修改，所以是禁止修改
        ),
        ...
    );

    // 依賴的資料表
    protected $_dependentTables = array('Products');
}
```

### One-To-One, Many-To-One

在廣義的定義上，一對一和多對一其實基本概念是一樣的東西：

> A 資料表某個欄位，關聯到 B 資料表的某一個 unique 屬性的欄位
>
> 如：「文章資料表規定每篇文章只能歸類在某個分類裡；該欄位的值即為分類資料表的唯一鍵。」

Zend 可以設定這兩個資料表的關聯：

A 資料表（文章資料表）己設定如下：

```php
class Article extends Zend_Db_Table_Abstract
{
    protected $_referenceMap = array(
        'Category' => array(
            'columns'           => 'category_id',
            'refTableClass'     => 'Category',
            'refColumns'        => 'id'
        )
    );
}
```

在取得 Row 之後，可以用下面的方法取得 Category 物件：

```php
// $row->findParentRow($table, [$rule], [$select]);
$row->findParentRow('Category', 'Category');

// Magic function
// $row->findParent<TableClass>([Zend_Db_Table_Select $select])
$row->findParentCategory();

// Magic function
// $row->findParent<TableClass>By<Rule>([Zend_Db_Table_Select $select])
$row->findParentCategoryByCategory();
```

B 資料表（分類資料表）不一定要設定，如果要設定的話，如下：

```php
class Category extends Zend_Db_Table_Abstract
{
    protected $_dependentTables = array('Article');
}
```

在取得 Row 之後，可以用下面的方法取得 Rowset 物件：

```php
// $row->findDependentRowset($table, [$rule], [$select]);
$row->findDependentRowset('Article', 'Category');

// Magic Function
// $row->find<TableClass>()
$row->findArticle();

// Magic Functions
// $row->find<TableClass>By<Rule>()
$row->findArticleByCategory();
```

### Cascading Operations

總共有四種動作：

| Constant | Description |
| -------- | ----------- |
| Zend_Db_Table_Abstract::CASCADE | 關聯的記錄會進行刪除或修改 |
| Zend_Db_Table_Abstract::CASCADE_RECURSE | 與 CASCADE 同，不過會做遞迴確認到最上層的父資料表 |
| Zend_Db_Table_Abstract::RESTRICT | 有存在關聯記錄時，會禁止父資料表刪除或修改 |
| Zend_Db_Table_Abstract::SET_NULL | 把有關聯的記錄行設定成 NULL |
