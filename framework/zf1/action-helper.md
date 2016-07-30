Action Helper
=============

[Action Helpers](http://framework.zend.com/manual/1.12/en/zend.controller.actionhelpers.html) 是給 controller 重複使用的 function

## Initial

Action Helper 是透過 `Zend_Controller_Action_HelperBroker` 作管理的。

#### 註冊helper

```php
Zend_Controller_Action_HelperBroker::addHelper($helper);
```

#### 判斷helper是否新增

```php
Zend_Controller_Action_HelperBroker::hasHelper('name');
```

#### 移除helper

```php
Zend_Controller_Action_HelperBroker::removeHelper('name');
```

#### 註冊helper的前綴

```php
Zend_Controller_Action_HelperBroker::addPrefix('My_Action_Helpers');
```

#### 註冊helper的引用目錄

使用引用目錄可以更方便的增加helper

```php
Zend_Controller_Action_HelperBroker::addPath(APPLICATION_PATH . '/controllers/helpers');
```

## Custom Helpers

要寫自定義的 helper 就必須要繼承 `Zend_Controller_Action_Helper_Abstract` ，裡面有提供一些方法可以直接取得系統相關資訊

|  Method Name  |  Description  |
|  -----------  |  -----------  |
| setActionController(Zend_Controller_Action $actionController) | 設定 Action Controller |
| getActionController() | 取得 Action Controller |
| getFrontController() | 取得 Front Controller |
| init() | 當 Action 初始化的時候會執行，可用繼承修改 |
| preDispatch() | 當 helper 被加入前會執行，可用繼承修改 |
| postDispatch() | 當 helper 被加入後會執行，可用繼承修改 |
| getRequest() | 取得 Action Controller 的 request 物件 |
| getResponse() | 取得 Action Controller 的 response 物件 |
| getName() | 取得 helper 的名稱 |
