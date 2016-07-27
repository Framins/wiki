# Router

Router 的作用就很像 URL rewrite ，依不同的 URL 去指向不同的檔案。

## Start

Router 可以打在 `Bootstrap.php` 裡:

```php
function _initRoutes() {
    $frontController = Zend_Controller_Front::getInstance();
    $router = $frontController->getRouter();

    // Do something
}
```

## Default Routes

```php
// Assuming the following:
$front->setControllerDirectory(
    array(
        'default' => '/path/to/default/controllers',
        'news'    => '/path/to/news/controllers',
        'blog'    => '/path/to/blog/controllers'
    )
);
```

結果：

```
Module only:
http://example/news
    module == news

Invalid module maps to controller name:
http://example/foo
    controller == foo

Module + controller:
http://example/blog/archive
    module     == blog
    controller == archive

Module + controller + action:
http://example/blog/archive/list
    module     == blog
    controller == archive
    action     == list

Module + controller + action + params:
http://example/blog/archive/list/sort/alpha/date/desc
    module     == blog
    controller == archive
    action     == list
    sort       == alpha
    date       == desc
```

References
----------

* http://framework.zend.com/manual/1.12/en/zend.controller.router.html
* http://stackoverflow.com/questions/1340467/adding-sub-domain-based-routes-in-zend-framework
* http://rakesh.sankar-b.com/2010/09/16/zend-frameworkroute-url-by-hostname/
