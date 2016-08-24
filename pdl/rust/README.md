Rust
====

Rust 的家世可以查查 [wiki](https://zh.wikipedia.org/wiki/Rust) ，另外跟其他語言的比較也可以參考看看[這篇](https://buzzorange.com/techorange/2015/11/18/which-can-replace-language-c/)

Setup
-----

### Docker + Debian

```dockerfile
FROM debian:jessie

ENV BUILD_DEPS \
        ca-certificates \
        curl \
        file
ENV REQUIRE_DEPS \
        g++ \
        sudo

RUN set -xe && \
        apt-get update -y && apt-get install -y --no-install-recommends --no-install-suggests \
            ${REQUIRE_DEPS} \
            ${BUILD_DEPS} \
        && rm -r /var/lib/apt/lists/* && \
        curl -sSf https://static.rust-lang.org/rustup.sh | sh && \
        apt-get purge -y \
            ${BUILD_DEPS} \
        && rustc --version
```

Quick Start
-----------

先建立檔案 `main.rs`

```rust
fn main() {
    println!("Hello, world!");
}
```

然後下指令編譯

```
rustc main.rs
```

最後就會產生可執行檔，再執行即可

```
$ ./main
Hello, world!
```

References
----------

* [Rust 程式語言正體中文版](http://askeing.github.io/rust-book/)
