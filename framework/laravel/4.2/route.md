# Route

[官方說明](http://laravel.tw/docs/routing)

Route 是一條一條的規則，規則裡定義了一個路由可以接受的動作和需要的參數等。

它會由上往下一條一條比對，如果有符合就會執行，如果全部比對過了，還是沒有符合的，那就會是 `404 Not Found` 了

它可以搭配 `group` `prefix` `namespace` `sub-domain` 做彈性設計。

如果邏輯複雜的話，也可以轉向給 Controller 整合處理。

## Basic

Router 可以定義 http method 對應一個處理的方法：

```php
// 當 GET 時
Route::get('/', function(){});

// 當 POST 時
Route::post('/', function(){});

// 當 PUT 時
Route::put('/', function(){});

// 當 DELETE 時
Route::delete('/', function(){});

// 註冊多個動作
Route::match(array('GET', 'POST'), '/', function(){});

// 經過 HTTPS 加密時
Route::get('/', array('https', function(){}));     
```

可用 `URL::to` 來產生網址，指向定義的 route ：

```php
$url = URL::to('foo');
```

如果想在 URL 裡抓參數

```php
Route::get(('user/{id}', function($id) {
    return 'User '.$id;
});
```

Optional 參數，在後面加個 `?`

```php
Route::get(('user/{name?}', function($name = null) {
    return $name;
});
```

Optional + 預設值

```php
Route::get(('user/{name?}', function($name = 'Miles') {
    return $name;
});
```

使用 Regex

```php
Route::get(('user/{name?}', function($name = null) {
    return $name;
})
->where('name', '[A-Za-z]+');
```

如果有常用的正規標示式，可以用 `pattern` ：

```php
Route::pattern('id', '[0-9]+');

Route::get('user/{id}', function($id)
{
    // Only called if {id} is numeric.
});
```

## Resource Controller

資源控制器可以建立跟資源相關的 RESTful 控制器，如 `article` 資源，預設有下列 7 個方法：

|  HTTP Method  |  Path  |  Action  |  Route Name  |
| GET | /article | index | resouce.index |
| GET | /article/create | create | resouce.create |
| POST | /article | store | resouce.store |
| GET | /article/{id} | show | resouce.show |
| GET | /article/{id}/edit | edit | resouce.edit |
| PUT/PATCH | /article | update | resouce.update |
| DELETE | /article/{id} | destroy | resouce.destroy |

在 route 只要這樣設定就全都有了

```php
Route::resource('article', 'ArticleController');
```

## Route Filter

它可以對路由做限制訪問，如果要做認證的時候會很好用

Laravel 裡面包含的 Filter ： `auth` `auth.basic` `guest` `csrf`

## Check

可以使用 artisan 指令來檢查目前路由設定的狀況，比方說 route 的定義如下：

```php
Route::get('/', function()
{
    return View::make('hello');
});

Route::get('/users', 'UserController@getIndex');

Route::group(array('domain' => '{user}.framins.com'), function()
{
    Route::controller('users', 'Framins\UserController');
});
```

使用檢查指令 `php artisan routes` 的結果如下：

    $ php artisan routes
    +--------------------+-------------------------------------------------------------+------+--------------------------------------+----------------+---------------+
    | Domain             | URI                                                         | Name | Action                               | Before Filters | After Filters |
    +--------------------+-------------------------------------------------------------+------+--------------------------------------+----------------+---------------+
    |                    | GET|HEAD /                                                  |      | Closure                              |                |               |
    |                    | GET|HEAD users                                              |      | UserController@getIndex              |                |               |
    | {user}.framins.com | GET|HEAD users/index/{one?}/{two?}/{three?}/{four?}/{five?} |      | Framins\UserController@getIndex      |                |               |
    | {user}.framins.com | GET|HEAD users                                              |      | Framins\UserController@getIndex      |                |               |
    | {user}.framins.com | GET|HEAD|POST|PUT|PATCH|DELETE users/{_missing}             |      | Framins\UserController@missingMethod |                |               |
    +--------------------+-------------------------------------------------------------+------+--------------------------------------+----------------+---------------+

Artisan 這個功能列出來的內容還蠻清楚的，也會提醒哪些沒實作的會對應到哪一個 method ，超棒的。
