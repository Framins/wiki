# [Silex](http://silex.sensiolabs.org/)

`PHP` [`Micro Framework`](/term/micro-framework.md)

跟 [Slim](/framework/slim/README.md) 一樣，是個簡單好用的 Micro Framework 。不一樣的是， Slim 是一個獨立的套件，而 Silex 使用 [Symfony](/framework/symfony/README.md) 的幾個特定元件實作出來的。

簡單 Hello World 如下：

```php
use Symfony\Component\HttpFoundation\Request;
use Symfony\Component\HttpFoundation\Response;

require_once __DIR__ . '/../vendor/autoload.php';

$app = new Silex\Application();
$app['debug'] = true;

$app->get('/', function (Request $request) use ($app) {
    return new Response('Hello World!!', 200);
});

$app->run();
```

Silex 比較好用的點是，它已經有跟很多套件先做好整合了，只要 composer require 和加 Provider 即可，如要使用 Twig ：

```
$ composer require twig/twig
```

然後程式要註冊

```php
$app->register(new Silex\Provider\TwigServiceProvider(), [
    'twig.path' => __DIR__ . '/../views',
]);
```

`index.twig` 長這樣

```twig
{{ hello }}
```

接著使用（需參考官方說明文件）

```php
$app->get('/', function (Request $request) use ($app) {
    return $app['twig']->render('index.twig', array(
        'hello' => 'Hellow World',
    ));
});
```
