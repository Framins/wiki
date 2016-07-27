Observer Pattern
================

觀眾者模式的定義

> Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

定義物件之間的一對多關係，使得一個物件改變狀態時，所有倚賴於它的物件都會得到通知並且自動被更新。

UML
---

Class Diagram

![](http://plantuml.com/plantuml/png/XOyn3i8m34NtdC9ZAvGBL1KB1s3W18xhYY2KeCH5GctlZbIQ89A1qVRp-xPrmc54OhXCviOaC2k00yneeWGaMG55aAwDx-1i8eSdXxP41lwBE2zsV3MjMfNDcOckGwV7WC8RhkYECSB9EmeilDzPT9D9gVI7Fdxr7MZmUn4pqIzQLzgyypFD-WA7lcQsjFYPlm40)

PlantUML code

```uml
interface Subject {
  + {abstract} attach(o: Observer)
  + {abstract} detach(o: Observer)
  + {abstract} notify()
}
interface Observer {
  + {abstract} update()
}

class ConcreteSubject
class ConcreteObserver

Subject -> Observer : - observers
Subject <|-- ConcreteSubject
Observer <|-- ConcreteObserver
ConcreteSubject <- ConcreteObserver : - subject
```

Terms
-----

  * *Subject* 被觀察者，它必需要能夠動態的增加、取消和通知觀察者，通常是抽象類別或實作類別
  * *Observer* 觀察者，在接收到被觀察者的通知時，對接受到的訊息做處理
  * *ConcreteSubject* 具體的被觀察者，定義自己的業務邏輯，並定義對哪些事件做通知
  * *ConcreteObserver* 具體的觀察者，每個觀察者在收到消息後的處理回應是不同的，各自有各自的邏輯

Example
-------

貓只要看到狗生氣，就會害怕逃走。

### Before using pattern

先依場景寫出介面和實作：

```php
// 貓的介面
interface ICat
{
    // 貓只要遇到危險就會逃跑
    public function run();
}

// 貓的實作
class Cat implements ICat
{
    public function run()
    {
        echo '塊陶啊!!';
    }
}

// 狗的介面
interface IDog
{
    // 狗只要不爽就會生氣
    public function angry();
}

// 狗的實作
class Dog implements IDog
{
    private $cat;

    public function __construct(Cat $cat)
    {
        $this->cat = $cat;
    }

    public function angry()
    {
        echo '林北今天每送!!';
        $cat->run();
    }
}
```

類別間的 UML 圖：

```
<uml>
Interface ICat {
  + {abstract} run()
}
Interface IDog {
  + {abstract} angry()
}
class Cat
class Dog
ICat <|..Cat
IDog <|.. Dog
Dog o- Cat
</uml>
```

場景實作如下

```php
// 會逃跑的貓
$cat = new Cat();
// 會生氣的狗
$dog = new Dog($cat);
// 狗生氣了
$dog->angry();
```

### Problems

程式是完成了，結果也是正確的，但是可以思考幾個問題：

* 如果今天兔子看到狗生氣的時候會跳起來 `Jump` ，程式該怎麼改？
* 如果今天有第二隻小貓看到狗生氣也會逃跑，程式該怎麼改？
* 也有可能貓和兔子都沒看到狗生氣，所以不會被嚇到，程式該怎麼改？

### After using pattern 1

首先解決第一個問題：兔子看到狗生氣的時候會跳起來。

其實可以發現，貓跟兔子看到狗生氣，都會去做特定的一件事 `doSomething`

所以可以把程式改成這樣：

```php
// 動物的介面
interface IAnimal
{
    // 動物只要遇到危險就會做某件事
    public function doSomething();
}

// 貓的實作
class Cat implements IAnimal
{
    public function doSomething()
    {
        echo '塊陶啊!!';
    }
}

// 兔子的實作
class Rabbit implements IAnimal
{
    public function doSomething()
    {
        echo '跳高高!!';
    }
}

// 狗的介面
interface IDog
{
    // 狗只要不爽就會生氣
    public function angry();
}

// 狗的實作
class Dog implements IDog
{
    private $animal;

    public function __construct(IAnimal $animal)
    {
        $this->animal = $animal;
    }

    public function angry()
    {
        echo '林北今天每送!!';
        $animal->doSomething();
    }
}
```

UML 圖如下：

```
<uml>
Interface IAnimal {
  + {abstract} doSometing()
}
Interface IDog {
  + {abstract} angry()
}
class Rabbit
class Cat
class Dog
IAnimal <|.. Cat
IAnimal <|.. Rabbit
IDog <|.. Dog
Dog o- IAnimal
</uml>
```

場景實作

```php
// 會逃跑的貓
$cat = new Cat();
// 嚇貓的狗
$catScaredByDog = new Dog($cat);
// 狗生氣了
$catScaredByDog->angry();

// 會跳高高的兔子
$rabbit = new Rabbit();
// 嚇兔子的狗
$rabbitScaredByDog = new Dog($rabbit);
// 狗生氣了
$rabbitScaredByDog ->angry();
```

目前改成這樣，那未來再把十二生肖都加進來都不會是問題了。

### After using pattern 2

再來解決第二個問題：有第二隻小貓看到狗生氣也會逃跑。所以狗必須要具備能一次能嚇很多隻動物的介面

兩個方法：

  - 在建構子決定好要嚇哪些動物
  - 執行時期決定要嚇哪些動物

方法 1 ，程式碼修改如下：

```php
// 狗的實作
class Dog implements IDog
{
    private $animals;

    public function __construct(array $animals)
    {
        $this->animals = $animals;
    }

    public function angry()
    {
        echo '林北今天每送!!';
        foreach ($this->animals as $animal) {
            $animal->doSomething();
        }
    }
}
```

UML 圖如下：

<uml>
Interface IAnimal {
  + {abstract} doSometing()
}
Interface IDog {
  + {abstract} angry()
}
class Rabbit
class Cat
class Dog
IAnimal <|.. Cat
IAnimal <|.. Rabbit
IDog <|.. Dog
Dog o- IAnimal
</uml>

場景實作如下：

```php
// 會逃跑的貓
$cat = new Cat();
// 會跳高高的兔子
$rabbit = new Rabbit();

// 嚇動物的狗
$dog = new Dog(array($cat, $rabbit));
// 狗生氣了
$dog->angry();
```

### After using pattern 3

方法 2 ，程式碼修改如下：

這同時也解決了問題三：也有可能貓和兔子都沒看到狗生氣，所以不會被嚇到。

```php
// 狗的介面
interface IDog
{
    // 你今天想嚇誰
    public function addAnimal(IAnimal $animal);
    // 狗只要不爽就會生氣
    public function angry();
}

// 狗的實作
class Dog implements IDog
{
    private $animals = array();

    public function addAnimal(IAnimal $animal)
    {
        $this->animals[] = $animal;
    }

    public function angry()
    {
        echo '林北今天每送!!';
        foreach ($this->animals as $animal) {
            $animal->doSomething();
        }
    }
}
```

UML 圖如下：

<uml>
Interface IAnimal {
  + {abstract} doSometing()
}
Interface IDog {
  + {abstract} addAnimal(IAnimal $animal)
  + {abstract} angry()
}
class Rabbit
class Cat
class Dog
IAnimal <|.. Cat
IAnimal <|.. Rabbit
IDog <|.. Dog
IDog -> IAnimal
</uml>

場景實作如下：

```php
// 會逃跑的貓
$cat = new Cat();
// 會跳高高的兔子
$rabbit = new Rabbit();

// 嚇動物的狗
$dog = new Dog();
// 今天想嚇貓
$dog->addAnimal($cat);
// 今天想嚇兔子
$dog->addAnimal($rabbit);
// 狗生氣了
$dog->angry();
```

Reference
---------

  * [Teddy 大師的教學](http://teddy-chen-tw.blogspot.tw/2013/08/observer-pattern.html)
