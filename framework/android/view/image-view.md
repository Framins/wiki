# ImageView

[ImageView](http://developer.android.com/reference/android/widget/ImageView.html) 為基本的圖片物件。

## Extends Structure

* java.lang.Object
  * android.view.View
    * android.widget.ImageView

## XML Attributes

| Attribute Name | Related Method | Description |
| -------------- | -------------- | ----------- |
| android:adjustViewBounds | setAdjustViewBounds(boolean) | 在調整 ImageView大小 時，可以保持長寬比 |
| android:baseline | setBaseline(int) | |
| android:baselineAlignBottom | setBaselineAlignBottom(boolean) | |
| android:cropToPadding | setCropToPadding(boolean) | |
| android:maxHeight | setMaxHeight(int) | |
| android:maxWidth | setMaxWidth(int) | |
| [android:scaleType](#android:scaleType) | setScaleType(ImageView.ScaleType) | 調整圖片縮放的方式 |
| android:src | setImageResource(int) | |
| android:tint | setColorFilter(int,PorterDuff.Mode) | |

### android:scaleType

圖片在放大縮小時，可以使用此屬性決定它的方式和位置。必須是下列其中一個值。

| Constant | Value | Description |
| -------- | ----- | ----------- |
| matrix | 1 | 用 matrix 來繪製 |
| fitXY | 2 | 圖片按照指定的大小在 View 中顯示，拉伸顯示圖片，不保持原比例填滿 View |
| fitStart | 3 | 圖片按比例擴大/縮小到 View 的寬度，顯示在 View 的上部分位置 |
| fitCenter | 4 | 圖片按比例擴大/縮小到 View 的寬度，居中顯示 |
| fitEnd | 5 | 圖片按比例擴大/縮小到 View 的寬度，顯示在 View 的下部分位置 |
| center | 6 | 按圖片的原來大小居中顯示，當圖片長/寬超過 View 的長/寬，則截取圖片的居中部分顯示 |
| centerCrop | 7 | 按比例擴大圖片的 size 居中顯示，使得圖片長/寬等於或大於 View 的長/寬 |
| centerInside | 8 | 將圖片的內容完整居中顯示，通過按比例縮小或原來的 size 使得圖片長/寬等於或小於 View 的長/寬 |

## Third-Party Library

通常 ImageView 的第三方函式庫都是在手勢或載入上做文章。

|  Library  |  Description  |  Links  |
|  -------  |  -----------  |  -----  |
| [Android Query](https://code.google.com/p/android-query/) | | |
| [Android Smart Image View](http://loopj.com/android-smart-image-view/) | | |
| [Android Universal Image Loader](https://github.com/nostra13/Android-Universal-Image-Loader) | | |
| [PhotoView](https://github.com/chrisbanes/PhotoView) | 雙指放大縮小、雙擊放小縮小。原始碼有內帶一個搭配 pager 的範例 | [Sample](https://play.google.com/store/apps/details?id=uk.co.senab.photoview.sample) |
| [GestureImageView](https://github.com/jasonpolites/gesture-imageview) | 提供多種手勢，如雙指放大縮小、雙擊放大縮小等。原始碼內帶範例。它的問題點在：當使用 setBitmap() 時，在放大縮小時會有跳動的情況發生，但使用 xml 定義的圖檔就不會有問題.... | |
