# Zend_Paginator

如果使用 Zend Framework 而且有產生分頁與對應資料的需求時，請參考 `Zend_Paginator`

## Data Source

Zend_Paginator 是使用 adapter pattern 來實作原始資料與輸出資料的轉換

內建以下幾種 adapter ：

|  Adapter  |  Description  |
|  -------  |  -----------  |
| Zend_Paginator_Adapter_Array | 使用 PHP 原生 array 作為資料來源 |
| Zend_Paginator_Adapter_DbSelect | 使用 Zend_Db_Select 物件作為資料來源，它會回傳 array |
| Zend_Paginator_Adapter_DbTableSelect | 使用 Zend_Db_Table_Select 物件作為資料來源，它會回傳 Zend_Db_Table_Rowset_Abstract 物件 |
| Zend_Paginator_Adapter_Iterator | 使用 Iterator 作為資料來源 |
| Zend_Paginator_Adapter_Null | 不使用 Zend_Paginator 來管理資料與分頁的關係，但還是可以控制分頁輸出的功能 |

## Construct

基本建立物件的方法，建構的時候同時傳入 adapter ：

```php
$paginator = new Zend_Paginator(new Zend_Paginator_Adapter_Array($array));
```

Zend_Paginator 另外還提供了一個工廠方法給懶人用的 ：

```php
$paginator = Zend_Paginator::factory($data);
```

Trace 過 source code，它會先確認 `$data` 的格式是否有跟內建的 adatper 相符，然後再去 new 對應的物件。

如果轉換的方法不單純的話，也可以選擇自己實作 `Zend_Paginator_Adapter_Interface`。自己建立的實作除了要使用第二個參數讓 factory 知道外，還必須要先用它提供的靜態方法增加載入的路徑，讓 `Zend_Loader` 知道要去哪裡載入：

```php
Zend_Paginator::addAdapterPrefixPath('path/to/adapter');
$paginator = Zend_Paginator::factory($data, 'MyAdapter');
```

`Zend_Paginator::factory()` 第一個參數，也可以傳 `Zend_Paginator_AdapterAggregate` 的實作，意思就是原始資料的物件只要有實作 `Zend_Paginator_AdapterAggregate`，那這物件就可以視同有分頁功能。好處是，這樣取得 paginator 的方法就能抽象到原始資料物件本身。
