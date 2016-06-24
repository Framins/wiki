# PHP 7

新特性筆記

## Function Argument Type Definition

Function 參數類型在 PHP 5.6 之前，都只能定義類別名或 array 。在 PHP 7 開始，可以定義標準類別，如 int / string 等等。

```php
class Foo
{
    public function setNumber(int $number)
    {
        echo $number;
    }
}
```
