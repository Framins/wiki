Variable Type
=============

跟大多數語言一樣，它有基本資料型態、複合資料型態和特殊值。

JavaScript 是弱型別語言，所以需要檢查型態的語法。測試過下面這兩個都是可行的：

    > typeof(10)
    'number'
    > typeof 10
    'number'

基本資料型態
------------

基本資料型態有 `Number` `String` `Boolean` 三種。

### 不基本的 Number

JavaScript Number 的範圍

* 最小值 `Number.MINVALUE` (5e-324)
* 最大值 `Number.MAXVALUE` (1.7976931348623157e+308)

在 JavaScript 裡，Number 包括了下面這些內容

* 整數，常見的 Integer
* 浮點數，常見的 Float
* 無限大，正無限大為 `Infinity`，負無限大為 `-Infinity`
* 非數值，`NaN` (Not a Number)

數字表示的時候，可以用十進位、八進位和十六進位：

    1234 // 十進位
    0678 // 八進位，但使用 ES5 的嚴格模式時，不能使用八進位表示
    0xFF // 十六進位

要表示浮點數時，可以用科學記號

    123.4
    1.234E2 ( 1.234 * 10 ^ 2 )
    1.234E-10 (1.234 * 10 ^ -10)

正無限大和負無限大，也有常數可以直接取用：

    Number.POSITIVE_INFINITY // 正無限大
    Number.NEGATIVE_INFINITY // 負無限大

最後的 `NaN` 很抽象，它說不是個數字，可是使用 typeof 卻又看到回傳跟你說 `NaN` 是個數字(怒)；然後 `NaN` 又不等於 `NaN`，JavaScript 你搞得我好煩啊！

    > typeof(NaN)
    'number'
    > NaN === NaN
    false

不過還是思考一下 JavaScript 為何會這樣設計，先看 `NaN` 是怎麼產生的：

    > 1/'s'
    NaN

當一般數值運算子中，遇到了一邊或兩邊都是非數值時，就會出現這種狀況。就想法上來說，確實想對非數值的資料做運算，那的確就是 `NaN` 。非數值也是絕對不會相等 ( `1/'a'` 和 `1/'b'` 是要怎麼比較啦) 。但是數值運算子預期的結果又是希望它是一個 `Number`

雖然是可以理解，但看起來的結果還蠻抽象的。

在判斷上，JavaScript 有提供內建 function `isNaN()`，不過奇怪的是，無法自動轉型到 Number 的值，都還是會回傳 true。

    > isNaN('string');
    true
    > isNaN(undefined);
    true

因此如果要使用 `isNaN()` 就必須要考慮這個值能不能被轉換成數字，不然還是自己寫 function

因為 `NaN` 是 JavaScript 中唯一自身不等於自身的值，所以該 function 的內容可以這樣寫：

```javascript
function isRealNaN(value) {
    return value !== value;
}
```

### 很基本的 String

JavaScript 並沒有字元，只有字串。可以用單引號或是雙引號來表示字串。

因為單引號和雙引號都可以使用，所以網頁 JavaScript 通常習慣上會使用單引號，雙引號給 HTML 使用。

```javascript
var html = '<div class="btn"></div>';
```

### 更基本的 Boolean

Boolean 就如一般寫程式所知道的，只有兩個值： `true` 和 `false` 。

### 複合資料型態

複合資料型態是指物件 (Object)，在用 typeof 時，都會回傳 `object`

    > typeof new Object()
    'object'
    > typeof new Array()
    'object'

可以使用 `instanceof` 關鍵字來測試物件是否是某個型態的實例：

    > {} instanceof Object
    true
    > {} instanceof Array
    false
    > [] instanceof Object
    true
    > [] instanceof Array
    true

`null` 在 typeof 時會是 `object` ，但 instanceof Object 的時候卻是 `false` 。

    > typeof null;
    'object'
    > null instanceof Object;
    false

一樣要思考一下，為何 JavaScript 要這麼設計：

JavaScript 認為 `null` 應該是用在物件參考上，所以把 `null` 當成是一個物件。但是它本身的意義就不該屬於任何物件的實體，所以在 `instanceof` 才會是 `false` 。

特殊資料型態
------------

最後的 `undefined` ，會出現在**預期會有明確的值，實際上並沒有明確定義詳細內容**的情況下。

舉幾個例子

```javascript
var x;
```

`x` 被宣告成是變數，預期裡面應該會有明確的值，實際上它並沒有被定義內容為何，所以它會是 `undefined` 。

```javascript
function f() {};
```

`f` 被宣告成是 function ，預期 function 都會有回傳值，實際上它沒有被定義回傳，所以它的回傳會是 `undefined` 。

Reference
---------

* [JavaaScript 語言核心（2）與眾不同的資料型態](http://www.codedata.com.tw/javascript/essential-javascript-data-type/)
