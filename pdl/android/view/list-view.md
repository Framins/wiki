# ListView

* [官方文件](http://developer.android.com/reference/android/widget/ListView.html)\\
* [說明](http://4789781.blog.51cto.com/4779781/1186653)

## Extends Structure

* java.lang.Object
  * android.view.View
    * android.view.ViewGroup
      * android.widget.AdapterView<T extends android.widget.Adapter>
        * android.widget.AbsListView
          * android.widget.ListView

## XML Attributes

| Attribute Name | Related Method | Description |
| -------------- | -------------- | ----------- |
| android:divider | | |
| android:dividerHeight | | |
| android:entries | | |
| android:footerDividersEnabled | | |
| android:headerDividersEnabled | | |

## Adapter

ListView 的 setAdapter 是接 [ListAdapter](http://developer.android.com/reference/android/widget/ListView.html)。依實作簡單到困難的順序為：

1. ArrayAdapter
2. SimpleAdapter
3. BaseAdapter
4. ListAdapter

## Third-Party Library

* [XListView](https://github.com/Maxwin-z/XListView-Android) - 下拉更新、滑到底載入的ListView

ListView FAQ
------------

### Performance

AbsListView 的性能大部分都會卡在 getView() 上，所以從修改 getView 的寫法是最直接可以增進效能的方法。

```java
// Using ViewTag

@Override
public View getView(final int position, View convertView, ViewGroup parent) {
    ViewHolder holder;

    // 取得子項目的ViewGroup
    if (convertView == null) {
        convertView = LayoutInflater.from(getApplicationContext()).inflate(R.layout.list_item, null);

        // 取得底下的View
        holder = new ViewHolder();
        holder.title = (TextView) convertView.findViewById(R.id.title);
        holder.desc = (TextView) convertView.findViewById(R.id.desc);
        convertView.setTag(holder);
    } else {
        holder = (ViewHolder) convertView.getTag();
    }

    // 取得對應的Data
    DataObject data = getItem(position);

    // 設定資料
    holder.title.setText(data.title);
    holder.desc.setText(data.desc);

    return convertView;
}

class ViewHolder {
    TextView title;
    TextView desc;
}
```


參考: http://blog.csdn.net/zuolongsnail/article/details/7197979

---

### 如何把每個項目設定相同的高度

通常，ImageView 都會設定固定長寬，然後再配合 AndroidScaleType 調整圖片縮放即可；會有這個要求，十之八九都是因為文字的關係。所以調整文字固定一行+自動滾動即可。

```
android:singleLine="true"
android:ellipsize="marquee"
android:marqueeRepeatLimit="marquee_forever"
```
