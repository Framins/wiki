Prototype Pattern
=================

原型模式是把一個物件當作基底，然後 clone 一份一模一樣的出來當作是新的。

Pors and Cons
-------------

### Pors

* 因為是記憶體直接 clone，所以會比 new 還要快
* 不會被 constructor 約束，相對就比較自由。

### Cons

* 不會被 constructor 約束，相對就比較不安全。

Context
-------

Prototype Pattern 適用於下例場合：

* 資源需要最佳化的情況
* 效能或權限要求比較多的情況
* 一個物件會被很多個 client 修改的情況
