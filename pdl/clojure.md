Clojure
=======

[Clojure][] 是個強健、實際、快速的程式語言，它運行在 JVM 上，意指它可以用 [Java](/pdl/java/README.md) 的函式庫，並且備跨平台的能力

Setup
-----

### MacOS

Homebrew 懶人安裝法，先裝 [Leiningen][]

```
$ brew install leiningen
```

接著就能開啟 REPL 了，使用 exit 離開

```
$ lein repl
...
user=> exit
Bye for now!
```

也可以使用 new 來產生新專案

```
$ lein new clojure-practice
```

Hello World
-----------

啟動後輸入下面字串即可 Say Hello 了

```
user=> (def hello (fn [] "Hello world"))
#'user/hello
user=> (hello)
"Hello world"
user=>
```

運算
----

加法函數 `(+)` 可以接受任何數值，然後回傳它們的加總。當沒有傳的時候會回傳 0 ：

```
user=> (+)
0
user=> (+ 1)
1
user=> (+ 1 2)
3
user=> (+ 1 2 3) 
6
user=> (+ 1 2 3 4) 
10 
```

[Clojure]: https://clojure.org/
[Leiningen]: https://leiningen.org/
