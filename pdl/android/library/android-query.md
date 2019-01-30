# Android Query

下載位置

* [Google Code](https://code.google.com/p/android-query/)
* [GitHub](https://github.com/androidquery/androidquery)
* [maven.org](http://search.maven.org/#search%7Cga%7C1%7CAndroid-Query)

官方文件

* [Google Code Wiki](https://code.google.com/p/android-query/wiki/API)

它的目標也跟 jQuery 一樣，Less Code！實現的方法也是使用 Chaining

## Core Concept

它的概念很簡單，就只有一個主要的 class，就叫 AQuery。而它有兩種狀態：`root` 和 `view`。

平常用 Activity 在 new 一個 AQuery 時，它就會是 root。而在用 id 找資源的時候，就會變成 view。

```java
// In Activity
aq = new AQuery(this);

// id(R.id.text) - 取得該 View
// text("Hello") - 設定 text。這裡它應該是用反射去處理的。
aq.id(R.id.text).text("Hello");

// id(R.id.button) - 切換不同的 view
// text("Click Me")
// clicked(this, "buttonClicked") - 設定 listener，使用 method name
aq.id(R.id.button).text("Click Me").clicked(this, "buttonClicked");

aq.id(R.id.image);
if (aq.isExist()) {
    ImageView imageView = aq.getImageView();
    //perform other non-AQuery operations
}
```

而 Fragment 官方建議在 onCreateView 裡初始化 AQuery

```java
@Override
public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
    View view = inflater.inflate(getContainerView(), container, false);             

    aq = new AQuery(getActivity(), view);
    return view;
}
```

官方建議不要把 AQuery 的變數設定為 static

## AsyncAPI

* [官方文件](https://code.google.com/p/android-query/wiki/AsyncAPI)

## Image Loading

* [官方文件](https://code.google.com/p/android-query/wiki/ImageLoading)

### Simple

使用 URL 載入影像，會自動快取在檔案和記憶體。也可以傳入參數決定要如何快取。

```java
aq.id(R.id.image).image("http://www.sample.com/sample.png");

// 檔案大的時候，就不要用 memCache 了
boolean memCache = false;
boolean fileCache = true;
aq.id(R.id.image).image("http://www.sample.com/sample.png", memCache, fileCache);
```

### Down Sampling

有篇文章提到了要做 Downsampling，不然會發生 OOM

http://blog.androidquery.com/2011/05/down-sample-images-to-avoid-out-of.html

```java
// 200 是指 image 的寬（最小/最大）
aq.id(R.id.image1).image("http://www.sample.com/sample.png", true, true, 200, 0);
```
