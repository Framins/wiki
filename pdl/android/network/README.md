# Network

網路操作相關用法。

## 必要權限

如果要有上網的功能，必須加下面的權限：

```xml
<uses-permission android:name="android.permission.INTERNET"/>
```

如果要取得網路連線狀態或種類等網路狀態，必須加下面的權限：

```xml
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
```

## 網路連線

* [HTTP](http.md) - 關於 HTTP 連線操作

## 網路狀態

使用 ConnectivityManager 來取得連線狀態的管理。

```java
// In Activity
ConnectivityManager cm = (ConnectivityManager) getSystemService(Context.CONNECTIVITY_SERVICE);
```

個別判斷 3G 或 Wifi，true 代表有連線，false 就是沒有了：

```java
boolean is3g = cm.getNetworkInfo(ConnectivityManager.TYPE_MOBILE).isConnectedOrConnecting();
boolean isWifi = cm.getNetworkInfo(ConnectivityManager.TYPE_WIFI).isConnectedOrConnecting();
```

取得目前啟用的網路相關狀態，如果目前完全沒有網路的話。如果沒有網路連線會取得 null，所以必需要做 null 的判斷或 Exception ：

```java
NetworkInfo info = cm.getActiveNetworkInfo();
```

info 可以取得的相關資訊：

|  Method  |    |  Description  |
|  ------  | -- |  -----------  |
|  String| getTypeName() | 連線方式，如 WIFI/MOBILE |
|  NetworkInfo.State| getState() | 連線狀態，參考[官網](http://developer.android.com/reference/android/net/NetworkInfo.State.html) |
|  boolean| isAvailable() | 是否可使用 |
|  boolean| isConnected() | 是否已連接 |
|  boolean| isConnectedOrConnecting() | 是否已連接或連線中 |
|  boolean| isFailover() | 連線是否有問題 |
|  boolean| isRoaming() | 是否在漫遊中 |

## 下載檔案

下載實作很麻煩，建議還是用別人寫好的比較好，首推的還是 DownloadManager (需Android 2.3以上)

| Library | Description |
| ------- | ----------- |
| [AndroidQuery](https://code.google.com/p/android-query/wiki/AsyncAPI) | AndroidQuery 裡的子函式，有一個正是下載功能 |
| [AFinal](https://github.com/yangfuhai/afinal) | 子功能 FinalHttp 有下載功能，它是基於 AsyncTask 的實作 |
| [AndroidCommon](https://github.com/Trinea/android-common) | 一些工具，包含下載 |
