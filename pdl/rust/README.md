Rust
====

Rust 的家世可以查查 [wiki](https://zh.wikipedia.org/wiki/Rust) ，另外跟其他語言的比較也可以參考看看[這篇](https://buzzorange.com/techorange/2015/11/18/which-can-replace-language-c/)

Setup
-----

### Mac

使用 Homebrew 安裝

```
brew update
brew install rust

# Install completion
brew install rust-completion
brew install cargo-completion
```

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

Cargo
-----

Cargo 是一個類似 Composer / NPM 的套件管理工具，同樣具備開發新專案的功能

比方說官方網站的範例是建一個 `guessing_game` 專案，可以這樣下指令

```
$ cd ~/projects
$ cargo new guessing_game --bin
```

其中 `cargo new` 是指建立新專案， `--bin` 是指要直接產生可執行檔，因為打算定義這是一個專案，而不是函式庫

接著裡面會產生兩個檔案，一個是專案的描述檔 `Cargo.toml` ，另一個是 HelloWorld 原始碼 `src/main.rs` 。進到專案目錄後再下 `cargo build` 會開始編譯，並產生執行檔；下 `cargo run` 會編譯並執行：

```
$ cargo build
   Compiling practice-02-guessing-game v0.1.0 (file://path/to/projects/guessing_game)
$ cargo run
     Running `target/debug/guessing_game`
Hello, world!
```

References
----------

* [Rust 程式語言正體中文版](http://askeing.github.io/rust-book/)

[Composer]: /pdl/php/composer.md
[NPM]: /pdl/node/README.md
