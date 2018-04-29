# Javascript Snippet

## Random

```javascript
var maxNum = 99; // 大數
var minNum = 0;  // 小數

// rand = 0 ~ 99 其中之一
var rand = Math.floor(Math.random() * (maxNum - minNum + 1)) + minNum;
```

## Fluent Interface Pattern 2

跟 JavaScript 一樣是 First-class function 的語言都能這樣玩。

```javascript
var dom1 = {'className': 'dom1'},
    dom2 = {'className': 'dom2'},
    dom3 = {'className': 'dom3'};

var addClass = function(dom, className) {
    dom.className += ' ' + className;
    return addClass;
};

addClass(dom1, 'class1')(dom2, 'class2')(dom3, 'class3');

console.log(dom1);
console.log(dom2);
console.log(dom3);
```
