# CalendarView

[CalendarView](http://developer.android.com/reference/android/widget/CalendarView.html) 是 Android 3.0 新增的 Widget 。這個 Widget 並沒有做向下 Support ，所以只有 3.0 以上才能使用。

[教學](http://cookiesp.pixnet.net/blog/post/94549716-android---%E6%97%A5%E6%9B%86%E8%A1%8C%E4%BA%8B%E6%9B%86%E5%AF%A6%E7%8F%BE-calendarview)

屬性的 getter/setter 都是要到 Android 4.1 才能使用；那可能在 4.1 前，這個日曆就只能看看而已。有找到其他 open source 如下：

* [android-calendar-view](https://code.google.com/p/android-calendar-view)
* [CalendarView](https://github.com/SimonVT/android-calendarview) - 它是把原生的 CalendarView 做向下相容到Android 2.2

## Inherited Class

* android.view.View
  * android.view.ViewGroup
    * android.widget.FrameLayout
      * android.widget.CalendarView

## XML Attributes

| Attribute Name | Description |
| -------------- | ----------- |
| android:dateTextAppearance | |
| android:firstDayOfWeek | |
| android:focusedMonthDateColor | |
| android:maxDate | |
| android:minDate | |
| android:selectedDateVerticalBar | |
| android:selectedWeekBackgroundColor | |
| android:showWeekNumber | |
| android:shownWeekCount | |
| android:unfocusedMonthDateColor | |
| android:weekDayTextAppearance | |
| android:weekNumberColor | |
| android:weekSeparatorLineColor | |

## Public Methods

# CalendarView Library

因為 Android 本身的 CalendarView 感覺就是有點問題，所以大部分的 Library 都是從 FrameLayout 直接從頭打造的，而不是從 CalendarView 。

## android-calendar-view

* [官方網站](https://code.google.com/p/android-calendar-view/)
* [maven.org](http://search.maven.org/#search%7Cga%7C1%7CCalendarView)

## TimesSquare

* [GitHub](https://github.com/square/android-times-square)

Maven

```xml
<dependency>
    <groupId>com.squareup</groupId>
    <artifactId>android-times-square</artifactId>
    <version>(insert latest version)</version>
    <type>apklib</type>
</dependency>
```

Gradle

```groovy
compile 'com.squareup:android-times-square:(version)@aar'
```

## android-calendar-card

* [GitHub](https://github.com/kenumir/android-calendar-card)
* [Demo](https://play.google.com/store/apps/details?id=com.wt.calendarcardsample)
