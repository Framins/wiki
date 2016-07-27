# Tutorial

從 Eclipse 轉用 Android Studio 的筆記

## 調整設定

一般來說，除了外觀、編輯器、 Code Style 外，還可以調整 Run/Debug Configurations

裡面很多項可以選擇（與 Android 相關的）：

* Android Application
* Android Tests
* JUnit

## 預設常用快捷鍵

| 快捷鍵 | 功能 | 備註 |
| ------ | ---- | ---- |
| Ctrl+N | 找Class | |
| Ctrl+Shift+N | 找檔案 | |
| Ctrl+Alt+L | 格式化程式碼 | |
| Ctrl+Alt+O | 最佳化import | |
| Alt+Insert | 程式碼自動產生，如constructor/getter/setter/ .... | |
| Ctrl+E | 最近使用過的檔案 | |
| Ctrl+Alt+E | 最近修改過的檔案 | |
| Alt+Shift+C| 最近修改過的內容 | |
| Ctrl+R | Replace | |
| Ctrl+F | Find | |
| Ctrl+Shift+Space | 自動補全提示 | |
| Ctrl+Alt+Space | Class/Interface 提示 | |
| Ctrl+Space | 程式碼自動提示 | 會被切換輸入法蓋掉，沒試過 |
| Ctrl+P | Method params 提示 | |
| Ctrl+Shift+Alt+N | 找Class裡的Method/Member | |
| Alt+Shift+C | 比較最近修改的程式碼 | |
| Ctrl+Shift+Up/Down | 以區塊為單位，移動上下位置 | |
| Ctrl+X / Ctrl+Y | 刪除整行 | |
| Ctrl+D | 複製整行 | |
| Ctrl+/ | 用 %%//%% 註解 | |
| Ctrl+Shift+/ | 用 /**/ 註解 | |
| Ctrl+J | 自動產生程式碼 | |
| Ctrl+H | 顯示Class的繼承關係 | |
| Ctrl+Q | 顯示註解文件 | |
| Alt+F1 | 尋找程式碼所在的位置 | |
| Alt+1 | 開關目錄Panel | | ;
| Ctrl+Alt+Left/Right | 回到上次瀏覽的位置 | |
| Alt+Left/Right | 切換程式碼Tab | |
| Alt+Up/Down | 可以在Member/Method快速定位 | |
| F2/Shift+F2 | 往下/往上定位錯誤或警告 | |
| Ctrl+Shift+F7 | Highlight 目前位置的文字，按Esc取消 | |
| Ctrl+W | 以目前位置去選取程式碼，連續按會擴大範圍 | |
| Alt+F3 | 使用Ctrl+F尋找目前位置的文字 | |
| Ctrl+Up/Down | 不移動游標或滑鼠，直接達到點選上下捲軸的功能 | |
| Ctrl+B / Ctrl+LeftClick | 打開目前位置/點選位置的Class/Method/Member等 | |
| Shift+LeftClick / MiddleClick | 關閉檔案 | |
| Shift+F6 | Refactor / Rename | |

## Import .jar Library (舊)

一般會建議用 maven 的方法 import ：

首先去 [maven.org](http://search.maven.org/) 找你想要的 library 。以 ORMLite 為例，找到後左下角有個 Dependency Information ，選 Grails ，把裡面的 code 複製下來。

在 `build.gradle` 裡，找到 `dependencies` ，然後打入下面的內容即可加入。

```groovy
dependencies {
    compile 'com.j256.ormlite:ormlite-core:4.48'
}
```

如果是實體 jar 檔的話（路徑是相對於 `build.gradle` 的）：

```groovy
dependencies {
    compile files ('libs/ormlite-core-4.48.jar')
}
```

最後讓 Android Studio 重整即可： Tools -> Android -> Sync Project with Gradle Files

以上是 module 裡的 `build.gradle` ，如果是 application 的 `build.gradle` 試過是無法成功。

## Import .jar Library

找不到是哪一版開始，就可以用 GUI 新增 library 了。在 File -> Project Structure... (Ctrl+Alt+Shift+S) -> Dependencies 裡

右上角有一個加號，按下去即可選擇是要 Meven 、 File 或是直接引用其他 Module 。

另外 File 的引用，從 0.4.4 開始，會預設加一行：

```groovy
dependencies {
    compile fileTree(dir: 'libs', include: '*.jar')
}
```

這樣它會從 `ModuleName/libs` 找所有 .jar 和 .aar 檔，並匯入。這樣的操作方式會跟 Eclipse 比較像，從 Eclipse 轉過來會比較習慣。

## Import .so Library

.so即NDK相關，Android Studio 0.4.2 還沒有相關的解法，不過理論上只要把.so壓進apk就可以執行了。

實際成功的做法(Use Android Studio 0.4.2, Gradle 0.7.+)：

1. 建立目錄，`[ProjectHome] \ lib \ armeabi` ，然後把.so檔全放進去。
2. 切換到 `[ProjectHome]` 然後把lib這個目錄壓縮，並改名成 `armeabi.jar`
3. 把jar放到 `[ModuleHome] \ libs` 目錄裡。
4. 打開 `[ModuleHome] \ build.gradle` 。
5. 在 `dependencies {}` 裡加入 `compile fileTree(dir: 'libs', include: '*.jar')`

前兩個動作其實並不是必要，只要zip目錄結構是正確的即可。

## 操作說明

* developer:framework:android:android-studio:android-studio:code
* developer:framework:android:android-studio:android-studio:refactor
