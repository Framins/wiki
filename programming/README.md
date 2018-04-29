# Developer

身為一個要成為開發者的路圖。

## Basic

* [Basic Concept](basic-concept.md)
* [Statement & Expression](statement-n-expression.md)
程式設計入門需要必備的基礎知識。

### Function and Subroutine

如果只使用基本概念寫程式的話，會遇到一個問題是：重複的程式碼過多。  
在這個情況下，我們可以用函式的方法來解決這個問題。  
這也是程式設計常見的程序導向設計的實際做法。

### Object-Oriented Programming

函式雖然可以有效解決重複程式碼問題，可是一個函式只能處理一件事，當然很多功能時，就要寫很多函式來解決。  
這時多希望一個函式能有很多功能啊。  
不過事實上，函式是很難辦到的，但我們可以使用物件導向設計來解決。

## Advanced

進階的程式設計相關知識。

* [Regex](regex.md)
* [MVC](mvc.md)
* [Dependency injection](di.md)
* [ORM](orm.md)
* [Refactoring](refactoring.md)

### Exception Handling

在程式的執行過程中，總是會發生很多不可預期的錯誤，而導致程式執行錯誤而造成當機。  
而學會了例外處理，就可以解決大部分執行錯誤的問題了。

### Process & Thread

有時我們會希望程式能同時做兩件以上的事，比方說遊戲要一邊繪圖、一邊接受使用者命令、一邊讀取關卡資料。  
可是程式撰寫都是一行一行的命令處理下去的，該如何變成同時處理多行命令？這時我們就要用到 Process 或 Thread 了！  
當然同時要能處理多行命令時，會有幾個大問題必需要解決：時間和空間、資料一致性。  
必須要先了解原理後，才能寫出不易出錯的程式。

* [Process & Thread](process-n-thread.md)

### Networking

現在網路的方便性和實用度，比起以前已經大大提升了不少。但相對的，對於開發者來說，把網路加入程式也變成一種基本技能了。

### Algorithm

演算法描述了處理任務的具體步驟。它定義一個開始狀態，然後在有限的步驟內執行完畢，並在最終產生輸出，並停止於一個結束狀態。

演算法的好壞，直接決定了程式執行的效率。所以學習設計一個好的演算法，也是一門非常重要的課程。

## Extreme

程式設計到了最後，當然是要學如何控制程式版本和多人多工了。

## References

* [工程師生涯 30 年：真希望在菜鳥時期就懂得的這些事](https://buzzorange.com/techorange/2016/02/15/lessons-from-my-lifetime-of-being-a-programmer-during-30-years/)
