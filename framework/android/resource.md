# Resource

Android 資源分為以下幾種：

  * Animation Resources

Define pre-determined animations.
Tween animations are saved in res/anim/ and accessed from the R.anim class.
Frame animations are saved in res/drawable/ and accessed from the R.drawable class.

  * Color State List Resource

Define a color resources that changes based on the View state.
Saved in res/color/ and accessed from the R.color class.

  * Drawable Resources

Define various graphics with bitmaps or XML.
Saved in res/drawable/ and accessed from the R.drawable class.

  * Layout Resource

Define the layout for your application UI.
Saved in res/layout/ and accessed from the R.layout class.

  * Menu Resource

Define the contents of your application menus.
Saved in res/menu/ and accessed from the R.menu class.

  * String Resources

Define strings, string arrays, and plurals (and include string formatting and styling).
Saved in res/values/ and accessed from the R.string, R.array, and R.plurals classes.

  * Style Resource

Define the look and format for UI elements.
Saved in res/values/ and accessed from the R.style class.

  * More Resource Types

## Tools Attributes

[Tools Attributes](http://tools.android.com/tech-docs/tools-attributes) 也是一個命名空間，不過在編譯打包過程中，並不會把 tools 命名空間的部分打包進去；它的作用主要就是在協助開發過程。

### tools:ignore

### tools:targetApi

### tools:locale

### tools:context

這個屬性通常是設定在 Layout XML 的根元素，它的值會是 Activity 。設定了之後， IDE 會把此 Layout 跟設定的 Activity 建立關聯。這時，因 Activity 的主題都是在 AndroidManifest.xml 定義， IDE 有了關聯後， Layout Editor 就會自動設定成該 Activity 的 Theme 。

它的值跟 AndroidManifest.xml 一樣可以用 `.` 代表 package 。

Example:

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
              xmlns:tools="http://schemas.android.com/tools"
              android:layout_width="match_parent"
              android:layout_height="match_parent"
              tools:context=".MainActivity">
</LinearLayout>
```
### tools:layout

### tools:listitem / listheader / listfooter

### Designtime Attributes

# String

如果遇到兩個以上的 `%` 可能需要用 `\u0025` 再用 utf8 解碼才行

http://stackoverflow.com/questions/9386411/escape-multiple-characters-in-android
