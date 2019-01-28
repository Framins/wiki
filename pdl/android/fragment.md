# Fragment

[Fragment](http://developer.android.com/guide/components/fragments.html) 是 Android 3.0 後的新元件，為的是解決手機平板共存的問題。使用起來跟 Activity 很像，但又有點不大一樣，主要的概念就是 Activity 會去呼叫 Fragment；因此 Activity 與 Fragment 的配合就非常重要了。

* [FAQ](faq.md)

## Template

基本樣版

```java
public class MainFragment extends Fragment {
    private static final String TAG = MainFragment.class.getSimpleName();

    public MainFragment() {}

    /**
     * 用 Resource 取得 View
     */
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container, Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment, container, false);
    }

    /**
     * 初始化 View
     */
    @Override
    public void onViewCreated(View rootView, Bundle savedInstanceState)
    {
        initView(rootView);
        initVars(rootView);
    }

    @Override
    public void onActivityCreated(Bundle savedInstanceState) {
        super.onActivityCreated(savedInstanceState);

        setListener();
        setData();
    }

    protected void initView(ViewGroup rootView) {}
    protected void initVars(ViewGroup rootView) {}
    protected void setListener() {}
    protected void setData() {}
}
```

## FAQ

經典麻煩的問題：

* 由 Activity 建立 Fragment
* Activity 傳值給 Fragment
* 由 Fragment 建立 Fragment
* Menu 控制
* 旋轉螢幕
* 全螢幕

### 建立選單

要在開啟 Fragment 的時候建立選單，就需要在 onCreate 裡多設定 `setHasOptionsMenu(true)`，其他部分就跟 Activity 做法是一樣的：

```java
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setHasOptionsMenu(true);
}

@Override
public void onCreateOptionsMenu(Menu menu, MenuInflater inflater) {
    super.onCreateOptionsMenu(menu, inflater);
    // Create Menu
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    // Listener
    return super.onOptionsItemSelected(item);
}
```

### Fragment 傳值給 Fragment

這應該是最麻煩的，要從一個啟動中的 Fragment 動態傳值給另一個啟動中的 Fragment。

## References

* http://mobile.51cto.com/aprogram-397222_all.htm
* http://andcooker.blogspot.tw/2012/08/android-fragment_24.html
* http://developer.android.com/design/patterns/multi-pane-layouts.html
