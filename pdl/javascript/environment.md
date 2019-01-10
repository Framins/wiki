# Environment

JavaScript 除了可以在 Browser上開 Console 測試外，也可以安裝 [JavaScript Shell](https://developer.mozilla.org/en-US/docs/JavaScript/shells) 做簡單的測試，JavaScript Shell 主要是可以做立即、簡單且預期想立即得到結果的實驗等。

## Chrome

打開 Chrome 後，選單 -> 工具 -> 開發人員工具 -> 頁籤選 *Console*，即可開啟 JavaScript Shell 命令列。

## Firefox

打開 Firefox 後，選單 -> 工具 -> 網頁開發者 -> 網頁主控台，即可開啟 JavaScript Shell 命令列。

## node.js

[node.js](http://nodejs.org/) 除了可以開發後端的網頁程式外，也能當做是 JavaScript Shell 做命令式交談。

## Hello World

在命令列上下指令

```javascript
console.log('Hello World');
```

即可看到 Console 顯示了 `Hello Wrold`，並回應了 `undefind`。

Console 的回應是依命令執行的最後結果來做回應，`console.log()` 是沒有定義回傳結果的，所以就會是 `undefind`.
