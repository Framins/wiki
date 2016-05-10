Adapter Pattern
===============

Adapter Pattern 的定義：

> Convert the interface of a class into another interface clients expect. Adapter lets classes work together that could not otherwise because of incompatible interfaces.

讓兩個不同規格的介面可以同時運作，就是 `Adapter Pattern` 了。它的特點是在原有不相容的系統間做一個轉換的動作，使得兩系統不需做大幅度地修改，也能正常運作。

現實生活中的 Adapter 指的是變壓器，其實也是同樣的道理：機器需要用直流電，但只有交流電該怎麼辦？用 Adapter ！交流電又有分 110V 和 220V 煩死了該怎麼辦？換 Adapter ！

UML
---

```uml
class Client

interface Target {
  + request()
}
class Adapter
class Adaptee {
  + specificRequest()
}

Client -> Target
Target <|.. Adapter
Adapter -> Adaptee : + adaptee
```

Terms
-----

以上述變壓器的說明來解釋下面的關鍵字：

* *Target* - 目標角色（直流電），簡單來說就是 Client 期望的介面。
* *Adaptee* - 來源角色（交流電），會被轉換成目標角色。
* *Adapter* - 轉接器角色（變壓器），此模式的核心角色，其他兩個角色都是原本存在的，這個角色是新建立準備要讓他們和平共處的。


Pluggable Adapter Pattern
-------------------------

上述情境是在 Adaptee 固定的情境下使用 Adapter Pattern 的。相反的， Client 固定，而 Adaptee 不固定時，就稱之為 *Pluggable Adapter* 。 

如果是這種情況的話， Adapter 就可以先行設計。讓未來想塞資料給 Client 的 source 實作 Adapter 即可。

參考實作：

* Android UI 的 `Adapter`
* Zend Framework 的 `Zend_Paginator`

Example
-------

想讓貓學其他的動物叫，如果沒用 adapter 的話就是要硬改:

```php
class Cat
{
    public function braking()
    {
        return 'Woof!!';
    }
}
```

今天可以幫貓做個變聲器，想讓它像貓就像貓，像狗就像狗：

```php
class Cat
{
    protected $_adapter;

    public function __construct(Adapter $adapter)
    {
        $this->_adapter = $adapter;
    }

    public function braking()
    {
        return $this->_adapter->braking();
    }
}

class Woof extends Adapter
{
    public function braking()
    {
        return 'Woof!!';
    }
}

class Nya extends Adapter
{
    public function braking()
    {
        return 'Nya!!';
    }
}

$adapter = new Woof();
$cat = new Cat($adapter);
echo $cat->braking();
```

Pros and Cons
-------------

### Pros

* 兩個無關的類別，只要有了 Adapter 搞定它們，就可以放在一起執行。
* Client 只會知道 Target 提供的方法，不會知道 Adaptee 的實作，符合 Least Knowledge Principle 。
* 原本的類別都沒做任何修改，所以一樣都還是可以再被其他類別正常使用。
* 靈活度高，想用 Adapter 就用，不想用就刪，其他程式碼都不用修改。

### Cons

* 轉換的過程有可能很麻煩。
* 中間隔了一層，效能可能會有影響

> 在「完美」的設計裡，是不需要 Adapter Pattern 的。通常用在事後的補救居多。

Reference
---------

* http://openhome.cc/Gossip/DesignPattern/AdapterPattern.htm
* http://www.dotblogs.com.tw/pin0513/archive/2010/05/30/15497.aspx
* http://teddy-chen-tw.blogspot.tw/2013/08/adapter-pattern.html
* http://teddy-chen-tw.blogspot.tw/2013/05/clean-codeadapter.html
* http://www.dotblogs.com.tw/wasichris/archive/2014/09/28/146732.aspx
