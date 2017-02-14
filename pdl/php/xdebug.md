# XDebug

[XDebug](http://xdebug.org/) 是 PHP 上一個強大的除錯工具

## Installation

Mac 安裝，使用 Homebrew 即可。但需要注意的是，預設安裝通常是 compiled 的，如果有安裝什麼特別的東西需要重新編譯 PHP 的話，那最好加個 `--build-from-source` 參數重編比較保險。如安裝 PHP 時，有加 `--with-thread-safety` 參數重編 PHP 的話，就必須要加此參數讓 XDebug 也重編：

```
$ brew install php70 --with-thread-safety
$ brew install php70-xdebug --build-from-source
```

## Reference

* [Xdebug 遠端除錯 (Remote Debugging)](http://blog.crboy.net/2012/06/xdebug-remote-debugging.html)
* KCachegrind
