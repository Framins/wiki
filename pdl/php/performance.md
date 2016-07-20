# Performance

參考網頁

* http://www.phpbench.com/
* http://blog.sina.com.tw/jiing/article.php?entryid=578626

## array_push?

為一個陣列 `$array` 新增一個元素時，下面兩種方法的結果是相同的：

```php
array_push($array, $item);
```

```php
$array[] = $item;
```

後者的寫法，效能會比前者的好，因為少了一層 function call stack.

除非是新增兩個元素以上才會有使用此函數的必要。

## echo

下面兩個執行結果會是一樣的：

```php
echo $item . ' is Item ' . $number;
```

```php
echo $item , ' is Item ' , $number;
```

後者的寫法，效能會比前者好，因為少了 `.` 運算。
