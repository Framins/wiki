# cURL

cURL 是額外模組，需另外安裝並重新啟動 Apache。

```bash
apt-get install php5-curl
service apache2 restart
```

程式部分需先確認是否有安裝 extension。

```php
// 確認 cURL 模組是否有安裝
if (!function_exists('curl_init')) {
  die('Sorry cURL is not installed!');
}
```

## Usage

跟 MySQL 一樣，首先，需要建立 curl 連線；有連線也會有關閉，所以都先寫好

```php
// 初始化
$ch = curl_init();

// 設定、執行連線、取資料等。

// 關閉連線
curl_close($ch);
```

設定的範圍，包括連線 URL、Agent、header、timeout 等，都是可以調整設定的，詳細可以參考[官方網站](http://php.net/manual/en/function.curl-setopt.php)，下面是比較常見的設定：

```php
// 設定要下載的 URL 位置
curl_setopt($ch, CURLOPT_URL, 'https://google.com.tw');

// 設定 HTTP referer (表示從哪連結到目前的網頁，格式也是 URL)
curl_setopt($ch, CURLOPT_REFERER, "https://www.google.com.tw/");

// 設定 User Agent
curl_setopt($ch, CURLOPT_USERAGENT, "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.125 Safari/537.36");

// 回傳訊息是否包含 Header 訊息
curl_setopt($ch, CURLOPT_HEADER, false);

// 如果是 true，curl_exec() 會回傳 string；false 會直接輸出結果
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

// 設定 Timeout (seconds);
curl_setopt($ch, CURLOPT_TIMEOUT, 10);
```

設定完畢後，就可以直接用 `curl_exec()` 取得資料了。

```php
// 因為剛剛有設定 CURLOPT_RETURNTRANSFER 為 true，所以可以把回傳來的 string 再做加工處理
$output = curl_exec($ch);
```

## References

* [用 curl 登入並取值的解](http://disp.cc/b/11-3agL)
* [用 cookie 登入](http://expect7.pixnet.net/blog/post/44130402)
* [如何使用PHP CURL，基礎教學。](http://expect7.pixnet.net/blog/post/36428081-%5B%E7%A8%8B%E5%BC%8F%5D%5Bphp%5D-%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8php-curl%EF%BC%8C%E5%9F%BA%E7%A4%8E%E6%95%99%E5%AD%B8%E3%80%82)
* [用PHP+cURL傳送Request (GET,POST或上傳檔案)至另一個網頁](http://blog.roodo.com/esabear/archives/16358749.html)
* [HTTP參照位址](http://zh.wikipedia.org/wiki/HTTP%E5%8F%82%E7%85%A7%E4%BD%8D%E5%9D%80)
