Testing
=======

Unit Testing
------------

Unit testing 是個蠻抽象的東西。常常會看到「期望」這個字眼，到底是要期望什麼東西啊？講清楚呀！結論通常還是需要自己想 ...

Keyword: 

* Rubber Duck Debugging: ㄧ行ㄧ行解釋程式碼在做什麼
* Test-driven development: 測試驅動開發
* Behavior-driven development: 行為驅動開發
* integra test: 整合測試。只管整體的行為是否正確，不管元件內部行為是不是正確。
  * bahavier test = 行為測試。只管元件內部行為是否正確，不管它與其他元件是否能共存。
    * 某個上層模組，會用到多個下層模組。只要跨過這個模組與模組的界線，就屬於 bahavier test 了
  * unit test = 單元測試。針對程式最小單位，來進行正確性的檢驗。
    * 即使裡面會有互相行為上的測試，仍然可被歸類為 unit test
    * constructor 通常不需要測，需要測的話，整體的設計就需要檢討了。
    * getter/setter 也不需要特別寫 unit test 測，只需要測有邏輯性的功能，如加減乘除等。
    * database schema 通常不需要測，因為當 schema 變動時，product code 要改，test code 也要改，影響整體太多了。這種測試感覺比較像為了測試寫測試，如果有 ORM 之類的套件可以做單一文件控管，此測試就會完全失去它的必要性了。
  * Mock object = 模擬物件。
    * 模擬的物件，主要知道使用它的上層模組，到底會如何使用這個模擬的物件，e.g. 一個算開根號的模組，一定會用到除法模組，但如果使用除法模組時，不該讓除數會等於 0，這時用模擬物件就可以測出這個除法模組在開根號模組裡，是正常被使用的。

Reference:

* http://www.codedata.com.tw/java/unit-test-the-way-changes-my-programming
* http://blog.tenyi.com/2006/06/mock-object-pattern.html
* http://www.dotblogs.com.tw/hatelove/archive/2011/12/18/meaning-of-unit-test.aspx

Terms
-----

* SUT - System Under Test, 測試的東西
* DOC - Depended On Component, 測試要依賴的元件
* Fixture - 基境
* test double - 測試替身
  * Dummy Object
  * Test Stub
  * Test Spy
  * Mock Object
  * Fake Object

Implement
---------

* JUnit (Use for Java)
* PHPUnit (Use for PHP)
* QUnit (Use for Javascript)
* Android Test (Use for Android)

Practice
--------

* Unit testing - 單元測試是針對程式專案中的每一個單元或類別進行測試，以確認它的執行結果符合需求。
* Integration testing - 將多個單元或類別結合起來，讓它們同時執行並進行互動，以確認它們之間的交互運作符合原來設計的目的。
* Database testing
* Mocking testing
* System testing - 讓整個軟體系統正式啟動，並進行各種測試操作，確認它的功能達到當初設計的需求。

Integration Testing
-------------------

Integration Testing ，整合測試簡單來說，是會與外部服務有相依的測試。

外部服務有很多種，如：

* Database
* Internet
* File I/O
* Environment setting (要先設定環境，才能執行測試)

Unit Testing
------------

單元測試的特性有五個特性，剛好是 `FIRST` ：

  * *Fast* 快
  * *Independent* 獨立
  * *Repeatable* 可重複，任何環境都能正常執行
  * *Self-Validating* 可以直接反應驗證的結果
  * *Timely* 及時，會跟 production code 同步

Step
----

單元測試有分四個階段：

1. *setup* - 建立基本測試環境
2. *exercise* - 執行測試案例
3. *verify* - 驗證結果
4. *teardown* - 還原最原始的狀態

以 PHPUnit 為例：

```php
/**
 * Prepares the environment before running a test.
 */
protected function setUp()
{
	parent::setUp();
}

/**
 * Cleans up the environment after running a test.
 */
protected function tearDown()
{
	parent::tearDown();
}
```

> 通常 setUp() 有用外部資源的時候，就需要 tearDown() 回歸原始狀態

所以執行順序應該會是 setUp() -> testA() -> tearDown() -> setUp() -> testB() -> tearDown() ....
