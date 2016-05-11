Bridge Pattern
==============

橋接模式的定義：

> Decouple an abstraction from its implementation so that the two can vary independently.

將抽象和實作解耦合，使得兩者可以獨立地變化。

UML
---

Class Diagram

PlantUML code

```uml
abstract class Abstraction {
  + {abstract} operation()
}

class RefinedAbstraction {
}

interface Implementor {
  + {abstract} implementation()
}

class ConcreteImplementor {
}

Abstraction o- Implementor : + impl
Abstraction <|-- RefinedAbstraction
Implementor <|-- ConcreteImplementor
```

Terms
-----

* *Abstraction* - 抽象化角色，使用這個物件的抽象行為，通常會是抽象類別
* *RefinedAbstraction* - 修正抽象化角色，抽象行為的實作
* *Implementor* - 實作化角色，可以是介面或抽象類別
* *ConcreteImplementor* - 具體實作化角色

Example
-------

```php
interface DrawingAPI
{
    function drawCircle($dX, $dY, $dRadius);
}

class DrawingAPI1 implements DrawingAPI
{ 
    public function drawCircle($dX, $dY, $dRadius)
    {
        echo "API1.circle at $dX:$dY radius $dRadius.<br/>";
    }
}
 
class DrawingAPI2 implements DrawingAPI
{ 
    public function drawCircle($dX, $dY, $dRadius)
    {
        echo "API2.circle at $dX:$dY radius $dRadius.<br/>";
    }
}

abstract class Shape
{ 
    protected $oDrawingAPI;
 
    public abstract function draw();
    public abstract function resizeByPercentage($dPct);
 
    protected function __construct(DrawingAPI $oDrawingAPI)
    {
        $this->oDrawingAPI = $oDrawingAPI;
    }
}

class CircleShape extends Shape
{ 
    private $dX;
    private $dY;
    private $dRadius;
 
    public function __construct($dX, $dY, $dRadius, DrawingAPI $oDrawingAPI)
    {
        parent::__construct($oDrawingAPI);
        $this->dX = $dX;
        $this->dY = $dY;
        $this->dRadius = $dRadius;
    }
    public function draw()
    {
        $this->oDrawingAPI->drawCircle(
                $this->dX,
                $this->dY,
                $this->dRadius
        );
    }
 
    public function resizeByPercentage($dPct)
    {
        $this->dRadius *= $dPct;
    }
}

$aShapes = array(
    new CircleShape(1, 3, 7,  new DrawingAPI1()),
    new CircleShape(5, 7, 11, new DrawingAPI2()),
);
 
foreach ($aShapes as $shape) {
    $shape->resizeByPercentage(2.5);
    $shape->draw();
}
```

Features
--------

* 符合 Least Knowledge Principle
* 抽象實作分離
* 想加實作？加！想加抽象？加！很好擴充。
