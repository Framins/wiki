# How to

## String

#### Build HTTP query string

其實 php 有原生內建函數 [http_build_query](http://php.net/manual/en/function.http-build-query.php) (PHP 5+)

原本可能會這樣寫：

```php
$params = `;
$split = '&';
$count = count($result);
$index = 0;
foreach ($result as $key => $value) {
    if ($count - 1 == $index) {
        $split = `;
    }
    $params = $params . $key . '=' . $value . $split;
    $index++;
}
```

使用 `http_build_query` ：

```php
$params = http_build_query($result);
```

> `http_build_query` 會做 URL-encoded ，所以相對的，傳入的值必須要是 raw data

#### Parse HTTP query string

相反的，解析 HTTP query 可以用 [parse_str](http://php.net/manual/en/function.parse-str.php) (PHP 4+)

```php
$str = 'foo=bar&test=ing';
$params = parse_str($str, $output);
$output['foo'];   // bar
$output['test'];  // ing
```

## Array

Array 操作

#### Array 找 key

[array_key_exists()](http://tw1.php.net/manual/en/function.array-key-exists.php)

return bool

#### Array 找 value

[array_search()](http://tw1.php.net/manual/en/function.array-search.php)

return key

#### 取得所有 key

[array_keys()](http://tw1.php.net/manual/en/function.array-keys.php)

return array(keys);

#### 取得所有 value

[array_values()](http://tw1.php.net/manual/en/function.array-values.php)

return array(values);

#### 取得 array 的交集 by key

[array_intersect_key()](http://tw1.php.net/manual/en/function.array-intersect-key.php)

#### 取得 array 的交集 by value

[array_intersect()](http://tw1.php.net/manual/en/function.array-intersect.php)

#### 取得 array 間的差集 by key-value

[array_intersect_assoc()](http://tw1.php.net/manual/en/function.array-intersect-assoc.php)

#### 取得 array 間的差集 by key

[array_diff_key()](http://tw1.php.net/manual/en/function.array-diff-key.php)

arg1 - arg2

#### 取得 array 間的差集 by value

[array_diff()](http://tw1.php.net/manual/en/function.array-diff.php)

arg1 - arg2

#### 取得 array 間的差集 by key-value

[array_diff_assoc()](http://tw1.php.net/manual/en/function.array-diff-assoc.php)

arg1 - arg2

## Sorting Arrays

http://php.net/manual/en/array.sorting.php
