# Plugin

## Start

Plugin 需要繼承 `Zend_Controller_Plugin_Abstract` ，跟一般所知的 plugin 一樣，都是用觀察者模式實作。官方有提供 Example 如下：

```php
class Application_Plugin_Test extends Zend_Controller_Plugin_Abstract
{
    /**
     * 在 FrontController 開始要分析 request 並送到 router 之前執行
     */
    public function routeStartup(Zend_Controller_Request_Abstract $request)
    {
        $this->getResponse()
             ->appendBody("<p>routeStartup() called</p>\n");
    }

    /**
     * 在 FrontController 分析完 router 之後執行
     */
    public function routeShutdown(Zend_Controller_Request_Abstract $request)
    {
        $this->getResponse()
             ->appendBody("<p>routeShutdown() called</p>\n");
    }

    /**
     * 在 FrontController 開始進入分派迴圈之前執行
     */
    public function dispatchLoopStartup(
        Zend_Controller_Request_Abstract $request)
    {
        $this->getResponse()
             ->appendBody("<p>dispatchLoopStartup() called</p>\n");
    }

    /**
     * 在 FrontController 分派 action 之前執行
     */
    public function preDispatch(Zend_Controller_Request_Abstract $request)
    {
        $this->getResponse()
             ->appendBody("<p>preDispatch() called</p>\n");
    }

    /**
     * 在 FrontController 分派 action 之後執行
     */
    public function postDispatch(Zend_Controller_Request_Abstract $request)
    {
        $this->getResponse()
             ->appendBody("<p>postDispatch() called</p>\n");
    }


    /**
     * 在 FrontController 離開分派迴圈之後執行
     */
    public function dispatchLoopShutdown()
    {
        $this->getResponse()
             ->appendBody("<p>dispatchLoopShutdown() called</p>\n");
    }
}
```

> Zend Framework 有預設 plugin 放的位置，可參考 [Resource Autoloader](autoloader#resource-autoloader)

再來就是要註冊 plugin ，用程式碼註冊的方法：

```php
$front = Zend_Controller_Front::getInstance();
$front->registerPlugin(new Application_Plugin_Test());
```

用 `application.ini` 註冊的方法：

```ini
resources.frontController.plugins[] = Application_Plugin_Test
```

## Reference

* [官方說明](http://framework.zend.com/manual/1.12/en/zend.controller.plugins.html)
