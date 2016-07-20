# Coding Style

PHP 的領域裡，一般會建議不要自個兒發明一些特殊的 coding style ，最好還是依社群提出來的規則為主，如果特殊需求再做調整。

## Zend Framework Coding Standard

http://framework.zend.com/manual/1.12/en/coding-standard.html

## PHP FIG

[PHP Framework Interop Group](http://www.php-fig.org/)

這個團隊制定了一些 PHP  coding style 的規範，目的是想讓 PHP open source 專案都有共同的 coding style ，以方便大家共同開發維護

參考網頁：

* [關於 PHP FIG Group 所制定的 PSR-0, PSR-1, PSR-2](http://blog.wu-boy.com/2012/07/about-php-fig-group-coding-style-guide/)
* [關於可維護的 PHP 專案：PHP-FIG 的 PSR-0、PSR-1、PSR-2](http://blog.gslin.org/archives/2012/07/23/2928/%E9%97%9C%E6%96%BC%E5%8F%AF%E7%B6%AD%E8%AD%B7%E7%9A%84-php-%E5%B0%88%E6%A1%88%EF%BC%9Aphp-fig-%E7%9A%84-psr-0%E3%80%81psr-1%E3%80%81psr-2/)

### PSR-0 Autoloading Standard

中譯：[PSR-0 Autoloading Standard](http://blog.mosil.biz/2012/08/psr-0-autoloading-standard/)

這份文件定義了檔案、類別、命名空間的命名方式，因為也有提到自動載入，所以同時也會規定檔案該如何存放等。

`PSR-0` 的設計是考慮到 5.2 沒有 namespace 時所留下來的特性，所以才會用底線分隔。當然還是建議用 `PSR-4` 比較好

### PSR-1 Basic Coding Standard

* https://github.com/PizzaLiu/PHP-FIG/blob/master/PSR-1-basic-coding-standard-cn.md

#### PSR-1 概觀

* PHP 程式碼**必須**以 `<?php` 或 `<?=` 標籤開始。
* PHP 程式碼**必須**以 `不帶 BOM 的 UTF-8` 編碼。
* PHP 程式碼中**應該**只定義 `類別` `函數` `常數` ，或其他會產生 `從屬效應` 的操作，兩者只能選其一。
* 命名空間以及類別**必須**符合 PSR 的自動載入規範： PSR-0 或 PSR-4 其中一個。
* 類別命名**必須**遵循 `StudlyCaps` 大寫開頭駝峰命名規範。
* 類別的常數所有字母都**必須**大寫，單字間用底線 `_` 分隔。
* 方法名稱**必須**符合 `camelCase` 式的小寫開頭駝峰命名規範。

### PSR-2 Coding Style Guide

* https://github.com/PizzaLiu/PHP-FIG/blob/master/PSR-2-coding-style-guide-cn.md
* https://github.com/PizzaLiu/PHP-FIG/blob/master/PSR-2-coding-style-guide-meta-cn.md

#### PSR-2 概觀

* 程式碼**必須**遵守 PSR-1 的規範。
* 程式碼**必須**使用 4 個空格，而不是 tab 進行縮排。
* 每行的字數**應該**保持在 80 個字以內，理論上**一定不能**多於 120 個字，但**一定不能**硬性限制。
* 每個 `namespace` 命名空間和 `use` 後面，**必須**插入一個空白行。
* 類別的開始大括號 `{` **必須**寫在類別宣告後獨立一行，結束大括號 `}` 也**必須**寫在類別最後面獨立一行。
* 方法的開始大括號 `{` **必須**寫在方法宣告後獨立一行，結束大括號 `}` 也**必須**寫在方法最後面獨立一行。
* 類別的屬性和方法**必須**加上能見度宣告 (`private` `protected` `public`) ， `abstract` 以及 `final` 宣告**必須**放在能見度宣告之前，而 `static` 宣告**必須**在能見度宣告之後。
* 流程控制的關鍵字之後，**必須**要有一個空白，而呼叫方法或函數的時候，則**一定不能**有空白。
* 流程控制的開始大括號 `{` **必須**寫在跟流程控制同一行，而結束大括號 `}` **必須**寫在最後面獨立一行。
* 流程控制的開始左括號後和結束右括號前，都**一定不能**有空白。

### PSR-3 Logger Interface

* https://github.com/PizzaLiu/PHP-FIG/blob/master/PSR-3-logger-interface-cn.md

### PSR-4 Autoloader

* https://github.com/PizzaLiu/PHP-FIG/blob/master/PSR-4-autoloader-cn.md

## Reference

* [PHP Coding Standard Fixer](http://cs.sensiolabs.org/)

關鍵字：

* 必須 (MUST)
* 一定不能 (MUST NOT)
* 需要 (REQUIRED)
* 將會 (SHALL)
* 不會 (SHALL NOT)
* 應該 (SHOULD)
* 不該 (SHOULD NOT)
* 推薦 (RECOMMENDED)
* 可以 (MAY)
* 可選 (OPTIONAL)

關鍵字的說明參考 [RFC 2119](http://www.ietf.org/rfc/rfc2119.txt)
