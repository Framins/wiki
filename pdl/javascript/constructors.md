# Constructors

## Object()

Object 有原生的建構式，不但不比實字定義清楚，而且還會造成一些無法預期的行為。如：

```javascript
var foo = new Object(1); // 它會是 Number object
var bar = new Object('str'); // 它會是 String object
var baz = new Object(true); // 它會是 Boolean object
```

建議還是使用實字定義比較好。

## Array()

同 Object ，但 Array 建構式的行為比較不一樣，也有它的特殊應用，範例如下：

```javascript
var foo = Array(10); // 有 10 個元素的 Array
var bar = Array(5).join('A'); // 產生 4 個 A 的字串： "AAAA" 
```

## RegExp()

RegExp 建構式通常很少使用，比方說要匹配反斜線的樣式如下：

```javascript
var foo = /\\/g;
var baz = new RegExp('\\\\', 'g');
```

使用 `RegExp()` 需要使用跳脫字元，因此常會需要使用 `\\` 來表示反斜線。上例即可看到會更難理解 RegExp ，因此建議還是使用實字會比較好。

除非， Pattern 無法在寫程式的時候決定，才需要使用 `RegExp()`。
