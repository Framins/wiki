# Node.js

用 JavaScript 寫後端應用

以下以 Linux / Mac 系列的系統做測試

* [started](started.md)
* [Babel](babel.md) | ES5 編譯器，想寫 ES6 就需要它幫助轉成 ES5 語法

## Setup

* Compile source ([official download](http://nodejs.org/download/))

### Ubuntu

用 `nvm` 安裝，可以下載並管理多個版本的 node.js

    sudo apt-get install curl  # nvm 需要使用 curl 下載功能
    sudo apt-get install git
    git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
    echo "source ~/.nvm/nvm.sh" >> ~/.bashrc # 設定每次開 terminal 時，都會執行  ~/.nvm/nvm.sh

    # 重開終端機
    nvm install v0.10         # 安裝 0.10.x 最新版
    nvm use 0.10              # 使用目前已安裝的 0.10.x 最新版
    nvm alias default 0.10    # 設定預設的版本號

### Mac

Mac nvm 安裝方法，建議使用 brew 比較簡單

    brew install nvm
    mkdir ~/.nvm
    echo "export NVM_DIR=\"\$HOME/.nvm\"" >> ~/.bash_profile
    echo ". \"\$(brew --prefix nvm)/nvm.sh\"" >> ~/.bash_profile

接著重啟終端機，就可以開始用 nvm 指令了

## Node.js Package Manager

### Using npm in Docker

如果不想為了測試簡單功能而裝 Node 的話，會很好用。但開發環境還是直接裝 nvm 會比較適合

    alias npm="docker run -i -t --rm -v \$PWD:/usr/src/app -w /usr/src/app node:6.3-slim npm"

### Usage

設定好開發環境後，就可以使用 npm 了。全域安裝指令，有時候有的套件有提供 cli 命令，這時可能就需要用到 `-g`

    npm install <package name> -g
    npm install express -g # 像 express 可以用 cli 來產生專案
    express new app

> 測試過，`nvm` + `npm` + `express` 似乎是沒辦法變成 cli 指令，需要再另外裝 `express-generator`，通常是會裝在 `~/.nvm/<version>/bin/express`，再來看要建 ln 還是怎樣的就隨意了。

想安裝 Module for 某個專案的話，需先切換到該目錄下，再使用 `npm install`。這裡不需要加 `-g` 選項

    cd /path/to/project
    npm install express
    # 程式裡可以用 var express = require('express'); 來使用 express 套件

移除全域套件

    npm uninstall <package name> -g

移除專案裡的套件一樣要切換到目錄下

    cd /path/to/project
    npm uninstall

## Packages

* [Vorpal](http://vorpal.js.org/) - CLI Framework
