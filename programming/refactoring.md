# Refactoring

Refactoring 不會修正錯誤，也不會改變外部行為，它的核心價值在於：增加程式碼的可讀性或改變結構與設計，讓未來除錯或加入新功能會更容易。

誰能保證下次看到程式碼的 programmer 可以馬上進入狀況，並立即開始除錯或加入新功能呢？

以下為 Refactoring 經常會用到的技巧：

* Comment - 最基本的，為原始碼加上註解。
* Rename - 縮寫、簡寫或是錯字，改成有意義或有規則的名稱，比瞎猜來的好太多了。
* Guard Clauses / Nested Structure
* EAFP / LBYL

## Example 1

Before

```php
class Example
{
    const _PRECENT = 100;

    public static function getPercent()
    {
        return self::_PRECENT;
    }
}
```

After

```php
class Example
{
    const PERCENT = 100;
}
```

### Reason

* 錯字(PRECENT)，在動態語言裡，常常會造成拼寫正確卻呼叫錯誤、然後無限鬼打牆、最後罵那個拼錯單字的人等無意義的事。
* PHP 裡，如果確定要宣告常數，而且單純只是拿來取用的話，那用 static function 只是多一層無意義的呼叫而已。這部分需要查原本的程式碼對此常數有沒有其他相關公開的用途，如果沒有的話，確實就會比較沒有意義了。
* PHP 在常數宣告上，底線是完全無意義 (變數因為有 visibility 的差別，通常有底線會是 private 或 protected )

## Example 2

Before

```php
// with Zend Framework: Zend_Controller_Action
$helper = $this->_helper->bet;
```

After

```php
//  with Zend Framework: Zend_Controller_Action
$helper = $this->getHelper('bet');
```

### Reason

* 只要哪天 `Zend_Controller_Action` 的 _helper 能見度改成 private 或是 _helper 的內容改變，所有的 Controller 都會中槍。雖然是不大可能發生，但使用 getHelper() 方法會發生這個問題的機率會更小。
* 語意上比較清楚易懂。

## Example 3

Before

```php
// with Zend Framework
class Model_DbTable_Example extends Zend_Db_Table_Abstract
{
    protected $_name = 'table_name';
	
    public function __construct($tableName = null)
    {
        if ($tableName != null)
        {
            $this->setTableName($tableName);
        }
        parent::__construct();
    }

    public function setTableName($tableName)
    {
        $this->_name = $tableName;
    }
}
```

After

```php
// with Zend Framework
class Model_DbTable_Example extends Zend_Db_Table_Abstract
{
    /**
     * 初始化資料表設定
     */
    public function __construct()
    {
        $config = array(
            Zend_Db_Table_Abstract::NAME => 'table_name'
        );
        parent::__construct($config);
    }
}
```

### Reason

* 請多參考官方文件與多利用官方的API

## References

* http://www.ewdna.com/2009/01/java-coding-stylecode-conventions.html
* http://ihower.tw/blog/archives/1960
