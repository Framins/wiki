# Magic Method

一般 PHP 的教學書都會這麼建議：

* public method的名稱直接打，如 `public function getData() {}`
* private 或 protected method的名稱前面加一個底線，如 `protected function _getData() {}`
* 另外最好不要用兩個底線開頭，如 `private function __getData() {}`

其實是因為 PHP 把所謂的 Magic Method 名稱都是設定為兩個底線開頭的。 Magic Method 正如其名，用起來會讓開發者覺得很 Magic ，活用它的特性還能讓其他開發者覺得 Amazing ！

PHP 其實已經有預設好幾個名稱，開發者其實也只要了解什麼時候會去調用它就行了。

## `__construct()`

    void __construct ([ mixed $args [, $... ]] )

這是 PHP 開發者最常使用的 Magic Method 了，這個 method 被 call 的時機是在建構的時候：

```php
$obj = new ClassName(); 
```

在 new 的同時， `ClassName::__construct()` 就會先執行了。通常這個 Magic Method 都是用在物件初始化。而方法後面所設定的參數要在 new 的後面傳入，如：

```php
class ClassName {
    public __construct ($data, $default = true){}
}

$obj = new ClassName($data);
```

另外， `__construct` 的能見度如果是 public 的話，代表這是可以被外部實例化的類別；相反的，如果是 `private` 或 `protected` 的話，就不能被外部實例化，但可以從內部的靜態方法裡實作實例化的方法。

## `__destruct()`

    void __destruct ( void )

這個就比較不常見了，它在解構的時候會執行，除了程式結束外，就是 unset 的時候了：

    unset($obj);

通常是用在程式收尾，如資料庫斷線等。

## `__call()`

    public mixed __call ( string $name , array $arguments )

這個就比較神奇了！

今天宣告一個 class 如下：

```php
class ClassName {
    public __call ($name, $arg) {
        echo 'No ' . $name . ' Method.';
    }
}
```

當我實例化並呼叫不存在方法(或非公開方法)時，就會呼叫 `__call` 方法了：

```php
$obj = new ClassName();
$obj->getData() // Output: "No getData Method."
```

參考下面程式碼

```php
class User {
    public findUser($condition) {
        // Get user data by condition.
        return $data;
    }

    public __call ($name, $arg) {
        if (strpos('findUserBy', $name) == 0) {
            $condition = strtolower(substr($name, 10));
            return findUser($condition);
        }
    }
}

$obj = new User();
$userdata = $obj->findUser('id');
$userdata = $obj->findUserById();
```

後面兩個寫法的結果會是一樣的，所以代表可以有理論無限多個 Method 。只是 Exception 要做好才不會有問題產生。

## `__callStatic()`

    public static mixed __callStatic ( string $name , array $arguments )

原理跟 `__call()` 一樣，不過是 static 的。

## `__get()`

    public mixed __get ( string $name )

與 `__call()` 很像，不過這是當要取得未定義或非公開的屬性時會呼叫的方法。如：

    $data = $obj->data;  // $obj->data  is not define / not public.

以上例來說， `$name` 的值為 ''data'' 。

## `__set()`

  public void __set ( string $name , mixed $value )

同 `__get()` ，設值一個未定義或非公開屬性時會呼叫的方法。

  $obj->data = 'John';  // $obj->data  is not define / not public.

以上例來說， `$name` 的值為 `data` ， `$value` 的值為 `John` 。

## `__isset()`

    public bool __isset ( string $name )

當對未定義或非公開屬性使用 `isset()` 或 `empty()` 時，會被呼叫。

    isset($obj->data);

## `__unset()`

    public void __unset ( string $name )

當對未定義或非公開屬性使用 `unset()` 時會被呼叫。

    unset($obj->data);

## `__toString()`

    public string __toString ( void )

當想要把物件當作一個 string 時，就會呼叫這個 Magic Method 並回傳一個值，如：

```php
class User
{
    public function __toString()
    {
        echo 'User';
    }
}

$obj = new User();
echo $obj; // Output: User
```

比較實際的應用如： JSON 物件處理完成後，要輸出時，就可以直接把物件當作字串輸出即可。

## `__invoke()`

    mixed __invoke ([ $... ] )

當想要把物件當作一個 function 呼叫時，就會呼叫這個 Magic Method ，如(官方範例)：

```php
class CallableClass 
{
    function __invoke($x) {
        var_dump($x);
    }
}

$obj = new CallableClass();
$obj(5);

var_dump(is_callable($obj));
```

## Reference

* [PHP: Magic Methods](http://www.php.net/manual/en/language.oop5.magic.php)
* [Magic Benchmarkd](http://www.garfieldtech.com/blog/magic-benchmarks)
