# ES6

`ES6` 其實就是 `ES2015`

特性記錄如下：

## Rest

如果參數是不固定數量，可以使用此方法處理：

```javascript
function sum(...args) {
  // args is array
  return args.reduce(function(carry, value) {
    return carry + value;
  }, 0);
}

sum(1, 2, 3, 4); // 10
```

> PHP 5.6 也支援此寫法，但名稱不懂

## Spread

這可以把 Array 的值，展開傳入 function ：

```javascript
function f(x, y, z) {
  return x + y + z;
}

// 使用 Spread
f(...[1,2,3]);

// 等價於
f(1, 2, 3);
```

> PHP 5.6 也支援此寫法，但名稱不懂

## References

* https://babeljs.io/learn-es2015/
* http://es6-features.org/
