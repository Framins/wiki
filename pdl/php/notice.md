# Notice

## in_array 比對規則

in_array 在比對的時候，只要不給第三個參數的話，就會做隱性轉型。但 **轉型會以 needle 為標準**，而把 haystack 裡的元素做轉型。

因此參考下列程式碼：

```php
$needle1 = 0;
$needle2 = '0';
$haystack = array('ABC', 'DEF');

$inArray1 = in_array($needle1, $haystack);   // true
$inArray2 = in_array($needle2, $haystack);   // false
```

## strtr() 與 str_replace() 的差異

參考 https://stackoverflow.com/questions/8177296/when-to-use-strtr-vs-str-replace
