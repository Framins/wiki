# Change log

幾個版本的重大變更：

## 7.1

參考[官方網站](http://php.net/manual/en/migration71.new-features.php)：

### Support for keys in list()

依照官方文件的範例，下面兩個是等價的：

```php
$data = [
    ["id" => 1, "name" => 'Tom'],
    ["id" => 2, "name" => 'Fred'],
];

// list() style
list("id" => $id1, "name" => $name1) = $data[0];

// [] style
["id" => $id1, "name" => $name1] = $data[0];
```

它也可以用在 foreach 上，但不確定 `list()` 是在哪一版開始可以用的：

```php
// list() style
foreach ($data as list("id" => $id, "name" => $name)) {
    // logic here with $id and $name
}

// [] style
foreach ($data as ["id" => $id, "name" => $name]) {
    // logic here with $id and $name
}
```

## 5.6

* [Migration for 5.6](http://php.net/manual/en/migration56.php)

### Variadic functions

定義 function 時，有時參數會有一個或多個，這時可以這樣寫：

```php
function sum(...$numbers) {
    // $numbers is array
    return array_sum($numbers);
}

echo sum(1, 2, 3, 4); // 10
```

> [官網參考](http://php.net/manual/en/functions.arguments.php#functions.variable-arg-list)

### Argument unpacking

傳 function 參數時，可以用 array 定義好，再使用這個運算子展開參數

```php
<?php
function sum($a, $b, $c, $d) {
    return $a + $b + $c + $d;
}

$items = [1, 2, 3, 4];

echo sum(...$items); // 10
echo call_user_func('sum', ...$items); // 10
echo call_user_func_array('sum', $items); // 10
```

下面三個結果是一樣的，不過用新的運算子 `...` 將會比使用 `call_user_func_array()` 快三倍

> [官網參考](http://php.net/manual/en/migration56.new-features.php)

## 5.5

* [Migration for 5.5](http://php.net/manual/en/migration55.php)
* [Generator](http://php.net/manual/en/language.generators.php)

## 5.4

* [Migration for 5.4](http://php.net/manual/en/migration54.php)
* [Trait](http://php.net/manual/en/language.oop5.traits.php)
* Closures support `$this`
* 支援實字陣列表示法，如 `[1, 2, 3, 4]`
* function 回傳陣列的時候，可以直接存取陣列裡的內容，如 `foo()[1]`
* new 完後直接使用，如 `(new foo())->bar();`

## 5.3

* [Migration for 5.3](http://php.net/manual/en/migration53.php)
* [Namespace](http://php.net/manual/en/language.namespaces.php)
* [Anonymous function](http://php.net/manual/en/functions.anonymous.php)
* Magic function: `__callStatic()` `__invoke()`
