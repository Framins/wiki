# PHP 7

新特性筆記

## Type Declarations

Function 參數類型在 PHP 5.6 之前，都只能定義類別名或 array。在 PHP 7 開始，可以定義標準類別，如 int / string 等等。

```php
class Foo
{
    public function setNumber(int $number)
    {
        echo $number;
    }
}
```

> 詳細可參考[官網說明](http://php.net/manual/en/functions.arguments.php#functions.arguments.type-declaration)

## Return Type Declarations

同樣的，回傳也可以定義 type 了

```php
class Foo
{
    public function setNumber(int $number): array
    {
        return range(1, $number);
    }
}
```

> 詳細可參考[官網 WIKI 說明](https://wiki.php.net/rfc/return_types)

## Null Coalesce Operator

這蠻類似三元運算的，下面的意思是 如果 `$_GET['user']` 不存在的話，就回傳 `nobody`

```php
$username = $_GET['user'] ?? 'nobody';
```

> 詳細可參考[官網 WIKI 說明](https://wiki.php.net/rfc/isset_ternary)

## Combined Comparison Operator

還有另一個稱呼叫 *Spaceship Operator*，這是用來比較兩邊的值，來回傳三種狀態：

* `0` 相等
* `-1` 小於
* `1` 大於

Example:

```php
// integer
echo 1 <=> 1; // 0
echo 1 <=> 2; // -1
echo 2 <=> 1; // 1

// float
echo 1.5 <=> 1.5; // 0
echo 1.5 <=> 2.5; // -1
echo 2.5 <=> 1.5; // 1

// string
echo "a" <=> "a"; // 0
echo "a" <=> "b"; // -1
echo "b" <=> "a"; // 1
```
