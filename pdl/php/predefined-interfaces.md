Predefined Interfaces
=====================

預定義的介面可以讓物件擁有如同變數一樣的性質，如：把物件當作陣列使用、物件能夠疊代等。

即然是介面，就會有必需實作的方法。使用上只要 implements 想用的介面後，再依需求實作方法即可。

Traversable
-----------

單純只是一個父介面，讓可以疊代的其他介面來繼承它。

實際上並不會去實作它，但是相對的倒是可以用 `instanceof` 來知道物件是否能夠被疊代。

Prototype

```php
Traversable {
}
```

Iterator
--------

繼承這個介面的物件，可以用 foreach 來進行疊代。

Prototype

```php
Iterator extends Traversable {
    abstract public mixed current ( void )
    abstract public scalar key ( void )
    abstract public void next ( void )
    abstract public void rewind ( void )
    abstract public boolean valid ( void )
}
```

其中裡面每個方法代表的含意為：

* *current* - 返回目前的元素
* *key* - 返回目前的索引
* *next* - 指標向前移動一個元素
* *rewind* - 指標返回到疊代器的第一個元素
* *valid* - 檢查位置是否有效

平常使用 foreach 可以會像下面這樣：

```php
$iterator = new myIterator();

foreach ($iterator as $key => $value) {
    echo $key, $value;
}
```

如果常用 foreach 的話，其實是可以預期的到它的執行步驟的：

1. 執行 `rewind()` ，讓指標可以從頭開始取資料。
2. 執行 `valid()` ，確定指標指向的位置是有資料的。
3. 再來執行 `$value = current()` 和$ `key = key()` ， 把取到的值代入 foreach 語法所設定的變數裡。
4. 當下一個 loop 開始時，換執行 `next()` ，其他 `valid()` 、 `current()` 、 `key()` 都同上。
5. 迴圈結束條件為當 `valid()` 回傳 false 。

IteratorAggregate
-----------------

看了官方文件，跟 Iterator 的結果好像沒什麼差別。

Prototype

```php
IteratorAggregate extends Traversable {
    abstract public Traversable getIterator ( void )
}
```

只要你回傳的是 Traversable 的物件就可以了，而這個物件需要自己動手做。

官方使用 ArrayIterator 來實現，其中 ArrayIterator 有實作到 Iterator ，所以是符合條件的。

ArrayAccess
-----------

實作這介面之後，可以讓物件多了像陣列一樣的存取方式。

```php
ArrayAccess {
    abstract public boolean offsetExists ( mixed $offset )
    abstract public mixed offsetGet ( mixed $offset )
    abstract public void offsetSet ( mixed $offset , mixed $value )
    abstract public void offsetUnset ( mixed $offset )
}
```

方法說明：

* *offsetExists* - 檢查指標所指向的位置有沒有存在
* *offsetGet* - 取得該指標的值
* *offsetSet* - 設定該指標的值
* *offsetUnset* - 刪除該指標的值

Reference
---------

* [[http://www.php.net/manual/en/reserved.interfaces.php|PHP: Predefined Interfaces]]
* [[http://www.php.net/manual/en/class.arrayaccess.php|PHP: ArrayIterator]]
* [[http://www.php.net/manual/en/language.oop5.iterations.php|PHP: Object Iteration]]
