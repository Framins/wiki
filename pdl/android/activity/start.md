# Activity

從 3.0 開始，Android 官方就建議使用 Fragment 來配合 Acitvity 實作，這樣能有更好的擴充性。

## Template

基本樣版

```java
public class MainActivity extends Activity {
    private static final String TAG = MainActivity.class.getSimpleName();

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        // 有需要強制定義語言時使用。
        Resources res = getResources();
        Configuration conf = res.getConfiguration();
        conf.locale = Config.getInstance(getApplicationContext()).getLanguage();
        res.updateConfiguration(conf, null);

        setContentView(R.layout.activity_main);

        initView();
        initVars();
        setListener();
        setData();
    }

    protected void initView() {}
    protected void initVars() {}
    protected void setListener() {}
    protected void setData() {}
}
```

* `initView()` 初始化 View 的物件。
* `initVars()` 初始化 `setData()` 所要用的變數。
* `setListener()` 設定監聽。
* `setData()` 設定資料。

## Lifecycle

官方有提供一個 Lifecycle 可以參考裡面提到的 Callback 順序 ((Android Developer: [ActivityLifecycle](http://developer.android.com/reference/android/app/Activity.html#ActivityLifecycle)))

{{http://developer.android.com/images/activity_lifecycle.png}}

不過實際上還有幾個 Callback 沒有寫在裡面。最後還是自己做測試比較準確：

* [LifeCycle](lifecycle.md)

## Activity 切換

### 切換效果

Android 2.0 開始新增了一個方法，可以把預設切換的動畫取代：

    public void overridePendingTransition(int enterAnim, int exitAnim)

其中：

* `enterAnim` 是新開的 Activity 進入螢幕時的動畫
* `exitAnim` 是原來的 Activity 離開螢幕時的動畫

動畫需要是 XML 定義的，包括 Android 定義好的 `android.R.anim`

## 傳遞基本參數

## 傳遞序列參數

Bundle 雖然提供了基本參數，但有時還是希望直接傳整個物件，這時就需要實作序列的方法了。

Android 可以使用兩種序列化的方法，[比較](http://my.oschina.net/zhoulc/blog/172163)：

* Serializable
* Parcelable

### Serializable

[教學](http://android.tgbus.com/Android/tutorial/201108/365927.shtml)

### Parcelable

[教學](http://fecbob.pixnet.net/blog/post/35394025)

Parcelable 實現有三個重點：

* writeToParcel 方法。該方法將類的資料寫入外部提供的 Parcel 中
* describeContents 方法。
* 靜態的 Parcelable.Creator 介面，本介面有兩個方法
  * createFromParcel(Parcel in) 實現從 in 中創建出類的實例的功能
  * newArray(int size) 創建一個類型為 T，長度為 size 的陣列
