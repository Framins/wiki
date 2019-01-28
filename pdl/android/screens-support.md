# Screens Support

[官方說明](http://developer.android.com/guide/practices/screens_support.html)

## Terms and concepts

術語與概念（[官方說明](http://developer.android.com/guide/practices/screens_support.html#terms)）：

|  Name  |  Description  |  Example  |
|  ----  |  -----------  |  -------  |
| Screen size | 裝置實際的大小，如10吋、8吋、7吋等 | small, normal, large, extra large. |
| Screen density | 螢幕的像素密度，通常單位都是 dpi(dots per inch) | ldpi, mdpi, hdpi, xhdpi |
| Orientation | 使用者觀看方向 | landscape/portrait |
| Resolution | 解析度 | 480x800 |
| Density-independent pixel | 一個虛擬的單位，定義：100dp，在160dpi 時基數為1，即為 100px；320dpi 時基數為2，即為 200px，依此類推 | 160dp |

## Dimension

單位（[參考網頁](http://www.imyukin.com/?p=277)，[官方說明](http://developer.android.com/guide/topics/resources/more-resources.html#Dimension)）：

|  Unit  |  Description  |  Applicable  |
|  ----  |  -----------  |  ----------  |
| dip (device independent pixels) | 設備獨立像素，不同的設備有不同的顯示效果 |
| dp (density-independent pixels) | 一個虛擬的單位，如上述所說 | Android 建議使用的單位 |
| sp (scale-independent pixels) | 文字要用 sp，在使用者調整文字大小時，設定 sp 的也會跟著變 | 用在文字上 |
| px (pixels) | 傳統的像素 | Android 裡不建議使用此單位 |
| pt (point) | 磅，印刷用單位，1pt = 1/72inch | |
| in (inches) | 英寸| |
| mm (millimeters) | 公厘 | |

dp、dpi、px 的關係：

$ px = dp * \frac{dpi}{160} $

寫成程式大概就像這樣：
```java
public class ScreenUtil {
	/**
	 * Covert dp to px
	 *
	 * @param dp
	 * @param context
	 * @return pixel
	 */
	public static float convertDp2Px(Context context, float dp) {
		return dp * getDensity(context);
	}

	/**
	 * Covert px to dp
	 *
	 * @param px
	 * @param context
	 * @return dp
	 */
	public static float convertPxToDp(Context context, float px) {
		return px / getDensity(context);
	}

	/**
	 * Get density
	 *
	 * @param context
	 * @return
	 */
	public static float getDensity(Context context){
		DisplayMetrics metrics = context.getResources().getDisplayMetrics();
		return metrics.density;
	}
}
```
