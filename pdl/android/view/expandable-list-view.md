# ExpandableListView

[ExpandableListView](http://developer.android.com/reference/android/widget/ExpandableListView.html) 是可以兩層展開的 ListView ，可以用在兩層資料的呈現。

## Extends Structure

* java.lang.Object
  * android.view.View
    * android.view.ViewGroup
      * android.widget.AdapterView<T extends android.widget.Adapter>
        * android.widget.AbsListView
          * android.widget.ListView
            * android.widget.ExpandableListView

## XML Attributes

| Attribute Name | Related Method | Description |
| -------------- | -------------- | ----------- |
| android:childDivider | | |
| android:childIndicator | | |
| android:childIndicatorEnd | | |
| android:childIndicatorLeft | | |
| android:childIndicatorRight | | |
| android:childIndicatorStart | | |
| android:groupIndicator | | |
| android:indicatorEnd | | |
| android:indicatorLeft | | |
| android:indicatorRight | | |
| android:indicatorStart | | |

## Adapter

ExpandableListView 要使用 setAdapter(ExpandableListAdapter) 接資料

> 雖然 ExpandableListView 是繼承 ListView，不過當 ExpandableListView 執行 setAdapter(ListAdapter) 時，會出現 Error。

BaseExpandableListAdapter 說明：

```java
public class MyExpandableListAdapter extends BaseExpandableListAdapter
{
    /**
     * 取得群組的總數
     */
    @Override
    public int getGroupCount()
    {
        // TODO: 計算群組的大小後回傳
        return 0;
    }

    /**
     * 取得子項目的總數
     */
    @Override
    public int getChildrenCount(int groupPosition)
    {
        // TODO: 計算子項目的大小後回傳
        return 0;
    }

    /**
     * 取得群組的物件
     */
    @Override
    public Object getGroup(int groupPosition)
    {
        // TODO: 回傳群組物件
        return null;
    }

    /**
     * 取得子項目的物件
     */
    @Override
    public Object getChild(int groupPosition, int childPosition)
    {
        // TODO: 回傳子項目物件
        return null;
    }

    /**
     * 取得群組的 ID
     */
    @Override
    public long getGroupId(int groupPosition)
    {
        // TODO: 回傳群組的 ID
        return groupPosition;
    }

    /**
     * 取得子項目的 ID
     */
    @Override
    public long getChildId(int groupPosition, int childPosition)
    {
        // TODO: 回傳子項目的 ID
        return childPosition;
    }

    /**
     * 回傳的 ID 是否穩定，如果用 position 當 id，就是不穩定的，如果有唯一的 id 那就是穩定了；通常是用在重新整理內容的時候用的
     */
    @Override
    public boolean hasStableIds()
    {
        return false;
    }

    /**
     * 取得群組的 View
     */
    @Override
    public View getGroupView(int groupPosition, boolean isExpanded, View convertView, ViewGroup parent)
    {
        if (convertView == null) {
            LayoutInflater inflater = LayoutInflater.from(getApplicationContext());
            convertView = inflater.inflate(R.layout.expandable_list_group_view, null);
        }

        return convertView;
    }

    /**
     * 取得子項目的 View
     */
    @Override
    public View getChildView(int groupPosition, int childPosition, boolean isLastChild, View convertView, ViewGroup parent)
    {
        if (convertView == null) {
            LayoutInflater inflater = LayoutInflater.from(getApplicationContext());
            convertView = inflater.inflate(R.layout.expandable_list_child_view, null);
        }

        return convertView;
    }

    /**
     * 子項目是否可選
     */
    @Override
    public boolean isChildSelectable(int groupPosition, int childPosition)
    {
        return false;
    }
}
```

## How to use OnItemLongClickListener

在看文檔時，會發現它的 Listener 有新增 setOnChildClickListener 和 setOnGroupClickListener ，可是就是沒有 LongClickListener 。

事實上是有辦法解決的，一樣要用 OnItemLongClickListener

```java
exListView.setOnItemLongClickListener(new OnItemLongClickListener() {
    @Override
    public boolean onItemLongClick(AdapterView<?> parent, View view, int position, long id) {
        int itemType = ExpandableListView.getPackedPositionType(id);

        if (itemType == ExpandableListView.PACKED_POSITION_TYPE_CHILD) {
            // 子項目被長按的時候
            childPosition = ExpandableListView.getPackedPositionChild(id);
            groupPosition = ExpandableListView.getPackedPositionGroup(id);

            return true;
        } else if(itemType == ExpandableListView.PACKED_POSITION_TYPE_GROUP) {
            // 群組被長按的時候
            groupPosition = ExpandableListView.getPackedPositionGroup(id);

            return true;
        } else {
            return false;
        }
    }
});
```

References
----------

* [參考網頁](http://stackoverflow.com/a/9950723)
