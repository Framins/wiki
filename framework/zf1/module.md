# Module

* [module-structure](module-structure.md)

## FAQ

* http://stackoverflow.com/questions/1836447/zend-modules-models

當建立 model 後，無法 autoload 時...

```php
<?php

class ModuleName_Model_ModelName
{
}
```

```php
$model = new ModuleName_Model_ModelName();
```

## application.ini

```ini
; 注冊 module
resources.modules[] = "default"
resources.modules[] = "News"

; 設定 module 主目錄，這樣可以透過 zend 的 autoload 找
resources.frontController.moduleDirectory = APPLICATION_PATH "/modules"

; 設定預設 module
resources.frontController.defaultModule = "News"
```

如果有定義 module 的話，可以為個別的 module 做設定，比方說現在有個 `blog` module ：

```ini
blog.resources.db.adapter = "pdo_mysql"
blog.resources.db.params.host = "localhost"
blog.resources.db.params.username = "username"
blog.resources.db.params.password = "password"
blog.resources.db.params.dbname = "dbname"
```

References
----------

* http://www.fanli7.net/a/bianchengyuyan/PHP/20130909/379297.html
* http://framework.zend.com/manual/1.12/en/zend.controller.modular.html
* http://framework.zend.com/manual/1.10/en/zend.application.available-resources.html#zend.application.available-resources.modules
* http://blog.lenss.nl/2010/02/zend-framework-bootstrapping-modules/
* http://cnn237111.blog.51cto.com/2359144/1290458
* http://hcj671223.blogspot.tw/2012/08/zend-framework-modules.html
* http://vandenbos.org/zend-framework-module-specific-layout/
