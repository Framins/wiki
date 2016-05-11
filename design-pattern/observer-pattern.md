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

Reference
---------

  * [[http://teddy-chen-tw.blogspot.tw/2013/08/observer-pattern.html|Teddy 大師的教學]]
