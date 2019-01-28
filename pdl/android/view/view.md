# View

在 Android 裡，所有畫面上可以看到的物件，幾乎都繼承了 `android.view.View` 這個物件。同理，如果想自己寫 View 的類別，就必需繼承它。它能做的操控就相當的多了，通常也不需要轉型就可以直接操作了。

## Palette

以下分類依 Android Studio 的 Layout Editor 工具為準。

### Layouts

Layout 是畫面排版的基本容器，主要有五大類

* FrameLayout
* LinearLayout
* RelativeLayout
* TableLayout

Android 因後來 App 功能需求，也有新增其他基本的 Layout

* GridLayout (API level 14, support library v7)

### Widgets

基本的 [View](http://developer.android.com/reference/android/view/View.html) 依繼承關係與文字順序排列

* [ImageView](image-view.md)
  * ImageButton
* ProgressBar
  * RatingBar
  * SeekBar
* Space
* SurfaceView
  * GLSurfaceView
  * [VideoView](video-view.md)
* TextView
  * Button
    * CompoundButton
      * Checkbox
      * RadioButton
      * Switch (Added in API level 14)
      * ToggleButton
  * CheckedTextView
  * [EditText](edit-text.md)
* [WebView](web-view.md)

### Text Fields

### Containers

另外還有一種 [ViewGroup](http://developer.android.com/reference/android/view/ViewGroup.html) 是一組 View 的集合

* AbsoluteLayout
* AdapterView
  * [AbsListView](abs-list-view.md)
    * GridView
    * [ListView](list-view.md)
      * [ExpandableListView](expandable-list-view.md)
  * AbsSpinner
    * Gallery (Deprecated since API level 16)
    * Spinner
  * AdapterViewAnimator
    * AdapterViewFlipper
    * StackView
* DrawerLayout
* FragmentBreadcrumbs
* FrameLayout
  * AppWidgetHostView
  * [CalendarView](view/calendar-view.md)
  * DatePicker
  * GestureOverlayView
  * HorizontalScrollView
  * MediaController
  * ScrollView
  * TabHost
  * TimePicker
  * ViewAnimator
* GridLayout
* LinearLayout
  * NumberPicker
  * RadioGroup
  * SearchView
  * TabWidget
  * TableLayout
  * TableRow
  * ZoomControls
* PagerTitleStrip
* RelativeLayout
* SlidingDrawer
* SlidingPaneLayout
* [ViewPager](view-pager.md)

### Date & Time

### Expert

### Custom

## XML Attributes

### android:focusable

當使用者在使用鍵盤要跟 UI 做互動時，UI 通常會有變化來提醒使用者現在是在跟哪個 UI 做互動，這樣就需要設定此屬性為 true 即可。

### android:focusableInTouchMode

當使用者開始用觸控面板的時候，Android 就會進入 Touch Mode。Android 對 [Touch Mode](http://android-developers.blogspot.tw/2008/12/touch-mode.html) 的定義，是如果是要用觸控面板點選 UI 時，UI 是不會有 focus 行為的，使用 requestFocus 也不會。此時的狀態會是 Pressed。

但如果某些 UI 在 Touch Mode 下，一樣會需要 focus，如 EditText。這時就需要設定此屬性為 true，點擊的同時就也能 focus 了。
