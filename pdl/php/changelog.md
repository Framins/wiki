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

參考 [5.6 版的改變](5.6.md)

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
