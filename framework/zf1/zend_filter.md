# Zend_Filter

* [官方說明](http://framework.zend.com/manual/1.12/en/zend.filter.html)

Zend_Filter 可以保留重要的文字，並把不重要文字內容取代或是濾除掉。

Zend 內建的 filter：

| Zend_Filter_HtmlEntities | 可把 HTML 需轉譯的字元轉成 HTML 字元 |
| Zend_Filter_Word_UnderscoreToCamelCase | Zend_Filter 轉成 ZendFilter |
| Zend_Filter_Word_CamelCaseToUnderscore | ZendFilter 轉成 Zend_Filter |


## Usage

單獨使用 Filter

```php
$filter = new Zend_Filter_HtmlEntities();

echo $filter->filter($data);
```

連續使用 Filter ，記得會有順序性，先加的會先濾除。下面兩個就是不同結果的範例

```php
$filter1 = new Zend_Filter();

echo $filter->addFilter(new Zend_Filter_HtmlEntities())->addFilter(new Zend_Filter_Alpha())->filter('&&&');

$filter2 = new Zend_Filter();

echo $filter->addFilter(new Zend_Filter_Alpha())->addFilter(new Zend_Filter_HtmlEntities())->filter('&&&');
```
