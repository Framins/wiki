# PHP

很多工具都能在 [Awesome-PHP](https://github.com/ziadoz/awesome-php) 上找到，以下是筆記。

* [Change Log](changelog.md)
* [Docker](docker.md)
* [Coding Style](coding-style.md)
* [Notice](notice.md)
* [Tricks](tricks.md)

## Basic

* [DataType](types.md)
* [How To](how-to.md)

## Advanced

* Socket
  + [Ratchet](https://github.com/ratchetphp/Ratchet)
  + [BrainSocket.php](https://github.com/BrainBoxLabs/brain-socket)
  + [PHP-Websockers](https://github.com/ghedipunk/PHP-Websockets)
  + [Latchet](https://github.com/sidneywidmer/Latchet)
* [Magic Method](magic-method.md)
* [Performance](performance.md)
* [Predefined Interfaces](predefined-interfaces.md)

## Extensions

* [curl](curl.md)

## Build Tools

使用 PHP 達成 [Makefile](/pdl/make/README.md) 一樣的功能，會使用這類工具會有兩個主要原因：執行環境沒有 make 、想要呼叫特定 PHP 的函式功能如建帳號。

* [Robo](http://robo.li/) | 支援非常多種 task ，除了基本檔案與連線操作外，還能跨到 VCS / npm / gulp / Docker 等。
* [Phing](https://www.phing.info/)

## Packages

* PEAR
* [Composer](composer.md)
* codesniffer

### Dependency Injection Container

* [Pimple](pimple.md)
* [PHP-DI](http://php-di.org/)

### ORM

* [Doctrine](http://www.doctrine-project.org/)
* [RedBeanPHP](http://www.redbeanphp.com/index.php)
* [Eloquent ORM](https://laravel.com/docs/5.1/eloquent)
* [Propel](http://propelorm.org/)

## Template engine

* [Blade](http://laravel.com/docs/templates) | Laravel built-in template
* Volt | Phalcon built-in template
* [Twig](http://twig.sensiolabs.org/)
* [Smarty](http://www.smarty.net/)

## Analysis Tools

* [PhpMetrics](http://www.phpmetrics.org/)
* [PHP 程式碼靜態分析工具](http://phpqatools.org/)
* http://stackoverflow.com/questions/4156157/tool-for-php-code-analysis
* http://ithelp.ithome.com.tw/articles/10138375

## Tools

* [phpMyAdmin](https://github.com/phpmyadmin/phpmyadmin)
* [RockMongo](http://rockmongo.com/)
* phpRedisAdmin

## Testing

* [PHPUnit](phpunit.md)
* [phpspec](http://www.phpspec.net/)
* [Codeception](http://codeception.com/)

## Debug or Benchmark

* [XDebug](xdebug.md)
* [PHP-Benchmark](http://victorjonsson.github.io/PHP-Benchmark/)
* [PHP Framework MVC Benchmark - v20111201-4](http://www.ruilog.com/blog/view/b6f0e42cf705.html)

## Editor

Editor

* [Sublime Text](http://www.sublimetext.com/)
* [Notepad++](http://notepad-plus-plus.org/) | Free!! Only for windows.
* [Atom](https://atom.io/) | Free!!

## IDE

IDE

* [Aptana](http://www.aptana.com/) | Free!! Base on Eclipse.
* [NetBeans](https://netbeans.org/) | Free!! HTML 5 support.
* [PHPStorm](https://www.jetbrains.com/phpstorm/) | **Non-free**, The Most Intelligent PHP IDE!! Base on IntelliJ.

## References

* phpDocumentor
* Memcache
* MongoDB
* [Redis](https://github.com/phpredis/phpredis)
* [PHP: The Right Way](http://laravel-taiwan.github.io/php-the-right-way/)
