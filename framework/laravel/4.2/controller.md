# Controller

[官方說明](http://kejyun.github.io/Laravel-4-Documentation-Traditional-Chinese/docs/controllers/)

Controller 的目錄放在 `app/controllers` 裡，在 `composer.json` 裡有定義。

官方範例：

```php
class BlogController extends BaseController {

    public function showProfile($id)
    {
        $user = User::find($id);
        return View::make('user.profile', array('user' => $user));
    }

}
```

Controller 必須繼承 `BaseController` ， 而 `BaseController` 裡面可以放所有 Controller 共用的邏輯。

## Resource Controller

使用指令建立：

    php artisan controller:make BlogController
