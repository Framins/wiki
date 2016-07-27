# Zend_View_Helper

* [官方文件](http://framework.zend.com/manual/1.12/en/zend.view.helpers.html)
* [寫自己的helper](http://framework.zend.com/manual/1.12/en/zend.view.helpers.html#zend.view.helpers.custom)

官方內建的 helper

| [Zend_View_Helper_BaseUrl](http://framework.zend.com/manual/1.12/en/zend.view.helpers.html#zend.view.helpers.initial.baseurl) | BaseUrl可以用在讀取static resource |
| [Partial Helper](http://framework.zend.com/manual/1.12/en/zend.view.helpers.html#zend.view.helpers.initial.partial) | 把頁面分區怪 |
| [Zend_View_Helper_ServerUrl](http://framework.zend.com/manual/1.12/en/zend.view.helpers.html#zend.view.helpers.initial) | Server端Url取得 |
| [Zend_View_Helper_Url](http://framework.zend.com/manual/1.12/en/zend.view.helpers.html#zend.view.helpers.initial) | 產生Url |

## Custom Helper

官方說明有提到：「雖然不是必要，但還是建議要實作 `Zend_View_Helper_Interface` 或繼承 `Zend_View_Helper_Abstract` 。」

helper 預設的載入路徑除了內建的 helper 的路徑外，自定義的路徑就是`application/views/helpers`了，前綴一樣都是`Zend_View_Helper`。這些都可以從 View 物件呼叫 setHelperPath() 設定。

```php
// in helpers dir
class Zend_View_Helper_TestCode extends Zend_View_Helper_Abstract {
    public function testCode() {
        echo "test";
    }
}

// in view scripts
$this->testCode();
```

> 注意 `Zend_View_Helper_TestCode` 的 Test 要與 function name: `testCode` 一致。（除了首字大寫）
