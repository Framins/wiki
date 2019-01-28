# Drawable

[Drawable](http://developer.android.com/guide/topics/resources/drawable-resource.html) 除了可以在 XML 裡定義，也能在程式裡呼叫 class ，但一般都會在 XML 定義，這樣就能保持良好的重用性和框架結構。

XML 有以下類型，同時也是標籤：

* `<bitmap>` - Android支持 .png .jpg .gif 影像檔，並做一些處理。
* `<nine-patch>` - 它是一個 png 檔，不過它的背景是具有延展性的，通常是做 button 用的
* `<layer-list>` - 它可以把多個 drawable 按照順序層疊起來，通常會用到的是 progressBar
* `<selector>` - 不同的狀態會有不同的圖，也是用在 button 上的。
* `<level-list>`
* `<transition>`
* `<inset>`
* `<clip>`
* `<scale>`
* `<shape>` - 可以用程式來畫基本的圖形。
* `<animation-list>` - 一連串的照片，來達成動畫的效果。

class有以下類型：

* [BitmapDrawable](http://developer.android.com/reference/android/graphics/drawable/BitmapDrawable.html)
* [NinePatchDrawable](http://developer.android.com/reference/android/graphics/drawable/NinePatchDrawable.html)
* [LayerDrawable](http://developer.android.com/reference/android/graphics/drawable/LayerDrawable.html)
* [StateListDrawable](http://developer.android.com/reference/android/graphics/drawable/StateListDrawable.html)
* [TransitionDrawable](http://developer.android.com/reference/android/graphics/drawable/TransitionDrawable.html)
* [ClipDrawable](http://developer.android.com/reference/android/graphics/drawable/ClipDrawable.html)
* [ScaleDrawable](http://developer.android.com/reference/android/graphics/drawable/ScaleDrawable.html)
* [ShapeDrawable](http://developer.android.com/reference/android/graphics/drawable/ShapeDrawable.html)
* [AnimationDrawable](http://developer.android.com/reference/android/graphics/drawable/AnimationDrawable.html)

## Bitmap

Android支援 .png .jpg .gif 三種格式的圖檔，並可以直接使用。

* 檔案位置: res/drawable/filename.png (.png, .jpg, or .gif)
* 資源類別: BitmapDrawable
* 資源參照: R.drawable.filename (in Java) / @[package:]drawable/filename (in XML)

## XML Bitmap

定義一個XML來指向一個Bitmap，然後能加上一些屬性或效果。

* 檔案位置: res/drawable/filename.xml
* 資源類別: BitmapDrawable
* 資源參照: R.drawable.filename (in Java) / @[package:]drawable/filename (in XML)

語法：

```xml
<?xml version="1.0" encoding="utf-8"?>
<bitmap xmlns:android="http://schemas.android.com/apk/res/android"
        android:src="@[package:]drawable/drawable_resource"
        android:antialias=["true" | "false"]
        android:dither=["true" | "false"]
        android:filter=["true" | "false"]
        android:gravity=["top" | "bottom" | "left" | "right" | "center_vertical" |
                          "fill_vertical" | "center_horizontal" | "fill_horizontal" |
                          "center" | "fill" | "clip_vertical" | "clip_horizontal"]
        android:mipMap=["true" | "false"]
        android:tileMode=["disabled" | "clamp" | "repeat" | "mirror"] />
```

* android:src Drawable原始檔，此為**必要屬性**
* android:antialias Boolean，開啟或關閉反鋸齒
* android:dither Boolean
* android:filter Boolean
* android:gravity 關鍵字
* android:mipMap Boolean
* android:tileMode 關鍵字
