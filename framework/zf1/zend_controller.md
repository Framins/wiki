# Zend_Controller

* [Zend Controller 官方文件](http://framework.zend.com/manual/1.12/en/zend.controller.html)

## The Request Object

原本 PHP 的 request 都是使用全域變數做存取，但在用 Framework 時，都會建議使用 Framework 提供的 function 來讀取。

主要會使用的就是 [Zend_Controller_Request_Http](http://framework.zend.com/apidoc/1.12/files/Controller.Request.Http.html) 了，在 Action Controller 裡，可以使用 `%%$this->getRequest()%%` 取得。

取消 layout

```php
$this->getHelper('layout')->disableLayout();
```

取消 view render

```php
$this->getHelper('viewRenderer')->setNoRender();
```
