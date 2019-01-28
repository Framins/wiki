# Controller

zf 指令新增 Controller

    zf create controller name

新增 Action

    zf create action name

## Error

當程式執行遇到錯誤時，可能會期望要輸出找不到網頁之類的頁面，而不是 `500`，這時可以用拋出例外的方式，就能直接導向 `404` 頁面了：

```php
$errorMessage = '404 Page not found';
$errorCode = 404;
throw new Zend_Controller_Action_Exception($errorMessage, $errorCode);
```

導向的網頁會交由 `ErrorController::errorAction()` 處理，Error 類型如下：

|  Type  |  Description  |
|  ----  |  -----------  |
| Zend_Controller_Plugin_ErrorHandler::EXCEPTION_NO_CONTROLLER | 找不到 Controller |
| Zend_Controller_Plugin_ErrorHandler::EXCEPTION_NO_ACTION | 找不到 Action |
| Zend_Controller_Plugin_ErrorHandler::EXCEPTION_NO_ROUTE | 沒有可用的的 Router |
| Zend_Controller_Plugin_ErrorHandler::EXCEPTION_OTHER | 其他 Exception，通常這就算是 500 了 |
