Lapis
=====

[`Lua`](/pdl/lua/README.md) `Micro Framework`

[Lapis][] 的效能評則比 [PHP](/pdl/php/README.md) 和 [Node](/pdl/node/README.md) 都來得高，試玩看看

Setup
-----

### Mac

使用 brew ，預設會裝 5.2 ，但 lapis 相依於 5.1

    brew install lua51

因為裝 lua51 後，指令都會有 `5.1` 的 suffix 很煩，所以以下是建 alias 解決

```bash
# Lua 5.1 Alias
alias lua="lua5.1"
alias luac="luac5.1"
alias luarocks-admin="luarocks-admin-5.1"
alias luarocks="luarocks-5.1"
```

用 Lua package manager - [LuaRocks](https://luarocks.org/) 安裝相關套件

    luarocks install lapis

其中因為 lapis 相依 luacrypto 套件，而 luacrypto 套件又相依 openssl 套件， openssl 可以用 brew 安裝

    brew install openssl

安裝的時候 luarocks 預設會在 `/usr/local` 裡面找相依套件，但 brew 是放在 `/usr/local/Cellar/` 裡，不過還好可以用環境變數來指定套件位置，如

    luarocks install luacrypto OPENSSL_DIR=/usr/local/Cellar/openssl/1.0.2h_1/

Hint: 到此 Lapis 的部分就算安裝完成了，只是還要另外去裝 OpenResty 待補完 ...

### Docker

參考 https://github.com/MilesChou/docker-lapis

```dockerfile
FROM debian:jessie

RUN apt-get update -y && apt-get install -y \
        build-essential \
        ca-certificates \
        git-core \
        libpcre3-dev \
        libssl-dev \
        lua5.1 \
        luarocks \
    && rm -r /var/lib/apt/lists/*

# Lapis
RUN luarocks install lapis
```

Hint: 同上

Startup
-------

它可以用 [MoonScript](http://moonscript.org/) 轉 Lua 或直接用 Lua 原生程式碼

Note: 葡萄牙語中， Lua 是月亮的意思，所以 MoonScript 的命名應該是這樣來的

References
----------

[Lapis]: http://leafo.net/lapis/
