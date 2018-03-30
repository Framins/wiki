# Template Method Pattern Example

今天想訓練小貓要做表演。

## Before using pattern

貓會做的表演有很多，可以先定義一個表演介面：

```php
interface Show
{
    // 跳火圈
    public function jumpFireRing();
    // 走鋼索
    public function walkOnTightrope();
    // 敬禮
    public function salute();
    // 表演囉
    public function run();
}
```

開始訓練小貓：

```php
class Cat implements Show
{
    public function jumpFireRing()
    {
        echo '貓跳火圈，搖來搖去';
    }

    public function walkOnTightrope()
    {
        echo '貓走鋼索，四平八穩';
    }

    public function salute()
    {
        echo '我是個很傲嬌的小貓';
    }

    public function run()
    {
        $this->jumpFireRing();
        $this->walkOnTightrope();
        $this->salute();
    }
}
```

來了一隻小狗，一樣也來訓練它做表演：

```php
class Dog implements Show
{
    public function jumpFireRing()
    {
        echo '狗跳火圈，生龍活虎';
    }

    public function walkOnTightrope()
    {
        echo '狗走鋼索，搖搖晃晃';
    }

    public function salute()
    {
        echo '我是個有禮貌的小狗';
    }

    public function run()
    {
        $this->jumpFireRing();
        $this->walkOnTightrope();
        $this->salute();
    }
}
```

### UML Diagram

![](http://plantuml.com/plantuml/png/oymhIIrAIqnELGZEo2zNgEPIKD1Mg4vCAYufIamkgLN8AiqjSCiiIWtAp4lNq4INBK_CoVRF2ybCpoWfoYz8nLHGd9XJMe95lAWq3oXOovMSarXShE2SM09bkUIdSu4TObEZfmSMH_20SW00)

### PlantUML code

```uml
@startuml
interface Show {
  + {abstract} jumpFireRing()
  + {abstract} walkOnTightrope()
  + {abstract} salute()
  + {abstract} run()
}
class Cat
class Dog
Show <|.. Cat
Show <|.. Dog
@enduml
```

場景程式如下：

```php
// 會表演的貓
$cat = new Cat();
// 來表演吧
$cat->run();

// 會表演的狗
$dog = new Dog();
// 來表演吧
$dog->run();
```

## Problems

目前程式可以發現的問題如下：

* `run()` 出現了重複的程式碼，要是新動物再加入的話，相同程式碼會無限擴張，那程式該如何改寫？
* 老鼠跳不高，無法表演跳火圈，但會表演走鋼索，程式該如何寫？

## After using pattern Part 1

依照物件導向的功能，可以把相同的程式碼提出來做抽象類別，其他程式再繼承它即可：

```php
abstract class ShowAnimal implements Show
{
    final public function run()
    {
        $this->jumpFireRing();
        $this->walkOnTightrope();
        $this->salute();
    }
}

// 小貓的實作
class Cat extends ShowAnimal
{
    public function jumpFireRing()
    {
        echo '貓跳火圈，搖來搖去';
    }

    public function walkOnTightrope()
    {
        echo '貓走鋼索，四平八穩';
    }

    public function salute()
    {
        echo '我是個很傲嬌的小貓';
    }
}

// 小狗的實作
class Dog extends ShowAnimal
{
    public function jumpFireRing()
    {
        echo '狗跳火圈，生龍活虎';
    }

    public function walkOnTightrope()
    {
        echo '狗走鋼索，搖搖晃晃';
    }

    public function salute()
    {
        echo '我是個有禮貌的小狗';
    }
}
```

### UML Diagram

![](http://plantuml.com/plantuml/png/oymhIIrAIqnELGZEo2zNgEPIKD1Mg4vCAYufIamkgLN8AiqjSCiiIWtAp4lNq4INBK_CoVRF2ybCpoWfoYz8nLHGd9XJMe95lAWq3oXOomKJ0Tlkc9UPcvW3TGDCHN9EOd6nWdDY2PJbaf_E1NQgJOsU7f8sBYGJR6fqTS5QqCM0cW40)

### PlantUML code

```uml
@startuml
interface Show {
  + {abstract} jumpFireRing()
  + {abstract} walkOnTightrope()
  + {abstract} salute()
  + {abstract} run()
}
abstract ShowAnimal {
  + run()
}
class Cat
class Dog
Show <|.. ShowAnimal
ShowAnimal <|-- Cat
ShowAnimal <|-- Dog
@enduml
```

## After using pattern Part 2

再來解決問題二：老鼠跳不高，無法表演跳火圈，但會表演走鋼索。

需要在樣版裡修改一些方法：

```php
abstract class ShowAnimal implements Show
{
    protected function canJumpFireRing()
    {
        return true;
    }

    protected function canWalkOnTightrope()
    {
        return true;
    }

    final public function run()
    {
        if ($this->canJumpFireRing()) {
            $this->jumpFireRing();
        }

        if ($this->canWalkOnTightrope()) {
            $this->walkOnTightrope();
        }

        $this->salute();
    }
}

// 老鼠的實作
class Mouse extends ShowAnimal
{
    protected function canJumpFireRing()
    {
        return false;
    }

    public function jumpFireRing() {}

    public function walkOnTightrope()
    {
        echo '老鼠走鋼索，我超強';
    }

    public function salute()
    {
        echo '我是天竺鼠啦！';
    }
}
```

### UML Diagram

![](http://plantuml.com/plantuml/png/ZP3B2i8m44Nt-Oe1DqffFq2w4SM5888AhgSXrcWwANdGHTj_LqChDRXmDvovpE6E92VC5Rc0qqqtq3A06N2adQ_ghJJYAAcSBs09XTPA88tx2wh7WSwol3cZQn554cYniCuWTptSlqx5soO-50SiAkz-SEFf1Nisab1WHR925MeadmHNQ2siqGtJHfV3jDVUYZzAzony9--oRA9X4sFUfMbGnEmjYrdGFW40)

### PlantUML code

```uml
@startuml
interface Show {
  # canJumpFireRing() : boolean
  # canWalkOnTightrope() : boolean
  + {abstract} jumpFireRing()
  + {abstract} walkOnTightrope()
  + {abstract} salute()
  + {abstract} run()
}
abstract ShowAnimal {
  + run()
}
class Cat
class Dog
class Mouse {
  # canJumpFireRing() : boolean
}
Show <|.. ShowAnimal
ShowAnimal <|-- Cat
ShowAnimal <|-- Dog
ShowAnimal <|-- Mouse
@enduml
```

場景程式如下：

```php
// 會表演的貓
$cat = new Cat();
// 來表演吧
$cat->run();

// 會表演的狗
$dog = new Dog();
// 來表演吧
$dog->run();

// 會表演的老鼠，但不會跳火圈
$mouse = new Mouse();
// 來表演吧
$mouse->run();
```
