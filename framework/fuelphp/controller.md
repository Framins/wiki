Controller
==========

預設目錄

    fuel/app/classes/controller

在定義 Controller 名稱的時候，需要加上 `Controller_` 前綴；而 Action 的名稱則是要用 `action_` 前綴，如官網上的範例：

```php
class Controller_Example extends Controller
{
    public function action_index()
    {
        $data['css'] = Asset::css(array('reset.css','960.css','main.css'));
        return Response::forge(View::forge('welcome/index'));
    }
}
```

另外，也可以針對不同的 http method 呼叫不同的 method，如官網上的範例：

```php
class Controller_Example extends Controller
{
    public function get_index()
    {
        // 當 HTTP 方法是 GET 時將被呼叫。
    }

    public function post_index()
    {
        // 當 HTTP 方法是 POST 時將被呼叫。
    }
}
```
