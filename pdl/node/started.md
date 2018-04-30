以下用 [Docker][] 來快速建置環境與練習

可以參考 [Docker Hub](https://hub.docker.com/_/node/) 選擇 Docker image 版本，這裡使用 `node:4.4` 做練習

> 本篇主題是 Node.js ， Docker 的部分不會著墨太多

# HelloWorld

首先先建立 `app.js` 開始寫 HelloWorld 程式

```javascript
console.log("HelloWorld");
```

使用 Docker 去 run 這隻程式：

```bash
docker pull node:4.4
docker run --rm -v `pwd`:/usr/src/app -w /usr/src/app node:4.4 node app.js
```

輸出範例如下

    $ docker run --rm -v `pwd`:/usr/src/app -w /usr/src/app node:4.4 node app.js
    HelloWorld

# HTTP Server

Node.js 有內建基本的 HTTP Server 可以直接使用，程式碼如下：

```javascript
var server;
var ip = "0.0.0.0";
var port = 3000;
var http = require('http');

server = http.createServer(function (req, res) {
  res.writeHead(200, {'Content-Type': 'text/plain'});
  res.end('Hello World\n');
});

server.listen(port, ip);

console.log("Server running at http://" + ip + ":" + port);
```

不過 Docker 只要 run 下去就無法中斷了，目前問題原因還不清楚

可以換進到 Docker bash run ：

```bash
docker run --rm -v `pwd`:/usr/src/app -w /usr/src/app -p 3000:3000 node:4.4 bash

# In docker container
node app.js
```

執行後會出現監聽訊息

    $ node app.js
    Server running at http://0.0.0.0:3000

這時開頁面就可以看到 HelloWorld 了

# NPM

[NPM](https://www.npmjs.com/) 全名為 *Node Package Manager* ，為套件管理工具，類似 [PHP][] 的 [Composer][] 或 [Ruby][] 的 [Gem](https://rubygems.org/)

使用 Docker 初始化 NPM 套件定義檔

```bash
docker run --rm -it -v `pwd`:/usr/src/app -w /usr/src/app node:4.4 npm init -y
```

執行完後，會多一個檔叫 `package.json` 。假如要裝 [Express](http://expressjs.com/) 可以下指令安裝

```bash
docker run --rm -it -v `pwd`:/usr/src/app -w /usr/src/app node:4.4 npm install express --save
```

# NPM Command

上述 Docker 每次執行完之後都會移除 container ，所以如果有裝全域套件的需求時，建議可以使用 *Dockerfile* 安裝

比方說我想要用 `express` 的指令，首先建立一個名為 `Dockerfile` 的檔案：

```dockerfile
FROM node:4.4
RUN npm install -g express-generator
```

然後下指令建 image

```bash
docker build -t=mynode .
```

建完後就可以用 `mynode` 來 run express 了

```bash
docker run --rm -it -v `pwd`:/usr/src/app -w /usr/src/app mynode express
```

## References

* [Docker 指令參考](https://docs.docker.com/engine/reference/run/)
* [node.js 基本教學](http://dreamerslab.com/blog/tw/node-js-basics/)

[Docker]: /docker/README.md
[PHP]: /pdl/php/README.md
[Composer]: /pdl/php/composer.md
[Ruby]: /pdl/ruby/README.md
