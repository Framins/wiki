# Library

Android 函式庫不大好找， Google 到的都是 APK 。所以有看到的話，都記一下比較好....。

* [參考網頁1](http://rritw.com/a/JAVAbiancheng/ANT/20131109/441267.html)
* [參考網頁2](http://www.usingdll.com/plus/view.php?aid=3773)
* [參考網頁3](http://blog.csdn.net/wannawang/article/details/9963837)
* [讀取PDF相關](http://my.oschina.net/ernest/blog/16999)

以下自行分類

## UI Widget

UI Widget 大部分都是繼承 View 相關的 Class ，並以固定目標去加強 View 的功能，如可以用手勢放大縮小的 ImageView 。

### extends ImageView

參考 ImageView

### extends ListView

|  Library  |  Description  |  Links  |
|  -------  |  -----------  |  -----  |
| [DevsmartLib-Android](http://www.dev-smart.com/archives/34) | 簡單來說，就是橫向的 ListView 。這繼承的不是ListView ，而是 `AdapterView<ListAdapter>` 。只是因為性質跟 ListView 很像，所以就放這裡了。 | [GitHub](https://github.com/dinocore1/DevsmartLib-Android) |
| [TwoWayView](https://github.com/lucasr/twoway-view) | 同上，也是繼承 `AdapterView<ListAdapter>` | |

### ActionBarSherlock

ActionBar 是個很好用也很煩的東西，因為有版本的問題，就跟 HTML5 在 IE8 會死很慘的意思是差不多的。 ActionBarSherlock解決了這個問題。

* [官方網站](http://actionbarsherlock.com/)
* [maven.org](http://search.maven.org/#search%7Cga%7C1%7CActionBarSherlock)

### ViewPagerIndicator

加強 ViewPager 的功能，裡面還有一堆範例可以參考。

* [官方網站](http://viewpagerindicator.com/)
* [maven.org](http://search.maven.org/#search%7Cga%7C1%7Cviewpagerindicator)

### GifView

因為 Android 本身不能看 Gif 動畫，所以才會出現這個套件。

* [Google Code](https://code.google.com/p/gifview/)

### AndroidQuery

看這個名字，它的目標應該是做得像 [jQuery](http://jquery.com/) 一樣的函式庫

* [使用筆記](library/android-query.md)
* [Google Code](https://code.google.com/p/android-query/)
* [maven.org](http://search.maven.org/#search%7Cga%7C1%7CAndroid-Query)

### Horizontal ListView

橫向的 ListView

* [介紹頁面](http://www.dev-smart.com/archives/34)
* [GitHub](https://github.com/dinocore1/DevsmartLib-Android)

## Database

參考[Database](database.md#Third-Party Library)。

## PDF

http://www.oschina.net/project/tag/255/pdf-tools?sort=view&lang=19&os=0

PDF 有分兩大類，一種是 Generator ，另一種是 Reader

* [MuPDF](http://www.mupdf.com/) - Reader 最好的選擇，但它是用 NDK 寫的....
* [Android-PDF-Viewer-Library](https://github.com/jblough/Android-Pdf-Viewer-Library)
* [PDFView](https://github.com/JoanZapata/android-pdfview)

## 待確認

* [Table](https://github.com/InQBarna/TableFixHeaders)
