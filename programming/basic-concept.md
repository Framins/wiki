# Basic Concept

此基礎理論為各程式間共同的特性，如變數、型別、運算、判斷、迴圈等。學程式語言之前可以先了解這些，會有個概念可以幫助未來的學習。

參考的程式語言：

* Java
* PHP

## 基本概念

厲害的程式設計師通常會專精某一種程式語言，而其他語言都能短時間掌握。因為他能了解不同語言間的共同點與不同點，並能夠快速的融入到新語言的世界裡。

其實不同程式語言也只是寫法不同。邏輯和概念是相同的。就如同國文和英文的句型裡，一樣會有主詞動詞，只是寫法或順序不同而已。

當然會有這麼多程式存在，必然有它的道理。最主要的原因就是：程式本身的特性，會有它的優缺點。通常這部分是指效能或內建函數等。

## 程式語言分類

這裡程式語言分類的方法是個人自定的：

* 靜態程式語言
* 動態程式語言
* 結構化查詢語言
* 標記式語言

而以下討論的都是帶有 if/else 等流程控制的語言為主。所以標記式語言並不算在此列，結構化查詢語言應該勉強能算。

靜態程式語言與動態程式語言的差別在：

* 型別檢查在編譯時期是靜態語言。
* 型別檢查在執行時期是動態語言。

## 程式寫作風格

每個程式都有獨特的寫作風格，在學習新的程式語言時都必需注意：

* 基本框架
* 英文大小寫
* 空格和換行
* 結束符號
* 註解

## 命名規則

電腦存資料的時候，需要有一個名字，稱**識別字**。而裡面的資料稱為**值**。

數命名規則會依不同程式語言而有所不同，通常如下：

* 英文字母或底線「_」開頭
* 限制字元
* 可以使用大小寫英文、數字或底線「_」
* 區分英文大小寫

## Reserved Word & Keyword

通常指的是程式語法所使用的單字，如 if/else 等。

因為電腦會不懂人類所寫的到底是變數還是語法，所以都會禁止這類單字當作變數或函式名稱。

## Constant & Variable

常數是指不會改變的資料，如 PI = 3.1415...。變數是指會隨著程式執行過程中改變的資料。

變數裡所能儲存的資料則是由資料型態所決定的。

## Scope

牽涉到儲存空間的問題，所以某些變數的資料型態會有其限定的範圍。

## Style

常數與變數命名風格：

* 常數通常以全大寫英文字表示，使用底線「_」分隔單字。
* 匈牙利命名法：把資料型態寫在變數前面。
* 名稱由兩個以上的單字組成時，使用底線「_」分隔單字。
* 駝峰式命名法：利用大小寫區別單字，例如 firstName。

## 基本資料型態

常見的基本資料型態

* 整數（Integer）
* 浮點數（Float, Double）
* 文字（Character, String）
* 布林（Boolean）

## Strong & Weak

* 強型別禁止資料型態自動轉變，如 C/C++、Python
* 弱型別允許資料型態自動轉變，如 PHP、JavaScript

## 運算子

常見到的運算子：

* 算數運算子：+、-、*、/、%
* 關係運算子：==、!=、>、>=、<、<=
* 邏輯運算子：NOT、AND、OR、XOR、!、&&、||、^
* 位元運算子：~、<<、>>、&、|、^
* 指定運算子：=

當然最重要的是優先順序，如果不清楚優先順序的話，可以使用括號輔助。

## 流程控制

流程控制是程式設計最重要的一環，有了流程控制也才能做到判斷的功能。

### if / else

最基本的判斷語法。依組合會有下列幾種情況：

* if : 條件成立就做，不成立就什麼都不做。
* if / else : 條件成立就做，不成立就做else。
* if / else if : 條件A成立就做A，條件B成立就做B，都不成立就什麼都不做。
* if / else if / else : 條件A成立就做A，條件B成立就做B，都不成立就做else。

```
if(condition1)
{
 // condition1 == True
}
elseif(condition2)
{
 // condition2 == True
}
else
{
 // condition1 == False && condition2 == False
}
```

### switch/select case

if / else if / else 如果太多的話，通常都能轉換成 switch / select case 的方式呈現。
可以用以下程式碼跟 if / else if /else 程式比較：

```
switch(variable)
{
 case condition1:
 // condition1 == True
 break;

 case condition2:
 // condition2 == True
 break;

 default:
 // condition1 == False && condition2 == False
}
```

### for

for 迴圈指令通常用在已知迴圈次數的情況下， foreach 也是類似的情況。

```
for(set initial; condition; control)
{
 // run code
}
```

### while

while 迴圈指令通常用在不知迴圈次數的情況下。

case 1 與 case 2 的差別：

  * case 1 為先判斷條件，再決定要不要進入迴圈。
  * case 2 為先進入迴圈，再判斷條件。

#### case 1

```
while(condition)
{
 // run this field when condition is True
}
```

#### case 2

```
do
{
 // run this field when condition is True
 // this field can be run at least once
} while(condition);
```

### break & continue

```
break; //跳出
continue; //跳至下一輪的迴圈
```
