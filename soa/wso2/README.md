# WSO2

[官網](http://wso2.com/)

官方提供的 [Dockerfiles](https://github.com/wso2/dockerfiles)

## [WSO2 Data Service Server](http://wso2.com/products/data-services-server/)

懶人 Docker 安裝法，[說明網頁](https://github.com/wso2/dockerfiles/tree/master/wso2dss)

首先要有 Java JDK & WSO2 DSS 的執行程式，因為官方版權的關係，需要自行去下載，無法自己打包超級懶人包

準備好了丟到它說明裡提到的指定目錄，下指令即可包好 Docker image

```
./build.sh -v 3.5.0
```

Run 的時候可以用說明提供的方法，也可以直接用 `docker run`，手動 run 的時候記得要開 9443 port

```
docker run -p 9763:9763 -p 9443:9443 --rm -it wso2dss:3.5.0
```

執行完後，會有提示可以進管理介面，有綁定的話直接到 `https://localhost:9443/carbon` 即可

預設管理員帳密 `admin` / `admin`

> 9763 還不知道是做什麼用的
