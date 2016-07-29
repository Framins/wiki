# Layout

預設最外層的 Screen 是屬於 VerticalArrangement 排版。裡面可以加上其他不同的排列方法，進而達到排版的效果。

## HorizontalArrangement

橫向排列的容器，裡面的可以放其他元件，不過排列規則就是一個接著一個。

> 與原生 LinearLayout 加上 `orientation="horizontal"` 屬性相同。

### Properties

| Name | Value | Description |
| ---- | ----- | ----------- |
| AlignHorizontal | Left/Center/Right | 內部元件水平對齊的方向。與原生 LinearLayout 使用 gravity 屬性，設定成 left/center_horizontal/right 相同。 |
| AlignVertical | Top/Center/Bottom | 內部元件水平對齊的方向。與原生 LinearLayout 使用 gravity 屬性，設定成 top/center_vertical/bottom 相同。 |
| Visible | Showing/hidden | 顯示或隱藏。與原生 View 使用 visibility 屬性，設定成 visible/gone 相同。 |
| Width | Automatic/Fill parent/Custom | 容器的寬度。當選 Automatic 時， AlignHorizontal 會失效。 |
| Height | Automatic/Fill parent/Custom | 容器的高度。當選 Automatic 時， AlignVertical 會失效。 |

## TableArrangement

表格形式的容器。

> 與原生的 GridLayout 比較像

### Properties

| Name | Value | Description  |
| ---- | ----- | -----------  |
| Columns| Integer | 欄數。與原生 GridLayout 的 columnCount 屬性相同。 |
| Rows | Integer | 列數。與原生 GridLayout 的 rowCount 屬性相同。 |
| Visible | Showing/hidden | 顯示或隱藏。與原生 View 使用 visibility 屬性，設定成 visible/gone 相同。 |
| Width | Automatic/Fill parent/Custom | 容器的寬度 |
| Height | Automatic/Fill parent/Custom | 容器的高度 |

## VerticalArrangement

直向排列的容器，與 HorizontalArrangement 一樣，不過是直向的。

> 與原生 LinearLayout 加上 `orientation="vertical"` 屬性相同。

### Properties

| Name | Value | Description  |
| ---- | ----- | -----------  |
| AlignHorizontal | Left/Center/Right | 內部元件水平對齊的方向。與原生 LinearLayout 使用 gravity 屬性，設定成 left/center_horizontal/right 相同。 |
| AlignVertical | Top/Center/Bottom | 內部元件水平對齊的方向。與原生 LinearLayout 使用 gravity 屬性，設定成 top/center_vertical/bottom 相同。 |
| Visible | Showing/hidden | 顯示或隱藏。與原生 View 使用 visibility 屬性，設定成 visible/gone 相同。 |
| Width | Automatic/Fill parent/Custom | 容器的寬度。當選 Automatic 時， AlignHorizontal 會失效。 |
| Height | Automatic/Fill parent/Custom | 容器的高度。當選 Automatic 時， AlignVertical 會失效。 |
