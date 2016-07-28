# Adapter

[Adapter](http://developer.android.com/reference/android/widget/Adapter.html) 是一個 Interface ，也是下面所有類別的最上層父類； AdapterView 所實作出來的子類都需要它協助呈現資料； Adapter 實作出來的東西卻是很常使用；只要是一組資料想要用同一個 layout 顯示，就會需要 Adapter 。

Adapter 是一個介於原始資料和 View 的端口，大概動作如下：

* 資料設定給 Adapter
* Adapter 決定如何設定資料給 AdapterView
* 當資料更新時，需要通知 Adapter 資料同步到 AdapterView
* 當 AdapterView 發生點擊事件時，可以從 Adapter 取得對應資料

## ListAdapter

[ListAdapter](http://developer.android.com/reference/android/widget/ListAdapter.html) 是 ListView 所需要的 Adapter 的最上層介面，平常應該也不會去動用這部分，但還是需要了解。通常都會用 BaseAdapter 實作，而有有需要用進階的功能時，再直接 override 即可。

## BaseAdapter

[BaseAdapter](http://developer.android.com/reference/android/widget/BaseAdapter.html) 初始化時，要怎麼綁定，怎麼設定內容，都是程式裡去決定的，因此 Simple 做不到的加入事件的部分， BaseAdapter 就能解決了。

範例程式碼：

```java
List<DataObject> mData;

class MyAdapter extends BaseAdapter {
    /**
     * 暫存 List 資料的參考
     */
    List<DataObject> list;

    /**
     * 建構子
     */
    public MyAdapter(List<DataObject> list) {
        this.list = list;
    }

    /**
     * 取得資料總數
     */
    @Override
    public int getCount() {
        return mData.size();
    }

    /**
     * 取得某位置資料的物件
     */
    @Override
    public Object getItem(int position) {
        return mData.get(position);
    }

    /**
     * 取得資料的 ID
     */
    @Override
    public long getItemId(int position) {
        return position;
    }

    /**
     * 取得資料在 List 裡 View 該如何呈現
     */
    @Override
    public View getView(int position, View convertView, ViewGroup parent) {
        // 如果convertView是第一次讀取的話，需要先建立
        if (convertView ==null) {
            LayoutInflater inflater = getActivity().getLayoutInflater();
            convertView = inflater.inflate(R.layout.list_item, null);
        }

        // 取得 View 物件
        TextView title = convertView.findViewById(R.id.title);

        // 取得對應位置的資料
        DataObject data = (DataObject) getItem(position)

        // 設定資料
        title.setText(data.getTitle());

        return convertView;
    }
}
```

## ArrayAdapter

[ArrayAdapter<T>](http://developer.android.com/reference/android/widget/ArrayAdapter.html) 初始化時，綁定的對象就是 `Array` ，所以只適用在想在每一個項目裡，顯示單一資料時。

```java
// 假設 DataObject 有 Override toString()
List<DataObject> mData;

// 這行的結果，會把字串放到 R.layout.list_item 的 R.id.title 位置
ListAdapter adapter = new ArrayAdapter<DataObject>(getApplicationContext(), R.layout.list_item, R.id.title, mData);

// id 也可以省略，不過 layout 的 TextView id 就必需設定為 @android:id/text1
ListAdapter adapter = new ArrayAdapter<DataObject>(getApplicationContext(), android.R.layout.simple_list_item_1, mData);
```

Android有提供一些預設的 List Item Layout 可以直接拿來用，也有網友做出 [預覽圖參考](http://www.bcoder.com/java/android-java/different-sytles-to-show-data-in-listview) ：

* [simple_list_item_1](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_1.xml) - 單行文字
  * @android:id/text1
* [simple_list_item_2](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_2.xml) - 兩行文字
  * @android:id/text1
  * @android:id/text2
* [simple_list_item_2_single_choice](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_2_single_choice.xml) - 兩行文字，外加一個核選鍵
  * @android:id/text1
  * @android:id/text2
  * @+id/radio
* [simple_list_item_activated_1](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_activated_1.xml) - 單行文字，帶有 Activated 效果
  * @android:id/text1
* [simple_list_item_activated_2](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_activated_2.xml) - 兩行文字，帶有 Activated 效果
  * @android:id/text1
  * @android:id/text2
* [simple_list_item_checked](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_checked.xml) - 使用 CheckedTextView ，是帶有核選效果的 TextView
  * @android:id/text1
* [simple_list_item_multiple_choice](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_multiple_choice.xml) - 使用 CheckedTextView ，不過是多選
  * @android:id/text1
* [simple_list_item_single_choice](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_list_item_single_choice.xml) - 使用 CheckedTextView ，單選
  * @android:id/text1
* [simple_selectable_list_item](https://android.googlesource.com/platform/frameworks/base/+/master/core/res/res/layout/simple_selectable_list_item.xml) - Selectabled TextView
  * @android:id/text1

也許高手嫌專案寫的 Layout 太簡單的話，可以拿來直接用；初學者也可以看原始碼，參考該如何寫 List Item Layout 。

### Extends ArrayAdapter

ArrayAdapter 很方便，可惜就是只能綁定單一資料。如果想要能綁多筆資料，又不想太麻煩去繼承 [BaseAdapter](#BaseAdapter) 或用 [SimpleAdapter](#SimpleAdapter) 去設 Map ，那就可以考慮這個方案了。

範例程式碼：

```java
class ListItemAdapter extends ArrayAdapter<DataObject>
{
    private static final int LAYOUT = android.R.layout.simple_expandable_list_item_2;

    public ListItemAdapter(Context context, List<DataObject> data)
    {
        super(context, LAYOUT, data);
    }

    @Override
    public View getView(int position, View convertView, ViewGroup parent)
    {
        if (convertView == null) {
            LayoutInflater inflater = getActivity().getLayoutInflater();
            convertView = inflater.inflate(LAYOUT, null);
        }

        DataObject data = getItem(position);

        TextView title = (TextView) convertView.findViewById(R.id.title);
        TextView desc = (TextView) convertView.findViewById(R.id.desc);

        title.setText(data.title);
        desc.setText(data.desc);

        return convertView;
    }
}
```

## SimpleAdapter

[SimpleAdapter](http://developer.android.com/reference/android/widget/SimpleAdapter.html) 初始化時，綁定的是 `List<Map<String, ?>>` ，它可以藉由後面的 from 參數決定從 Map 中拿哪一筆資料； to 參數則是決定要放到 Layout 中哪個 View 。只要是單純設定內容到 Layout 裡，都會適用於 SimpleAdapter ；如果想做設定內容以外的事，如改變顏色、設定按鍵事件等。那就不能用 SimpleAdapter 了。

SimpleAdapter 的建構子如下：

```
SimpleAdapter(Context context, List<? extends Map<String, ?>> data, int resource, String[] from, int[] to)
```

裡面需要的參數：

* context: 上下文
* data: 原始資料
* resource: R.layout 的資源
* from: Map key
* to: 在 R.layout 裡可以找得的 R.id

其中， data 原始資料可以發現， List 裡面的元素是 Map<String, ?> ，所以 from 必需要是 String ，以選到 data 的資料。也因為 value 是不定類別，所以其實可以放其他類別。 from 跟 to 要剛好一個對一個，這樣才能個別對應並設值。

value 也可以是 ImageView 的 src ，需要 Bitmap 或 String (SD卡路徑)

範例程式碼：

```java
List<DataObject> data;
List<Map<String, ?>> adapterList = new ArrayList<Map<String, String>>();

for (DataObjectdata : data) {
    HashMap<String, String> map = new HashMap<String, String>();
    map.put("title", data.getTitle());
    map.put("desc", data.getDesc());
    map.put("img", data,getImg());
    adapterList.add(map);
}

ListAdapter adapter = new SimpleAdapter(
    getApplicationContext(),
    adapterList,
    R.layout.list_item,
    new int[]{"title", "desc", "img"},
    new String[]{R.id.title, R.id.desc, R.id.img},
);
```
