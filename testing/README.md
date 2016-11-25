Testing
=======

Testing 是門學問，可以參考 [wiki](https://en.wikipedia.org/wiki/Software_testing) 有非常多資料

### 測試種類

* Functional Testing
* Robustness Testing
* Stress Testing
* Performance Testing
* Security testing
* Smoke and sanity testing

### 測試層級

* [Unit Testing](unit-testing.md)
* [Integration Testing](integration-testing.md)
* Component interface testing
* System Testing - 讓整個軟體系統正式啟動，並進行各種測試操作，確認它的功能達到當初設計的需求。
* Operational Acceptance testing

> 單元測試與整合測試 https://media.giphy.com/media/l0MYSpvx4pnsoMNz2/giphy.gif

Tools

* http://webdriver.io/
* http://www.protractortest.org/

Terms
-----

* SUT - System Under Test, 測試的東西
* DOC - Depended On Component, 測試要依賴的元件
* Fixture - 基境
* Test Double - 測試替身
  - **Dummy Object:** 測試需要的物件，可是測試的過程不會用到它
  - **Stub:** 實作回傳固定值，通常是做「狀態驗證」
  - **Spy:** 實作呼叫記錄，通常是做「行為驗證」
  - **Mock:** 可以使用程式自動產生 Dummy Object / Stub / Spy
  - **Fake:** 以簡單實作來取代實際實作，如 SQLite 取代 MySQL
