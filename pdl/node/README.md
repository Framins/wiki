Node.js
=======

用 JavaScript 寫後端應用

以下以 Linux/Mac 系列的系統做測試

Setup Development Environment
-----------------------------

安裝方法如下：

* Compile souce ([official download](http://nodejs.org/download/))
* Use nvm

測試用的話，還是用 nvm ，可以下載並管理多個版本的 node.js

    sudo apt-get install curl  # nvm 需要使用 curl 下載功能
    sudo apt-get install git
    git clone https://github.com/creationix/nvm.git ~/.nvm && cd ~/.nvm && git checkout `git describe --abbrev=0 --tags`
    echo "source ~/.nvm/nvm.sh" >> ~/.bashrc # 設定每次開 terminal 時，都會執行  ~/.nvm/nvm.sh

    # 重開終端機
    nvm install v0.10         # 安裝 0.10.x 最新版
    nvm use 0.10              # 使用目前已安裝的 0.10.x 最新版
    nvm alias default 0.10    # 設定預設的版本號

Node.js Package Manager
-----------------------

設定好開發環境後，就可以使用 npm 了
全域安裝指令，有時候有的套件有提供 cli 命令，這時可能就需要用到 `-g`

    npm install <package name> -g
    npm install express -g # 像 express 可以用 cli 來產生專案
    express new app

> 測試過， `nvm` + `npm` + `express` 似乎是沒辦法變成 cli 指令，需要再另外裝 `express-generator` ，通常是會裝在 `~/.nvm/<version>/bin/express` ，再來看要建 ln 還是怎樣的就隨意了。

想安裝 Module for 某個專案的話，需先切換到該目錄下，再使用 `npm install` 這裡不需要加 `-g` 選項

    cd /path/to/project
    npm install express
    # 程式裡可以用 var express = require('express'); 來使用 express 套件

移除全域套件

    npm uninstall <package name> -g

移除專案裡的套件一樣要切換到目錄下

    cd /path/to/project
    npm uninstall

Express Structure
-----------------

下指令就能產生 express 專案目錄：

    express <ProjectName>


專案目錄 `<ProjectName>` 會產生在當前目錄

目錄結構：

* package.json - npm 依賴套件的配置文件，RoR 也有一個類似的東西叫 Gemfile
* app.js - Entry file
* bin/
* public/ - 靜態資源文件，如 js/css
* router/
* views/ - 樣版
* node_modules/ - package.json 裡的 npm 安裝後會放到這裡
  
express 詳細語法：

```
express [options]
Options:
-h, --help
-V, --version 
-e, --ejs (default to jade)
-H, --hogan
-c, --css [less|stylus|compass]
-f, --force 
```
> nvm 安裝 express 的話，除非建 link，不然就需要再加前面的完整目錄，如： `$ ~/.nvm/v0.10.29/bin/express <ProjectName>`
