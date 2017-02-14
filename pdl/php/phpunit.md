PHPUnit
=======

* [官方操作手冊](http://phpunit.de/manual/current/en/index.html)
* mock-object - PHPUnit 產生模擬物件的方法。
* assert - PHPUnit 提供的斷言 (assert) 方法。
* https://gist.github.com/loonies/1255249
* SeleniumTestCase

Installation
------------

安裝方式：

* [PEAR](http://phpunit.de/manual/current/en/installation.html#installation.phar)
* [Composer](http://phpunit.de/manual/current/en/installation.html#installation.composer)

PEAR
----

```bash
pear channel-discover pear.phpunit.de
pear channel-discover pear.symfony.com # 安裝 4.0 就不需要這個 channel 了
pear install --alldeps phpunit/PHPUnit-3.7.8
```

如果有要裝 SkeletonGenerator 的話：

```bash
pear channel-discover components.ez.no
pear install --alldeps phpunit/PHPUnit_SkeletonGenerator
```

[MAC + Zend Server 可能會有的問題](http://forums.zend.com/viewtopic.php?f=8&t=111083)

找到 phpunit script ，最上面這段

```
#!/usr/local/zend/bin/php
```

改成這段

```
#!/usr/bin/env /usr/local/zend/bin/php
```

phpunit 和 phpunit-skeleton 都通用

Composer
--------

在 `composer.json` 加入下面內容

```javascript
{
    "require-dev": {
        "phpunit/phpunit": "4.1.*"
    }
}
```

官方也有提到有其他可選套件，都是加入 `require-dev` 裡的：

* `phpunit/php-invoker`
* `phpunit/dbunit`
* `phpunit/phpunit-selenium`

Codeception
-----------

基於 PHPUnit 的 BDD framework

* Acceptance Testing
* Functional Testing
* API Testing
* Unit Test

### Example

* [Example for Laravel 4](https://github.com/Codeception/sample-l4-app)
