# 核心概念

> 從 v4.0.0 開始，就不一定要提供設定文件，但取而代之的是，需要了解下面原理。

* Entry
* Output
* Loader
* Plugins

## Entry

這是要告訴 Webpack 說，這一堆程式碼的 `main` 是哪一隻檔案，Webpack 才有辦法從這個檔案找出背後所依賴的其他檔案。

> 類似地概念：大部分的 [PHP](/pdl/php) 框架也可以從 `index.php` 找到背後所有依賴程式；[Go](/pdl/go) 則是 `main.go` 是執行程式的起始點。

設定範例如下：

```javascript
// webpack.config.js

module.exports = {
  entry: './index.js'
};
```

## Output

這項設定則是決定打包出來的檔案要放到哪個目錄，以及如何命名。預設是 `./dist`

```javascript
// webpack.config.js

const path = require('path');

module.exports = {
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  }
};
```

# Loader

Webpack 只管 Javascript 的檔案，所以其他檔案的處理，則是要靠這項設定來處理。

也因為 Webpack 這個特性，於是我們就能 `import` 其他類型的檔案，如：

```javascript
import 'ui/global.scss'
```

Webpack 能解析此語法，並處理 Javascript 與 Scss 的依賴關係。

要了解更清楚的用法，可以參考[官網](https://webpack.js.org/concepts/loaders/)

# Plugin

Plugin 可以用來處理更多「雜務」，如壓縮、最小化、優化等。

要了解更清楚的用法，可以參考[官網](https://webpack.js.org/concepts/plugins/)

# Mode

Webpack 可以透過設定 Mode 參數，來決定優化的方法，不過事實上只有兩個選項：

```
development
production
```
