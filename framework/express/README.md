Express
=======

[Express](http://expressjs.com/)

Setup
-----

安裝 Express 指令

    npm install express-generator -g

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
