# WebView

[WebView](http://developer.android.com/reference/android/webkit/WebView.html) 比較特別，是繼承 [AbsoluteLayout](http://developer.android.com/reference/android/widget/AbsoluteLayout.html) 這個已經 Deprecated 的類。它也沒有特別的 XML 屬性，只有一堆 Method 可以操作它的內容。

它的功能主要就是使用 Webkit 引擎載入網頁並顯示。

## Basic Usage

首先是 XML 定義

```xml
<WebView
    android:id="@+id/webView"
    android:layout_width="match_parent"
    android:layout_height="match_parent" />
```

WebView 功能就是載入網頁，所以只要有網址就能使用。

```java
WebView webView = (WebView) findViewById(R.id.webView);
webView.loadUrl("http://www.example.org/");
```

載入 String 構成的網頁

```java
WebView webView = (WebView) findViewById(R.id.webView);
String html = "html code";
mWebView.loadDataWithBaseURL("", html, "text/html","utf-8", "");
```

如果需要讀取本機檔案的話，需要加上 Setting

```java
WebSettings websettings = webView.getSettings();
websettings.setAllowFileAccess(true);
```

## WebView FAQ

WebView 基於 Web，所以問題自然就很多...

### How to set background to transparent

基本上，在 Layout 設定 background 是無效的，要在 java 裡設定

```java
mWebView = (WebView) rootView.findViewById(R.id.webView);
mWebView.setBackgroundColor(0);
```

Android 4.0 以上也許會失效

* 實測[HTC EVO 3D](http://www.eprice.com.tw/mobile/intro/4205/htc-evo-3d/) + 4.0.3無效
* [Asus PadFone Infinity](http://www.eprice.com.tw/mobile/intro/4717/asus-padfone-infinity-a80-64gb/) + 4.1.2成功

而成功的機型，在滑動時會出現黑色的閃爍現象；這都是因為開硬體加速的關係，關掉即可。

在 Layout 的 WebView 標籤加入下面的屬性：

```
android:layerType="software"
```

或是在 AndroidManifest.xml 的 Activity 標籤加入下面的屬性：

```
android:hardwareAccelerated="false"
```

### WebView in ScrollView

當 WebView 超出 ScrollView 時，點 WebView 後，會出現亂跳的現象。遇到這個問題，在 Layout 的 WebView 標籤加入下面的屬性即可

```
android:focusableInTouchMode="false"
```

### Enable Overview Mode

Overview Mode 是所謂的概觀模式，也就是一開 WebView 就會顯示全部頁面的內容，要放大才能看到細節。

需要呼叫兩個 Method `setUseWideViewPort(true)`、`setLoadWithOverviewMode(true)`

```java
WebSettings websettings = wv.getSettings();
websettings.setSupportZoom(true);
websettings.setUseWideViewPort(true);
websettings.setLoadWithOverviewMode(true);
```

### Load Asset or Drawable File

讀 Assets 的方法：

    mWebView.loadDataWithBaseURL("file:///android_asset/", "<img src='file.jpg' />", "text/html", "utf-8", null);

讀 Drawable 的方法

    mWebView.loadDataWithBaseURL("file:///android_res/drawable/", "<img src='file.jpg' />", "text/html", "utf-8", null);
