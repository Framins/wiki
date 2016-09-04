Clojure
=======

[Clojure][] 是個強健、實際、快速的程式語言，它運行在 JVM 上，意指它可以用 [Java](/pdl/java/README.md) 的函式庫，並且備跨平台的能力

Setup
-----

### MacOS

Homebrew 懶人安裝法，先裝 [Leiningen][]

    brew install leiningen

接著開啟 REPL

    lein repl

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

[Clojure]: https://clojure.org/
[Leiningen]: https://github.com/technomancy/leiningen
