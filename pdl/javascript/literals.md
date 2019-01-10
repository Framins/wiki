# Literals

JavaScript 提供許多實字定義方式，讓程式寫起來更簡單，也更具表達力。

## Object Literals

在 JavaScript 使用實字定義一個 Object 非常簡單，語法如下：

```javascript
var foo = {};

foo.bar = 'some-bar';
foo.baz = function baz() {};
```

Object 下的元素也可以直接先預定義，類似資料結構的 hash table，範例如下：

```javascript
var foo = {
  bar: 'some-bar',
  baz: function baz() {}
}
``` 

## Array Literals

Array 也非常簡單，語法如下：

```javascript
var foo = [];

foo[0] = 'bar';
foo[1] = 'baz';
```

Array 內容也可以先預定義

```javascript
var foo = [
  'bar',
  'baz'
];
```

## Function Literals

Function 也可以用實字定義，詳細可以參考[該文件](function.md)
 
 ```javascript
var foo = function() {};
```

## RegExp Literals

RegExp 實字定義範例如下：

```javascript
var foo = /bar/;
```
