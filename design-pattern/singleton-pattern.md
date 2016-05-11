Singleton Pattern
=================

單例模式定義：

> Ensure a class has only one instance, and provide a global point of access to it.

UML
---

類別圖

![](http://plantuml.com/plantuml/png/Iyv9B2vM2CxCIyz9BSdFKwZcKb3GLQWkBaaioKokLSZC0xBoabE1ejgOeXgQLWYjNBLSN0XpTEqGCW00)

PlantUML code

```uml
class Singleton {
  - {static} instance
  + {static} instance(): Singleton
}

Singleton -> Singleton
```

Example
-------

```php
class Config
{
    private static $instance = null;
    
    private function __construct()
    {
    }
    
    public static function getInstance()
    {
        if (self::$instance === null) {
            self::$instance = new self();
        }
        return self::$instance;
    }
}
```

擴展的 singleton

```php
class Factory
{
    private static $instance = array();
    
    private function __construct()
    {
    }
    
    public static function getInstance($type)
    {
        if (!isset(self::$instance[$type])) {
            self::$instance[$type] = new $type();
        }
        return self::$instance[$type];
    }
}
```

Features
--------

* 使用 static function 取得實例
* 減少記憶體消耗，增加系統效能
* 通常沒有介面，所以想擴展只能改原始碼
