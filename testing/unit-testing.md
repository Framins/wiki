Unit Testing
============

單元測試是針對程式專案中的每一個單元或類別進行測試，以確認它的執行結果符合需求。

Unit testing 是個蠻抽象的東西。常常會看到「期望」這個字眼，到底是要期望什麼東西啊？講清楚呀！結論通常還是需要自己想 ...

* 即使裡面會有互相行為上的測試，仍然可被歸類為 unit test
* constructor 通常不需要測，需要測的話，整體的設計就需要檢討了
* getter/setter 也不需要特別寫 unit test 測，只需要測有邏輯性的功能，如加減乘除等
* database schema 通常不需要測，因為當 schema 變動時，production code 要改，test code 也要改，影響整體太多了。這種測試感覺比較像為了測試寫測試，如果有 ORM 之類的套件可以做單一文件控管，此測試就會完全失去它的必要性了

Feature
-------

單元測試的特性有五個特性，剛好是 `FIRST` ：

* *Fast* 快
* *Independent* 獨立
* *Repeatable* 可重複，任何環境都能正常執行
* *Self-Validating* 可以直接反應驗證的結果
* *Timely* 及時，會跟 production code 同步

Frameworks
----------

* [JUnit](http://junit.org/junit4/) `Java`
* [PHPUnit](/pdl/php/phpunit.md) `PHP`
* [Codeception](http://codeception.com/) `PHP`
* [RSpec](http://rspec.info/) `Ruby`
* [QUnit](https://qunitjs.com/) `JavaScript`
* [Mocha](https://mochajs.org/) `JavaScript`

Mock
----

Mock Object 是個很有趣的東西。測試框架利用一些機制，建造了一個虛擬物件，然後去偽裝成某個對象物件，這叫 Mock 。

舉例來說，今天有個權限 class 裡，有個可以檢查會員是否有某些權限的 function ，它需要傳入 Member object 。可是 Member object 並不是這個 case 想測試的目標，但我知道這個 Member object 的行為 (e.g. `getId()` ) ，這時，就是使用 Mock 的時機了。

測試框架可以建立一個具備 Member object 行為的虛擬物件，並可以測試被使用的行為，如「 Member object 可以依群組 id 得知是否有在某個群組，這個群組 id 應該要大於 0 」之行為，也可藉由 Mock 來測試。

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

References
----------

* http://www.codedata.com.tw/java/unit-test-the-way-changes-my-programming
* http://blog.tenyi.com/2006/06/mock-object-pattern.html
* http://www.dotblogs.com.tw/hatelove/archive/2011/12/18/meaning-of-unit-test.aspx
