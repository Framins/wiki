Builder Pattern
===============

Builder Pattern 的定義：

> Separate the construction of a complex object from its representation so that the same construction process can create different representations.

把一個複雜的物件建構過程和它的表示分離，使得一樣的建構過程可以創建出不同的表示。

Terms
-----

  * **Product:** - 產品類別，通常會實作 Template Method Pattern ，會有模板方法和基本方法。
  * **Builder:** - 抽象建造者，規範產品的組建，會由子類別實作。
  * **ConcreteBuilder:** - 具體建造者，實作 Builder 定義的所有方法，並返回一個組建好的物件。
  * **Director:** - 導演類別。它會用 ConcreteBuilder 設置零件，然後再取得物件。

Pros and Cons
-------------

### Pros

  * Client 不需要知道產品內部組成的細節，只要知道產生的物件就是期望的就好。
  * Builder 是相對獨立的，所以要擴展是非常方便的。
  * 承上，也因為是獨立的，所以各別的修改，並不會對其他模組造成任何影響。
