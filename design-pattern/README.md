Design Pattern
==============

建築師設計房子時，可以先為浴室的位置或是廚房的構造方式開發模版，使用這些模版即可快速設計更好的房子。而設計模式的核心概念正是如此，除了讓程式的開發能更快速外，也讓新功能的加入變得更方便。

談到 Design Pattern ，就一定要提一下 Gof 了，Gof 即 `Gang of four` ，也就是四人幫的意思。[設計模式](http://www.amazon.com/exec/obidos/tg/detail/-/0201633612/ref=ase_portlandpatternrA/002-6454224-1040813?v=glance&s=books)這本書就是由這四個人共同整理撰寫的。裡面總共有 23 種設計模式，概分成 3 個類型。這本書可以說是設計模式的經典之作。

最早講到設計模式，是指 Gof 的這本著作。後來設計模式一詞被廣泛的應用到各種經驗。

Glossary of terms
-----------------

設計模式裡面也蠻多專有名詞的。除了下面六大原則和那一堆模式外，其他可以簡單介紹的名詞，就在這裡面說明了。

* *robust* 強健性。
* *client* 通常泛指「相對」的上層模組。

Design Principles
-----------------

六大設計原則。

* Single Responsibility Principle
* Liskov Substitution Principle
* Dependency Inversion Principle
* Interface Segregation Principle
* Least Knowledge Principle
* Open Close Principle

Creational Patterns
-------------------

創建型模式是處理物件建立的設計模式，此模式會試著依需實際情況來使用合適的方法建立物件。

基本的物件建立方式會有設計上的問題，或是增加設計的複雜度，所以可以靠此一類型的設計模式來控制物件的建立，並解決實際的問題。

* Singleton Pattern
* Simple Factory Pattern
* Factory Method Pattern
* Abstract Factory Pattern
* Builder Pattern
* Prototype Pattern

加強的 Pattern：

* Registry of Singleton Pattern

Structural Patterns
-------------------

結構型模式。

* Proxy Pattern
* Bridge Pattern
* Decorator Pattern
* Flyweight Pattern
* Facade Pattern
* [Adapter Pattern](adapter-pattern)
* Composite Pattern

Behavioral Patterns
-------------------

行為型模式。此類型的模式主要是用來實現物件之間的交流方法，並增加物件交流時的彈性。

* Template Method Pattern
* Command Pattern
* Strategy Pattern
* Chain-of-responsibility Pattern
* Iterator Pattern
* Observer Pattern
* Interpreter Pattern
* State Pattern
* Mediator Pattern
* Visitor Pattern
* Memento Pattern
* Concurrency Pattern

Another Patterns
----------------

跟 Gof 文件無關，但現在很常見的 Patterns

* Fluent Interface Pattern

Reference
---------

* http://www.cnblogs.com/wisekingokok/archive/2011/10/14/2211247.html
