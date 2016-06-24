# Started

目標：建立一個最新消息功能，並有基本 CRUD 功能。頁面如下：

* 最新消息列表
* 最新消息內容
* 編輯最新消息
* 搜尋最新消息

下載準備：

1. [下載主程式](http://ellislab.com/codeigniter/download)
2. 解壓並放在網頁的目錄下

## Directory Structure

下載後解壓的目錄如下：

* application/ - 開發程式主要的目錄
  * cache - 快取檔
  * config - 主要設定，包括自動載入、資料庫、 Router 等
  * controllers - Controller 的程式檔
  * core - 當有改寫CI元件的需求時，可以把檔案放在這裡，再使用繼承的方法改寫。
  * error - 當程式出現錯誤時，會出現的畫面，如 404 找不到網頁。
  * helpers - 補助函數，可處理特定任務，它完全是用 function 所撰寫的。
  * hooks - Hook 可在程式執行到核心定義的幾個點時，做指定的動作
  * language - 語系檔
  * libraries - 自定義程式庫
  * logs - 記錄檔
  * models - Model 程式檔
  * third_party - 第三方程式庫
  * views - View 樣版檔
* system/ - CodeIgniter 系統的目錄。如果 CodeIgniter 更新時，只要更新此目錄即可
* index.php - 所有 request 的主要進入口。

## Helloworld

在 controllers 裡新增一個檔案 `news.php`

```php
<?php
class News extends CI_Controller {

    public function index() {
        echo 'Hello World!';
    }
}
```

接著在 Browser 打：

    example.com/index.php/news/

即可出現 Hello World! 字樣。

## URL

[URL](http://www.codeigniter.org.tw/user_guide/general/urls.html) 、 Controller 、 Router 的功能是環環相扣的。主要的目的是在處理 URL 並使用對應的 Controller 來回應 Browser

CodeIgniter 預設的 URL 定義很簡單好懂，它使用分段式的方法

    example.com/index.php/{class name}/{method name}/{params}....

* `class name` controller 的 class name
* `function name` controller 裡的 method name
* `params` 傳入的參數，可以很多個，用斜線分隔

舉實例：

    example.com/index.php/news/edit/3

這在URL上的解釋很明顯表達出「最新消息，編輯 `id=3` 的記錄」的意義。

## Controller

[Controller](http://www.codeigniter.org.tw/user_guide/general/controllers.html) 是處理 request URI 的元件。

修改 Helloworld：

```php
<?php
class News extends CI_Controller {

    public function index() {
        echo 'Hello World!';
    }

    public function edit($id = 0) {
        echo 'Edit News: ' . $id;
    }
}
```

這樣就可以達到 URL 最後實例的效果了。

## Router

[Router](http://www.codeigniter.org.tw/user_guide/general/routing.html) 機制，會先檢查使用者傳入參數是符合哪一個 Controller ，再進行轉向的動作。

Router 的定義在 `application/config/routes.php` 裡：

```php
<?php
$route['default_controller'] = "news";  // 保留的路由名，在未指定 controller 時，會選擇此 controller 。
$route['404_override'] = '';  // 保留的路由名，當找不到網頁的時候會開啟此頁面
$route['news/(:num)'] = "news/view/$1";  // news/4 => news/view/4 (:num 表示的是數字)
$route['news/latest'] = "news/view/28";  // news/latest => news/view/28
$route['news/(:any)'] = "news/search/$1";  // news/text => news/search/text (:any 表示的是所有字)
```

* 右邊 target 的 ''$1'' 指的是：左邊的 pattern 從左邊數起來第一個括號裡匹配的文字
* Router 定義有順序性，先定義的如果符合就會執行，後面的就會全部忽略。
* 承上，所以保留的路由必須要放在最上面。
* 開頭結尾都不能用斜線。

## View

View 可以是一個頁面，或是頁面的一個區塊； View 要由控制器來呼叫並載入頁面資料，首先在 views 資料夾裡新增 `news_list.php` 檔案

```html
<html>
<head>
    <title>最新消息列表</title>
</head>
<body>
    <h1>最新消息列表</h1>
</body>
</html>
```

通常首頁就是顯示列表，所以我們可以在 controllers 裡的 `news.php` 這麼打：

```php
public function index() {
    $this->load->view('news_list');
}
```php

> **Notice:** 不能把 `.php` 加進去，除非不使用 `.php` 的檔案

當然也可以把 View 放到子目錄裡，然後再去載入 View ：

```php
public function index() {
    // view 放在 views/news/ 裡
    $this->load->view('news/list');
}
```

### Pass data

Controller 可以傳送資料給 View

```php
public function index() {
    $data = array(
        'title' => '最新消息列表',
        'heading' => '最新消息列表'
    );

    $this->load->view('news/list', $data);
}
```

View 檔也需要做變動（注意傳入陣列與 View 裡使用的變數差別）：

```html
<html>
<head>
<title><?php echo $title; ?></title>
</head>
<body>
    <h1><?php echo $heading; ?></h1>
</body>
</html>
```

### View in View

View 裡面再次載入 View

```php
public function index() {
    $data = array(
        'title' => '最新消息列表',
        'heading' => '最新消息列表',
        'head_view' => 'news/head'
    );

    $this->load->view('news/list', $data);
}
```

View 檔的變動：

```html
<html>
<head>
<title><?php echo $title; ?></title>
</head>
<body>
    <?php echo $this->load->view($head_view, '', true); ?>
</body>
</html>
```

當然一樣要新增一個 `news/head.php` 檔

```html
<h1><?php echo $heading; ?></h1>
```

## Model

Model 的原型，名稱通常會加個 model ，以避免命名衝突

```php
class News_model extends CI_Model {
    function __construct() {
        parent::__construct();
    }

    function getData() {
        return array('a', 'b', 'c');
    }
}
```

載入的方式

```php
$this->load->model('News_model');

// 後面就可以這樣取得資料
$this->News_model->getData(); // array('a', 'b', 'c')
```

## Database Setting

資料庫的設定檔 `application/config/database.php` ，裡面可以設定資料庫的位址和帳密等資料。通常只會動到下面五個變數

```php
$db['default']['hostname'] = 'localhost';        // 資料庫位址
$db['default']['username'] = 'root';             // 帳號
$db['default']['password'] = '';                 // 密碼
$db['default']['database'] = 'database_name';    // 資料庫名稱
$db['default']['dbdriver'] = 'mysql';            // 伺服器種類
```
