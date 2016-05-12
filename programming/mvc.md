MVC
===

在專案開發的時候，可能會遇到以下問題：

* 視覺美觀和程式混雜在一起，難以分辨
* 程式碼除錯因包含視覺美觀，所以更難找到關鍵有問題的程式碼
* 擴充功能時，常常會因為動到一個變數，導致整個系統需要大變動
* 多人開發專案常常會因為程式碼的連帶關係，變成必須等待關鍵程式碼完成，才能進行下一階段開發。

有以上問題，先說聲恭喜。因為代表 Coding 技術可以再前進了一大步。

以上問題首選的解決方法就是－－使用 MVC Design Pattern 。MVC的目的是要實作一個低耦合的框架基底，使得擴充功能或是後續修改的問題都能夠有效降低。

以下以 PHP 語言說明 Web MVC 的觀念

Basic Concept
-------------

MVC 是一種軟體設計的模式，它裡面有三種主要元件：

* Model (資料讀取)
* View (視覺美觀)
* Controller (流程控制)

此三種主要元件的互動如下：

![](http://plantuml.com/plantuml/png/Iyv9B2vMS2hABozEBU9A1lDyyrDISw3iiCpKSYZJEJ-lf2W_9mUeZWkgGK7N3baOmLIm0Sf0p44Ir0KAWWq44M0Ur1m0)

  - Browser 對 Controller 提出 Request。
  - Controller 依 Request 去提取 Model。
  - Controller 依 Request選擇適合的 View ，並傳送 Model 的資料給 View 準備做顯示。
  - View 將資料放入樣版中，並輸出給 Browser。

===== Model =====

''Model'' 是負責處理資料相關和存取的元件。

Model 設計要注意以下重點：

  * Model 不會有任何 HTML 或任何輸出，因為它不管資料如何呈現
  * 同理， Model 不會出現 ''echo'' 、 ''print'' 、 ''header'' 、 ''exit'' 等輸出內容的方法
  * 只有 Model 才能存取資料庫、檔案或其他資料媒介
  * 不可直接存取 GET/POST/COOKIE... 等全域變數
  * 只有 Model 會出現資料結構與演算法

=== Model & Table ===

Model 與 Table 的關係如下，都是合理的：

  * 一個 Model 對應一張 Table，這也是最常見的狀況
  * 一個 Model 會從許多 Table 取得資料並組合
  * Model 沒有對應的 Table

畢竟， **Model 是一個 Layer** ，跟 Database 並沒有絕對要直接一對一的關係

===== Library =====

多個 Model 常做同一件事的話，可以改使用 Library 。

===== View =====

''View'' 決定了資料該用什麼方式呈現，如：可以用 HTML/XML/RSS/JSON 不同的格式輸出；也可以做不同版面設計的輸出，像手機版、電腦版和列印版等。

View 設計要注意以下重點：

  * 唯一可以出現 HTML/XML.... 的檔案
  * 不可直接存取 GET/POST/COOKIE... 等全域變數
  * 依輸出方式不同，可能會有 if/else/switch/for 等
  * View 會用 Model 取得的資料做輸出，但實際上它不需要理會 Model 是如何設計的

===== Controller =====

''Controller'' 是唯一會直接接受 client 的要求，並會依 client 要求去取得需要的 Model ，並選擇 View 做輸出。

Controller 設計要注意以下重點：

  * Controller 不會有任何 HTML ，因為它不管資料如何呈現
  * Controller 不會有任何 SQL 或是 fopen 等存取資料的方法
  * 理論上會用到流程控制只會有 if/else/switch，而不會有for

===== Helper =====

''Helper'' 通常處理的都只是單純資料格式轉換，或是產生 HTML 等。所以通常都是 View 和 Controller 會出現。

===== Something else =====

其他相關名詞：

  * Service - 從 DAO / Model 取出資料後，整理出對 Service 有意義的資料
  * DAO - Data access object - 存取資料的物件
  * [[http://martinfowler.com/eaaCatalog/dataTransferObject.html|DTO]] - Data transfer object - Controller / View / Service 共用的傳輸資料媒介

參考：

http://my.oschina.net/pacoyang/blog/151695
===== Implements =====

實作 MVC 的 Framework

{{topic>MVC&simplelist}}

===== Reference =====

  * [[http://blog.turn.tw/?p=217|MVC ，令人搞不懂的 MODEL。]]
