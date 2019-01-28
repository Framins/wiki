# Phar

從 PHP 5.3 開始，PHP 也支援打包的功能。Phar 其實指的就是 PHP Archive，功能很類似 JAR。

## Start

有個函式庫是用 composer 開發，但另外一個團隊並沒在用，那簡單一點該如何分享呢？首先先在函式庫的根目錄，建立一個檔案叫 `build.php` ：

```php
#!/usr/bin/env php
<?php
$exts = ['php'];
$dir = __DIR__ . '/';
$file = 'lib.phar';
$phar = new Phar(__DIR__ . '/' . $file, FilesystemIterator::CURRENT_AS_FILEINFO | FilesystemIterator::KEY_AS_FILENAME, $file);

$phar->startBuffering();

foreach ($exts as $ext) {
    $phar->buildFromDirectory($dir, '/\.' . $ext . '$/');
}

$phar->setStub($phar->createDefaultStub('vendor/autoload.php'));
$phar->stopBuffering();

echo "Finished {$file}\n";
```

再來要用指令執行

```
php -d phar.readonly=off /usr/local/bin/phar-composer build.php
```

接著專案目錄下就會看到 `lib.phar` 檔，另一個團隊只要 include 這個檔案即可使用裡面的套件。

## References

* http://www.zendei.com/article/21307.html
