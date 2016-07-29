# Theme

Theme 跟 style 很像，不過套用的對象是 Application 或 Activity ，用法也是大同小異。

## 繼承概念

跟大多數的程式設計概念一樣，它也有繼承的概念。如： `Theme.Holo` 是繼承 Theme ， `Theme.Holo.Light` 則是繼承了 `Theme.Holo` 。而 Theme 都是先繼承目前現有的，再去做個別風格的修改。

## Android SDK 內建 Theme

| Theme系列 | 可供使用的Theme | 說明 |
| -------- | ------------- | ---- |
| Theme | @android:style/Theme | 基本（深色） |
| ::: | @android:style/Theme.Dialog | 對話盒 |
| ::: | @android:style/Theme.Panel | 小窗格（背景透明） |
| ::: | @android:style/Theme.NoTitleBar | 沒有 ActionBar |
| ::: | @android:style/Theme.NoTitleBar.Fullscreen | 全螢幕 |
| Theme.Light | @android:style/Theme.Light | 基本（淺色） |
| ::: | @android:style/Theme.Light.Dialog | 對話盒 |
| ::: | @android:style/Theme.Light.Panel | 小窗格（背景透明） |
| ::: | @android:style/Theme.Light.NoTitleBar | 沒有 ActionBar |
| ::: | @android:style/Theme.Light.NoTitleBar.Fullscreen | 全螢幕 |
| Theme.Holo | @android:style/Theme.Holo | Holo（深色） |
| ::: | @android:style/Theme.Holo.Dialog | 對話盒 |
| ::: | @android:style/Theme.Holo.Panel | 小窗格（背景透明） |
| ::: | @android:style/Theme.Holo.NoTitleBar | 沒有 ActionBar |
| ::: | @android:style/Theme.Holo.NoTitleBar.Fullscreen | 全螢幕 |
| Theme.Holo.Light | @android:style/Theme.Holo.Light | Holo（淺色） |
| ::: | @android:style/Theme.Holo.Light.Dialog | 對話盒 |
| ::: | @android:style/Theme.Holo.Light.Panel | 小窗格（背景透明） |
| ::: | @android:style/Theme.Holo.Light.NoTitleBar | 沒有 ActionBar |
| ::: | @android:style/Theme.Holo.Light.NoTitleBar.Fullscreen | 全螢幕 |
| Theme.Translucent | @android:style/Theme.Translucent | 背景透明 |
| ::: | @android:style/Theme.Translucent.NoTitleBar | 沒有 ActionBar |
| ::: | @android:style/Theme.Translucent.NoTitleBar.Fullscreen | 全螢幕 |
