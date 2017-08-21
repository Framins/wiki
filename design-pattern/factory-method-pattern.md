Factory Method Pattern
======================

工廠方法模式，定義為：

> Define an interface for creating an object, but let subclasses decide which class to instantiate. Factory Method lets a class defer instantiation to subclasses.

UML
---

類別圖

![](http://plantuml.com/plantuml/png/oymhIIrAIqnELN0kIaqioIzIgEPIKD1MS4jC1d8gVLDBCl9JD3IvQhaouIe3Yl9JIfDBk99p4ekB5PppyvABKajIeVhHH65gkM36szJewcBeWQf2bKHeHLMje6U7hWO0)

PlantUML code

```uml
interface Creator {
  + FactoryMethod()
}
interface Product
class ConcreteCreator
class ConcreteProduct

Creator <|-- ConcreteCreator
Product <|-- ConcreteProduct

ConcreteCreator .> ConcreteProduct
```

Before Using Pattern
--------------------

原本有 `Cat` 類別和 `Dog` 類列是屬於動物類別，實作如下：

```php
$cat = new Cat();
$cat->setBraking('Nya');
$cat->setName('Nyales');

$dog = new Dog();
$dog->setBraking('Woof');
$dog->setName('Woofles'); 
```

看程式碼可以思考出幾個問題：

* 如果類別行為修改的話，比方說多一個 `setWalk()` 方法，太棒了！程式所有 `new Cat()` `new Dog()` 的地方都必須修改。
* 兩種類別都是動物類別，行為會是相似的，今天如果加了一個新的類別叫 `Rabbit` ，太棒了！一樣的 code 全都要再 copy 一次。
* 承上，因為行為一樣，所以代表有一樣程式碼的地方可能都需要加個判斷，太棒了！要把所有 `new Cat()` `new Dog()` 再找過一次再確認並修改。

這時就可以使用 `Factory Method Pattern` 解決上述問題

After Using Pattern
-------------------

先寫一個產生動物的 method：

```php
class Factory
{
    /**
     * @param String $animal 動物的類型
     * @param String $name 動物的名字
     * @return AnimalInterface 動物的實體
     */
    public static function getAnimal($animal, $name)
    {
        $object = null;
        switch ($animal) {
            case 'cat':
                $object = new Cat();
                $object->setBraking('Nya');
                $object->setName($name);
                break;
            case 'dog':
                $object = new Dog();
                $object->setBraking('Woof');
                $object->setName($name); 
                break;
            default:
                throw new Exception('未存在的動物: ' . $animal);
        }
        return $object;
    }
}
```

然後原本的程式碼（上層模組）改成這樣：

```php
$cat = Factory::getAnimal('cat', 'Nyales');
$dog = Factory::getAnimal('dog', 'Woofles');
```

從這兩段程式碼可以觀察出一些事：

* 會變動的因素轉變成 method 的引數，如：動物類型、動物名字等。
* 把物件固定行為包裝在 method 裡，如：動物叫聲、動物走路方法等。
* 回傳定義成 interface ，這裡是定義回傳的物件是動物，所以未來有新的動物類別都可以在這裡加入。也可以從這個定義預期它取到的物件會有某種程度的共同性。
* 在 switch 的時候，通常習慣會寫一個會 throw exception 的 default ，因為也許上層模組程式改好了，但底層忘了改，這時在 test 程式的時候馬上就會知道了。

References
----------

* [[http://www.dotblogs.com.tw/joysdw12/archive/2013/06/23/design-pattern-simple-factory-pattern.aspx|簡單工廠模式 (Simple Factory Pattern)]]
