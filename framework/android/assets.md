# Assets

資源，常見的就是如圖片、聲音、影片等；比較特別可能還會有 SQL 、 TXT 、 CVS 等純文字檔。

## 圖片匯入

[Android Studio](/editors/ide/android-studio) 內建匯入圖片功能，叫 Asset Studio。

執行方法為：按 Alt+1 叫出 Project 目錄，然後在 res 目錄上點右鍵 -> New -> Image Asset 即可叫出影像資源匯入的對話盒。

`Asset Type` 是選這個圖片是什麼類型

`Launcher Icons` 是做安裝好程式後，在App清單裡會出現的圖片是長什麼樣的。

`Foreground` 要選的是前景圖的來源：

* `Image` 是選擇圖檔，下面就會是`Image file`，要你選圖檔來源
* `Clipart` 有點像是Office系列的美工圖案，也就是可以用內建圖來做點顏色改變
* `Text` 純文字
* `Trim surrounding blank space` 會用放大的方法把旁邊的留白填滿

`Additional padding` 很明顯的就是要加 padding

`Foreground scaling` 是控制它的放大縮小要到什麼程度， Crop 可能會裁掉一點， Center 是會置中顯示全部。

`Shape` 背景的圖檔。

Color 就只是 Color 而已，當選 `Clipart` 或 `Text` 時，會雬要選 `Foreground color` 。

因為是 Launcher 的圖，所以檔名是固定的，這邊就不需要在打 `Resource name` 了。

這裡是做 ActionBar 和 TabIcons 的，所以圖案會變成純色。上面選項都差不多，不過下面變成要選 `Theme` 和 `Resource name` 。

`Notification icons` 是做通知列的Icon，它會分別產生v11和預設的，因為通知列的底色不同。

當然 Android Studio 這些功能其實都還算是基本而已，有人針對這部分做了一個可以產圖的程式： [Android Asset Studio](http://android-ui-utils.googlecode.com/hg/asset-studio/dist/index.html)。裡面除了上面提到的功能外，還有其他延伸功能。
