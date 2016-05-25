Template Method Pattern
=======================

模板方法的定義：

> Define the skeleton of an algorithm in an operation, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm structure.

在一個操作中定義一個演算法框架，而將一些步驟延到子類別，使得子類別不需改變任何演算法結構即可重新定義該演算法的某些特定步驟。

UML
---

Class Diagram

![](http://plantuml.com/plantuml/png/IqmgBYbAJ2vHS8God7CIYuiLghaK59GLgXEXWhKAAVd1-Rcf9HcPUUaQca19ROMIrDo2dCIIL5-WQ7uAKB2MAncirpa_BxaejIGLR18N5wh1DZMwkgWg0000)

PlantUML code

```uml
abstract AbstractClass {
  # {abstract} doSomething()
  + templateMethod()
}
class ConcreteClass

AbstractClass <|-- ConcreteClass
```

Feature
-------

* 封裝不變部分，擴展可變部分
* 提取公共部分，便於維護
* 行為由父類別控制，子類別實作
* 子類別的實作會對父類別的抽象方法產生影響

Note
----

Template method 裡面的演算法有三種變化：

1. abstract
2. default
3. hook

Example
-------

* [Example code](template-method-pattern-example.md)
