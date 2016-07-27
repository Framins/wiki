# Android Studio

[官方下載](http://developer.android.com/sdk/installing/studio.html)

* [Tutorial](tutorail.md)
* [gitignore](gitignore.md)
* [build.gradle](build.gradle.md)

## Change Log

#### 1.0 RC

[2014-11-21發佈](http://tools.android.com/recent/androidstudio1rc1_releasecandidate1released)

總算要發佈正式 1.0 版了

#### 0.5.8

[2014-5-8發佈](http://tools.android.com/recent/androidstudio058released)

* 修正一些會導致crash的回報
* 整合了兩個 IntelliJ EAP builds
* Gradle 支援到 1.12 ，Android Gradle plugin 更新到0.10
* 新的 Gradle 0.10.0 ，可以設定 resource prefix，如果 resource 在命名時沒有照這個設定走的話，它會出現提醒
* Layout 編輯器預覽畫面現在支援滑鼠移入功能，當滑鼠移入時，對應的物件會高亮顯示
* Ctrl + C,X,V 會複製錯誤的問題修正 (應該是這樣，看不大懂)
* ...

#### 0.5.7

[2014-4-25發佈](http://tools.android.com/recent/androidstudio057released)

* 修正 0.5.6 專案結構對話框裡的嚴重錯誤

#### 0.5.6

[2014-4-24發佈](http://tools.android.com/recent/androidstudio056released)

* 修正一堆害死人不償命的 Bug
* 改善 `build.gradle` 的編輯器支援
* 新的樣版：支援 Google Play Service 的樣版
* Gradle 同步時的錯誤，現在會顯示訊息視窗裡了，這樣除錯會比較方便

#### 0.5.5

[2014-4-16發佈](http://tools.android.com/recent/androidstudio055released)

* 更新 IntelliJ 13.x EAP build: 135.667
* 編輯功能
  * 新增資源類型的檢測
  * 新增對 annotation 的支援，像 `@NonNull` 之類的
  * 移除不正確的 `@Nullable` annotation
* Layout 繪圖
  * 在裝置選擇時，會顯示符合或不符合目前 layout 的裝置有哪些。
  * 自動選擇裝置功能
* 專案功能
  * 匯入 module 時，可以直接由 Eclipse ADT 匯入
  * 專案結構對話框整合。
* 新的樣版，可以建立 manifest, AIDL, resource XML 等
* Attach to Process
* 修正一堆 Bug

#### 0.5.4

[2014-4-3發佈](http://tools.android.com/recent/androidstudio054released)

* 修正一堆 Bug
* 新增 Lint API Check。
* 新樣版－－ Google Map Activity。
* 0.5.4 版需要 Tool 22.6.2 ，所以必需要升級。

#### 0.5.3

[2014-3-28發佈](http://tools.android.com/recent/androidstudio053released)

* 更新 IntelliJ IDE 到 13.1.1 版(([更新說明](http://confluence.jetbrains.com/display/IDEADEV/IntelliJ+IDEA+13.1.1+Release+Notes)))。
* Gradle支援
* 現在可以直接匯入專案當作 Module 使用。(這功能我等好久了...)
  * 同步或匯入失敗時，它不只會彈出氣泡式提醒，也會寫到訊息視窗裡。
  * Build variants 視窗現在有 Conflicting variants ，只是我找不到在哪....。
  * Templates
  * 現在新增 Activity 的時候可以選擇你要建立的是 main 、 debug 或是 release 等 build 版本。
  * 新增元件原本是進對話視窗，再選擇詳細功能，現在改成使用 nest 選單直接選裡面的項目，原因應該是因為多了上面 build 版本的選擇。
* 修正 Bug

#### 0.5.2

[2014-3-21發佈](http://tools.android.com/recent/androidstudio052released)

* 修正 Bug
* 更新 IDE 到 IntelliJ 13.1 RC2
* 新增 Lint 檢查

這次更新感覺沒啥特別的，看起來還是以修正Bug為主吧！

#### 0.5.1

[2014-3-8發佈](http://tools.android.com/recent/androidstudio051released)

主要是修正嚴重的Bug：

* 讀取 project 時會出現 "Unable to load class 'org.gradle.api.artifacts.result.ResolvedComponentResult'" 的訊息。
* 0.5.0 無法執行在自定結構的 project ，像 Eclipse 匯出的就是自定結構。
* 0.5.0 無法在 Mac OSX + Java 7 上啟動。官方有公佈 0.5.0 升 0.5.1 的方法，當然直接下載是比較快啦...。
* 啟動有時會出現 NullPointerException

#### 0.5.0

[2014-3-7發佈](http://tools.android.com/recent/androidstudio050released)

* 支援 Gradle plugin 0.9 ，但同時必需也把專案升到 0.9 ，方法官方有提供[教學](http://tools.android.com/tech-docs/new-build-system/migrating_to_09)。
* 升級到 IntelliJ 13.1 EAP
  * 新的 code completion 樣版
* Gradle 新功能。
* Lint
  * 做了更多的檔案交叉測試，可以確定程式的寫法是正確。官方舉例是 findViewById 會比對 XML 上的宣告，來知道 java 上的類別有沒有打錯。其他檢查如： `String.format` 參數型別檢查、 Array 大小檢查、未知 ID 檢查...等。
* 編輯器支援 transition 資源編輯。

#### 0.4.6

[2014-2-19發佈](http://tools.android.com/recent/androidstudio046released)

* 修正 bug ，看起來像是語言切換的問題。
* 如果 JAR 有文件，會有提示功能。
* 改善 project, activity 的模版。
  * Activity 預設不加入 fragment 了，改在附加選項裡。事實上，如果沒要用 framgent 的話，預設硬要加入的確是很煩。
  * LoginActivity 預設樣版多了 Google+ 登入功能； component 多了 +1 的 fragment 的樣版。
  * Asset Studio wizard > clipart 多了幾個圖片可用

#### 0.4.5

[2014-2-14發佈](http://tools.android.com/recent/androidstudio045released)

* 這一版除了修正了一堆bug外還有新增以下功能：
* 整合最新的 IntelliJ 版本(13 EAP build [133.818](http://confluence.jetbrains.com/display/IDEADEV/IntelliJ+IDEA+13+133.818+Release+Notes))
* 在 Project Structure -> Modules -> Dependencies 裡，改善了新增 Library 的方式；這同時也是最多人嫌它的地方。
  * 可以用關鍵字直接從 Maven 找 Library 並新增，超方便的。
  * 它有包含了本地的 Maven repositories ，像是 support library
* 如果手動去改 `build.gradle` 的話，它會提醒你要做立即更新
* Log cat 會自動建立 filter ，以前的版本只要開新專案都要手動建立
* 新增 Lint checks ，尤其是[Assertion](http://openhome.cc/Gossip/JavaGossip-V1/Assertion.htm)，Android會建議用`BuildConfig.DEBUG` 取代。
* Icon asset 產生器更快了。

0.4.4 之前的就不打了，自行看[官網](http://tools.android.com/recent)吧。
