# ORM

因網路上的資訊很多很雜，以下純屬個人理解

詳細說明可以參考 [wiki][] ，與 SQL 之間的差異可參考[這裡](http://www.dotblogs.com.tw/code6421/archive/2009/02/10/7100.aspx?fid=60147)

Zend 的 ORM 實作是使用 Active Record

兩者的差異應該是實作 ORM 時，本身並不會具備 save(), delete() 等邏輯 function ，而 Active Record 是有的 ([RoR][] 亦同，但 [CodeIgniter][] 雖然稱之為 Active Record ，可是卻沒有這種感覺...)

## Overview

### Pros

* 資料庫結構與程式有個對應/統一的方式，對穩定性會有幫助，以 [Doctrine][] 來說，只要程式有了變動並在程式端有執行更新 schema 的話，資料庫的所有欄位都會跟著程式的定義同步。
* 資料庫結構本來也就是一個不易變動的因數，所以與之對應的物件設計，就不容易變動；使用該物件的上層模組變動的因數也會降低。
* 因為是使用物件導向的概念來呈現每筆 Record 的樣子，代表 Record 除了原本的欄位資料外，還可以有物件的定義方式，比如說暫存變數或 function ，甚至還能做到 Lifecycle Callback 等功能。

### Cons

* ORM 最多人垢病的缺點就是效能差。只能使用 cache 或是部分讀取方法改成傳統 SQL 等方法，來提升效能。
* 當 ORM 寫的邏輯越來越多的時候，可能會違反 SRP 原則，可能會跟 OOAD 的概念有所衝突。

## Implements

不同語言裡的實作

### PHP

* [Doctrine][]
* Propel
* RedBeanPHP

### Java

* ORMLite

### Ruby

* Rails ActiveRecord

[wiki]: https://zh.wikipedia.org/wiki/对象关系映射
[RoR]: http://ihower.tw/rails3/activerecord.html
[CodeIgniter]: http://www.codeigniter.org.tw/user_guide/database/active_record.html
[Doctrine]: http://www.doctrine-project.org/
