# Layout

主要分和靜態定義和動態程式兩部分說明。

## XML

Android裡有五個主要的排版元件

* FrameLayout
* LinearLayout
* AbsoluteLayout
* RelativeLayout
* TableLayout

### FrameLayout

### LinearLayout

使用 LinearLayout 的時機：

  * 無序列表項目需要設計依比例排列元件時。
  * 需要設計符合多種尺寸的裝置時。

#### XML Attributes

LinearLayout 的 XML 屬性：

| View | Name | Type | Description |
| ---- | ---- | ---- | ----------- |
| LinearLayout | baselineAligned | boolean | 當設定為 false ，可以避免 Layout 去調整子元素的基線 |
| ::: | baselineAlignedChildIndex | R.id | 指定對齊子元素的基線 |
| ::: | divider | Drawable | 設定分格線 |
| ::: | gravity | [R.attr.layout_gravity](http://developer.android.com/reference/android/R.attr.html#layout_gravity) | 設定子元件的對齊方法 |
| ::: | measureWithLargestChild | boolean | 如果是 true 的話，所有子元素的 weight 都會被視為最大尺寸的最小尺寸 |
| ::: | orientation | [R.attr.orientation](http://developer.android.com/reference/android/R.attr.html#orientation) | 設定方向， horizontal 為橫向， vertical 為直向 |
| ::: | weightSum | int | 定義 weight 的總合 |

LinearLayout 子元素可以用的 XML 屬性：

layout_weight 設定的重點：

* 在 layout_width 設置為 fill_parent 的時候， layout_weight 所代表的是你的控件要優先盡可能的大,但這個大是有限度的，即 fill_parent 。
* 在 layout_width 設置為 wrap_content 的時候， layout_weight 所代表的是你的控件要優先盡可能的小,但這個小是有限度的，即 wrap_content 。

### RelativeLayout

使用 RelativeLayout 的時機：

  * 當子元素必需重疊覆蓋時

### TableLayout

使用 TableLayout 的時機很明確，當需要做表格排版時就是用 TableLayout 了。

TextView 不會自動換行，可以在 TableLayout 加入下面的屬性即可：

* `android:shrinkColumns="0,3,4"` 表示0 3 4欄可以伸縮。
* `android:shrinkColumns="*"` 表示所有行可以伸缩。

### GridLayout

> API Level 14+ needed，需使用[android.support.v7](http://developer.android.com/tools/support-library/features.html#v7-gridlayout) 才能支援舊版本。
>
> Gradle build script dependency identifier：
>
> ```com.android.support:gridlayout-v7:18.0.+```

常用屬性

|  View  |  Name  |  Type  |  Description  |
|  ----  |  ----  |  ----  |  -----------  |
| GridLayout | columnCount | int | 設定螢幕分割的欄數，編號從 0 開始 |
| ::: | rowCount | int | 設定螢幕分割的列數，編號從 0 開始 |
| Children View | layout_column | int | 指定 View 要放在哪一欄 |
| ::: | layout_row | int | 指定 View 要放在哪一列 |
| ::: | layout_columnSpan | int | 指定 View 要跨幾個欄 |
| ::: | layout_rowSpan | int | 指定 View 要跨幾個列 |

### 其他

* [Re-usable Layout](http://developer.android.com/training/improving-layouts/reusing-layouts.html)

## JAVA

使用 LayoutInflater 取得 Layout 的方法 [參考](http://blog.csdn.net/zuolongsnail/article/details/6370035)

方法一：

```java
// in Activity
LayoutInflater inflater = LayoutInflater.from(this);  
View layout = inflater.inflate(R.layout.main, null);
```

方法二：

```java
// in Activity
LayoutInflater inflater = getLayoutInflater();  
View layout = inflater.inflate(R.layout.main, null);  
```

方法三：

```java
// in Activity
LayoutInflater inflater = (LayoutInflater) getSystemService(LAYOUT_INFLATER_SERVICE);  
View layout = inflater.inflate(R.layout.main, null);  
```

上面的方法，如果第二個參數傳 null 會被 Android Lint 說有問題，可以參考這篇：

* http://stackoverflow.com/questions/24832497/avoid-passing-null-as-the-view-root-need-to-resolve-layout-parameters-on-the-in
