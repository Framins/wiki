# build.gradle

Android Studio的build.gradle有分Project(Top-level)和Module；所以Project的一定會被讀取到，但Module的就是個別定義。

[官方教學](http://tools.android.com/tech-docs/new-build-system/user-guide)

## Base Concept

Android project會有三個主要的區塊

  buildscript { ... } // 定義建置的方法
  apply plugin: 'android' // 匯入Android的plugin，從這行開始，下面才可以用android區塊。
  android { ... } // 定義Android建置的內容

## Dependencies

  * compile
  * androidTestCompile
  * debugCompile
* releaseCompile