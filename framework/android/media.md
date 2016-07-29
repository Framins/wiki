# Media

這裡要記錄的是 Android 要如何處理媒體資料，包括讀和寫。媒體廣泛指的是文字、圖片、聲音、影片等，但這邊還是就以聲音和影片為主，文字和圖片可以參考 TextView 和 ImageView 。

一開始要講的就是官方所提供的[狀態流程圖](http://developer.android.com/reference/android/media/MediaPlayer.html#StateDiagram)和說明。其中藍色的圈圈是狀態(State)，箭頭旁邊的是使用了方法(Method)後會造成狀態的改變。

![](http://developer.android.com/images/mediaplayer_state_diagram.gif)

當開發測試過程中遇到很多 IllegalStateException 時，十之八九就是沒有按照這張圖的規則處理。

## 影片

Android 實現影片播放的方法有兩種：

* VideoView - 實作容易，可控性低。
* SurfaceView - 實作麻煩，可控性強。
