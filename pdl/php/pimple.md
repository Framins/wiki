# Pimple

[Pimple][] 是個實作 IoC 的 PHP 套件，它的特色就是非常簡單

使用 [Composer](composer.md) 安裝

    composer require pimple/pimple

## Example

初始化

```php
$container = new Pimple\Container();
```

儲存變數

```php
$container['logger_driver'] = 'monolog';
```

單例模式 (每次取物件都會是同一個物件)

```php
use Monolog\Logger;

$container['logger'] = function($container) {
    $log = new Logger('default');
    return $log;
};

// 取物件並執行
$container['logger']->info('Hello world');
```

工廠模式 (每次取物件都會是新產生的物件)

```php
use Monolog\Logger;

$container['logger'] = $container->factory(function($container) {
    $log = new Logger('default');
    return $log;
});
```

如果想要把 container 當作是 application 的參數時，建議用 protect + anonymous function。平常使用 ArrayAccess 設定的值，是有機會被覆蓋的。用這個方法可以避免被覆蓋。

Note: 看原始碼的感覺是這樣用的...

```php
$container['db_settings'] = $container->protect(function () {
    return [
        'db_host' => '127.0.0.1',
        'db_name' => 'default',
        'db_user' => 'root',
        'db_pass' => 'password',
    ];
});

var_dump($container['db_settings']);
```

Service Provider

```php
class DbSettingProvider implements Pimple\ServiceProviderInterface
{
    public function register(Pimple\Container $container)
    {
        $container['db_settings'] = $container->protect(function () {
            return [
                'db_host' => '127.0.0.1',
                'db_name' => 'default',
                'db_user' => 'root',
                'db_pass' => 'password',
            ];
        });
    }
}
$container->register(new DbSettingProvider());

var_dump($container['db_settings']);
```

[Pimple]: http://pimple.sensiolabs.org/
