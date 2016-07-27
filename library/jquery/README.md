# jQuery

好用好學的 library

## API

記錄 API 的使用經驗

* [API Documentation](http://api.jquery.com/)

### .animate()

[官方說明](http://api.jquery.com/animate/)

`.animate()` 可以建立基於可量化的 CSS 屬性所構成的動畫，如 `width` ， `height` etc 。

animate() 原型，詳細用法參考官網：

    .animate(properties [, duration] [, easing] [, complete])

* properties ，必要，動畫屬性
* duration ，動畫時間
* easing ，動畫 easing 類型
* complete ，當動畫結束後，會執行的 callback function 。

動畫會移動捲軸到上面 30px 的範例：

```javascript
$("html,body").animate({
    scrollTop: 30
}, 5000, function() {
    // 動畫結束會做的事
});
```

> `scrollTop: 30` 指的是捲軸從最上面開始，往下拉 `30px` ，也就是這個捲軸會影響的區塊，最終上面會有 `30px` 的空間是看不到的

## .offset()

[官方說明](http://api.jquery.com/offset/)

`.offset()` 可取得目前元素的座標，它會回傳一個 `Object` 裡面包含了兩個元素 `top` 和 `left`

<WRAP center round tip 60%>
可見的元素才能取得座標，如果元素有被設定 `visibility:hidden` 或 `display:none` 就無法取得座標
</WRAP>

Example

```javascript
var offset = $("#target").offset();
alert("Left: " + offset.left ", Top: " + offset.top);
```

`.offset()` 也可以傳入一個座標值，它會設定座標給該元素，如：

```javascript
$("#target").offset({ top: 10, left: 30 });
```

## Else

* [Performance](performance.md)

也有其他語言模仿它的設計模式，也寫出其他語言的函式庫

* [phpQuery](https://code.google.com/p/phpquery/)
* [Android Query](https://code.google.com/p/android-query/)
