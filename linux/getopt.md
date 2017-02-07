# `getopt`

當 shell script 需要給一些參數的時候，這一頁的內容就會派上用場了。

## 定義

> 參考 PHP [Symfony Console](http://symfony.com/doc/current/components/console.html) 用法 

首先是參數的形式，通常有兩種：一種為 Option ，另一種為 Argument

Option 通常是 `-` 開頭，如

```
$ ls -a
```

Argument 則沒有，如

```
$ rm /path/to/file
```

根據使用經驗， Option 大多都是 optional 。 Argument 則不一定

### Option

Option 的表示方法又分為兩種，一長一短，如下面兩個都是同一個參數。

```
$ git push --force
$ git push -f
```

Option 的內容則有三種：布林、值、陣列。

**布林**是指有給為 true ，沒給為 false ，如下例兩個就是 true 和 false 的差別

```
$ composer install --no-dev
$ composer install
```

**值**會傳送一個字串給指令處理，如

```
$ php -S 0.0.0.0:8080
```

最後陣列則是同個參數可以重複傳多個字串給指令處理，如

```
$ docker run -p 80:80 -p 443:443 nginx
```

### Argument

比較起來 Argument 相對簡單很多，它只有必填跟選填的差別而已

必填如

```
$ rm /path/to/file
```

選填如

```
$ ls /path/to/file
$ ls
```

### 組合

Option 跟 Argument 亂打的話，有時會讓指令不知道哪個是 Option 哪個是 Argument ，簡單的方法是 Option 先，再 Argument ，中間用 `--` 隔開。以下是一個簡單的範例：

```
$ git diff --name-status ./somefile
$ git diff --name-status -- ./somefile
```

上述兩個例子都可以正常執行，但偶爾還是會出現預期外的結果，這時可以考慮做上面的動作，也許就能正常執行了。

## 寫腳本

上面介紹 Linux 用參數的一些潛規則，現在來看要如何在 shell script 上實現。以下將用 `getopt` 來處理。

Mac 原生的 `getopt` 有點怪，請使用 brew 安裝 GNU 版的 ([參考](http://stackoverflow.com/questions/12152077/how-can-i-make-bash-deal-with-long-param-using-getopt-command-in-mac))：

```
$ brew install gnu-getopt
$ brew link --force gnu-getopt
```

首先 `-o` 參數是定義短的 Option ，後面會接英文字和數個冒號，英文字代表要使用的 option ；後面沒冒號代表是布林；接一個冒號 `:` 代表傳入值是必填，兩個冒號 `::` 代表選填，舉個例子：

```bash
getopt -o a:bc::
```

`-a` 的字串是必填， `-b` 是布林， `-c` 的字串是選填

接著 `--long` 是定義長的 Option ，多個 option 用 `,` 隔開，冒號的規則跟短的是一樣的。

```bash
getopt --long force,volumn:,some-else::
```

這樣表示 `--force` 是布林， `--volumn` 需要參數， `--some-else` 是選填參數。

最後 Script 的範例可以參考最後面的連結。

## References

* [Command Line Options: How To Parse In Bash Using “getopt”](http://www.bahmanm.com/blogs/command-line-options-how-to-parse-in-bash-using-getopt)
