# Function

Function 應該是 JavaScript 最重要，也最需要被討論的部分了。

## Function 基本使用

function 就如同其他語言所知道的一樣，可以把重覆的行為定義成一個 function，然後透過呼叫 function 即可執行裡面定義的行為，也能藉此達到 code reuse。

```javascript
function f(a, b) {
    console.log(a);
    console.log(b);
}

f(1, 2); // 1, 2
f(1); // 1 undefined
f(); // undefined undefined
f(1, 2, 3, 4); // 1 2
```

這種寫法也稱為「函式宣告式」(function declaration)

## 當 Function 是變數時

從其他語言轉來寫 JavaScript，覺得這個概念超級抽象的，最後還是靠 caterpillar 的這句話點醒：

> 在 JavaScript 中，函式是物件，是 Function 的實例。

實際測試結果如下

    > function f() {}
    undefined
    > f
    [Function: f]
    > typeof f
    'function'
    > f instanceof Object
    true

所以在 JavaScript 裡，函式宣告定義好的 function 也可以像變數一樣地使用，或是指定在某個變數裡並呼叫。用變數呼叫的方法是把變數當成 function name，然後後面加上小括號和引數即可。

```javascript
function add(a, b) {
    return a + b;
}

var addFunction = add;

console.log(add(1, 2)); // 3
console.log(addFunction(1, 2)); // 3
```

### Function Expression (Anonymous Function)

「函式表達式」，或是更廣為人知的「匿名函式」。它能直接指定給變數，這是用函式實字 (Literal) 

```javascript
var addFunction = function(a, b) {
    return a + b;
};

console.log(addFunction(1, 2)); // 3
```

### Named Function Expression

「具名函式表示式」其實就是把函式實字給個名字，不過似乎是只能用在遞迴或除錯的場合。

```javascript
var levelFunction = function level(a) {
    return a == 1 ? 1 : a * level(a-1);
};

console.log(levelFunction(5)); // 120
console.log(level(5)); // ReferenceError: level is not defined
```

事實上，也可以直接建立 Function 實例：

```javascript
var addFunction = new Function('a', 'b', 
    'return a + b'
);

console.log(addFunction(1, 2)); // 3
```

即然 function 可以指定給變數並執行，代表 function 也可以當作其他 function 的引數：

```javascript
function cal(f, a, b) {
    return f(a, b);
}

var addFunction = function(a, b) {
    return a + b;
};

console.log(cal(addFunction, 1, 2)); // 3
```

甚至連 var 都不用，直接傳函式實字，只是這樣的可讀性不一定會比較好：

```javascript
function cal(f, a, b) {
    return f(a, b);
}

console.log(cal(function(a, b) {
    return a + b;
}, 1, 2)); // 3
```

以上範例我們可以知道，函式實字確實可以建立 Function 實例。

我們可以把整個函式實字用小括號括起來，就成了一個 Function 實例的變數；接著在後面加上小括號，就成了不需命名的匿名函式了。

```javascript
// 這在 JavaScript上是合法的，小括號裡面就是一個 Function 實例
(function() {console.log('Anonymous Function')});

// 把上面的 Function 實例看成是一個變數 a，要呼叫 a 就是在變數後面加上小括號即可
// 同理也可以把上面的這個「變數」後面加上小括號，即可呼叫這個 Function 實例
(function() {console.log('Anonymous Function')})();  // Anonymous Function
```

函式宣告與函式實字用起來感覺幾乎是一樣的，但是還是有差異。如，這個是能正常執行的：

```javascript
add(1, 2);
function add(a, b) {
    return a + b;
}
```

這個會噴 `TypeError`，並且會說 add 是 `undefined`。

```javascript
add(1, 2);
var add = function(a, b) {
    return a + b;
}
```

原因是，直譯器載入檔案後，會先處理所有宣告，包括變數宣告和函式宣告，接著才開始執行程式，這就是所謂的變數跟函數的提升(hoisting)，提升是一種可以將變數或函數宣告移到作用域(scope)頂端的行為。

第一個例子因為函式宣告已處理過了，所以可以正常呼叫。

第二個例子因為變數宣告雖然有，可是執行到 `add()` 時，還沒有指定值給 add，因此 add 會是 `undefined`。

但是要注意的是 ES6 的 Class 是無法提升的。

```javascript
'use strict';
new foo(); // ReferenceError: foo is not defined
class foo {}
```

最後，JavaScript 對於 Function 的這些概念，會引發一些問題：

* **函式是物件的一種，所以是不是可以擁有自己的特性？** 答案是 Yes，不過這是屬於 Object 的層面的討論。
* **function 這樣傳來傳去的，那變數要共用的話，該如何解決？** Closure 和 Scope 會來研究這些問題。

## References

* [JavaScript 語言核心（9）不可輕忽的函式基礎](http://www.codedata.com.tw/javascript/essential-javascript-9-function-abc/)
* [JavaScript 語言核心（10）初探一級函式](http://www.codedata.com.tw/javascript/essential-javascript-10-first-class-function/)
* [JavaScript Essence: Function 實例](http://openhome.cc/Gossip/JavaScript/FunctionInstance.html)
* [Hoisting - Glossary](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting) | MDN
* [Classes - Javascript](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Classes#Hoisting) | MDN
