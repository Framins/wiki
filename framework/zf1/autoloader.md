Autoloader
==========

Zend 的自動載入機制蠻複雜的，不過也因此具備了強大的修改彈性和空間，可以做出多樣化的設計。

Namespace
---------

Zend 可以用 Zend 的套件，是因為它預設就有一個 `Zend_` 的命名空間，如果想要使用其他 library 的話，就必須跟 Autoloader 說一聲，你也有自己的命名空間想註冊：

註冊方法很簡單，直接在 `application.ini` 裡加一行：

```
Autoloadernamespaces[] = "Test"
```

這樣就可以在 `library/Test` 下，放自己的 library 了，比方說：

```php
$news = new Test_News();
```

Resource Autoloader
-------------------

資源指的是 Model 、 Form ....等，它的路徑和類別名跟上面提到的是使用不同的規則

因為這些資源是跟 Application 有關，所以一開始的命名空間也是跟 Application name 綁在一起的， Application name 也可以直接在 `application.ini` 做修改：

```
appnamespace = "MyApp"
```

`Zend_Application_Module_Autoloader` 裡面的資源，預設定義好的路徑：

|  Resource Name  |  Path  |
|  -------------  |  ----  |
| Model_DbTable | models/DbTable |
| Model_Mapper | models/mappers |
| Form | forms |
| Model | models |
| Plugin | plugins |
| Service | services |
| View_Helper | views/helpers |
| View_Filter | views/filters |

Reference
---------

* [The Autoloader](http://framework.zend.com/manual/1.12/en/zend.loader.autoloader.html)
* [Resource Autoloaders](http://framework.zend.com/manual/1.12/en/zend.loader.autoloader-resource.html)
* [Zend Framework v1 Autoloader](http://blog.johnsonlu.org/zfzend-framework-v1-autoloader/)
