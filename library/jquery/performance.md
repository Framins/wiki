# Performance

## Cache Usage

DOM 尋找是很浪費時間的，所以盡量 cache 可以重用的物件：

### Not good

```javascript
h = $('#element').height();
$('#element').css('height', h-20);
```

### Recommend

```javascript
$element = $('#element');
h = $element.height();
$element.css('height', h-20);
```

另外，Cache 父元素後再從父元素裡找子元素，會比直接找子元素來得快。

### Not good

```javascript
var
    $container = $('#container'),
    $containerLi = $('#container li'),
    $containerLiSpan = $('#container li span');
```

### Recommend

```javascript
var
    $container = $('#container '),
    $containerLi = $container.find('li'),
    $containerLiSpan = $containerLi.find('span');
```
