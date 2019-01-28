# Intent

許多文章都說，Android 的 Intent（意圖）機制非常地強大。簡單來說，Android 的做法是，Intent 是一個抽象的概念，可以說是「程式想要做某件事」，那 Android 系統就會試著去解釋這個 Intent 該如何做，如果系統能了解的話，就會去處理該工作。如果方法不只一種，更能讓使用者來自行選擇。

比方說，程式發出一個想看某個網址的訊息，Android 系統接受到後，可能就會理解成要看該網址裡的網頁內容，所以就是要開瀏覽器，並連結到該網址。而瀏覽器又分很多種，如 Chrome 或 FireFox 等，這時，就會讓使用者自行選擇該如何看網頁。這就是 Intent的執行過程。

## Share to

原始碼：

```java
// In Activity class
// subject: 主題，有的APP不會用到。
// body: 內容，也是主要要分享的內容。
// chooserTitle: 彈出選擇對話框時的標題。
String subject = "Subject";
String body = "Body";
String chooserTitle = "Title";

Intent intent = new Intent(Intent.ACTION_SEND);
intent.setType("text/plain");
intent.putExtra(Intent.EXTRA_SUBJECT, subject);
intent.putExtra(Intent.EXTRA_TEXT, body);

startActivity(Intent.createChooser(intent, chooserTitle));
```

## Share to by Filter

如果是要取得指定的內容，可以先把原始的分享內容取出來

```java
private List<ResolveInfo> getShareTargets() {
    Intent intent = new Intent(Intent.ACTION_SEND, null);

    intent.addCategory(Intent.CATEGORY_DEFAULT);
    intent.setType("text/plain");

    PackageManager pm = getActivity().getPackageManager();
    return pm.queryIntentActivities(intent, PackageManager.COMPONENT_ENABLED_STATE_DEFAULT);
}
```

再來要把該 List 內容做分析，並取得需要的內容：

```java
// In Activity class
String subject = "Subject";    // 主題，有的APP不會用到。
String body = "Body";          // 內容，也是主要要分享的內容。

List<ResolveInfo> resInfo = getShareTargets() {

if (!resInfo.isEmpty()) {
    List<Intent> targetedShareIntents = new ArrayList<Intent>();

    for (ResolveInfo info : resInfo) {
        Intent targeted = new Intent(Intent.ACTION_SEND);
        targeted.setType("text/plain");
        ActivityInfo activityInfo = info.activityInfo;

        // App名稱可用 activityInfo.packageName 判斷。
        // 以下是找到想要的App才加入

        if (activityInfo.packageName.contains("facebook")) {
            targeted.putExtra(Intent.EXTRA_SUBJECT, subject);
            targeted.putExtra(Intent.EXTRA_TEXT, body);
            targeted.setPackage(activityInfo.packageName);
            targetedShareIntents.add(targeted);
        }
    }
}
```

最後再建立一個自定 ChooserIntent 並啟動 Activity 即可

```java
String chooserTitle = "Title";    // 彈出選擇對話框時的標題。

Intent chooserIntent = Intent.createChooser(targetedShareIntents.remove(0), chooserTitle);

if (chooserIntent == null) {
    return;
}

chooserIntent.putExtra(Intent.EXTRA_INITIAL_INTENTS, targetedShareIntents.toArray(new Parcelable[] {}));

try {
    startActivity(chooserIntent);
} catch (android.content.ActivityNotFoundException ex) {
    Toast.makeText(this, "Can't find share component to share", Toast.LENGTH_SHORT).show();
}
```

如果要針對ResolveInfo(([ResolveInfo@Android Developers](http://developer.android.com/reference/android/content/pm/ResolveInfo.html)))直接啟動該App的話

```java
Intent intent = new Intent(Intent.ACTION_SEND);
intent.setType("text/plain");
intent.putExtra(Intent.EXTRA_SUBJECT, subject);
intent.putExtra(Intent.EXTRA_TEXT, body);

ActivityInfo activity = info.activityInfo;
ComponentName name = new ComponentName(activity.applicationInfo.packageName, activity.name);

intent.addCategory(Intent.CATEGORY_LAUNCHER);
intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_RESET_TASK_IF_NEEDED);
intent.setComponent(name);

startActivity(intent);
```

傳送 Email
---------

文字內容

```java
Uri uri = Uri.parse("mailto:jangconan@gmail.com");
Intent it = new Intent(Intent.ACTION_SENDTO, uri);
startActivity(it);
```

```java
Intent it = new Intent(Intent.ACTION_SEND);
it.putExtra(Intent.EXTRA_EMAIL, "me@abc.com");
it.putExtra(Intent.EXTRA_TEXT, "The email body text");
it.setType("text/plain");
startActivity(Intent.createChooser(it, "Choose Email Client"));
```

```java
Intent it=new Intent(Intent.ACTION_SEND);   
String[] tos={"me@abc.com"};   
String[] ccs={"you@abc.com"};   
it.putExtra(Intent.EXTRA_EMAIL, tos);   
it.putExtra(Intent.EXTRA_CC, ccs);   
it.putExtra(Intent.EXTRA_TEXT, "The email body text");   
it.putExtra(Intent.EXTRA_SUBJECT, "The email subject text");   
it.setType("message/rfc822");   
startActivity(Intent.createChooser(it, "Choose Email Client"));  
```

加入影音檔當附件

```java
Intent it = new Intent(Intent.ACTION_SEND);
it.putExtra(Intent.EXTRA_SUBJECT, "The email subject text");
it.putExtra(Intent.EXTRA_STREAM, Uri.parse("file:///sdcard/mysong.mp3"));
it.setType("audio/mp3");
startActivity(Intent.createChooser(it, "Choose Email Client"));
```

加入圖片檔當附件

```java
Intent it = new Intent(Intent.ACTION_SEND);
it.putExtra(Intent.EXTRA_SUBJECT, "The email subject text");
it.putExtra(Intent.EXTRA_STREAM, Uri.parse("file:///sdcard/mypic.jpg"));
it.setType("image/jpeg");
startActivity(Intent.createChooser(it, "Choose Email Client"));
```

Flag
----

| Flag Name | Description | API Level |
| --------- | ----------- | --------- |
| FLAG_ACTIVITY_BROUGHT_TO_FRONT | | 1 |
| FLAG_ACTIVITY_CLEAR_TOP | 無條件清除之前的所有 Activity | 1 |
| FLAG_ACTIVITY_CLEAR_WHEN_TASK_RESET | 此 Flag 跟 FLAG_ACTIVITY_RESET_TASK_IF_NEEDED 有相關 | 3 |
| FLAG_ACTIVITY_EXCLUDE_FROM_RECENTS | | 1 |
| FLAG_ACTIVITY_FORWARD_RESULT | | 1 |
| FLAG_ACTIVITY_TASK_ON_HOME | 指示開啟一個全新的 Activity，並放置於前景 | 11 |
| FLAG_ACTIVITY_LAUNCHED_FROM_HISTORY | | 1 |
| FLAG_ACTIVITY_MULTIPLE_TASK | | 1 |
| FLAG_ACTIVITY_NEW_TASK | | 1 |
| FLAG_ACTIVITY_NO_ANIMATION | | 5 |
| FLAG_ACTIVITY_NO_HISTORY | 啟動 D 之後再切換其他 Activity（包括按返回鍵），Main 會自動 finish，不會留存 | 1 |
| FLAG_ACTIVITY_NO_USER_ACTION | | 3 |
| FLAG_ACTIVITY_PREVIOUS_IS_TOP | | 1 |
| FLAG_ACTIVITY_REORDER_TO_FRONT | | 3 |
| FLAG_ACTIVITY_RESET_TASK_IF_NEEDED | | 1 |
| FLAG_ACTIVITY_SINGLE_TOP | 指示如果目前要開啟的 Activity 已經在執行，Activity 就不會被開啟，意即只有存在單一 Activity Instance | 1 |

Intent Filter
-------------

Intent Filter 可以讓系統知道這個應用程式的 Activity Service 和 BroadcastReceiver 具有何種資料處理的能力。系統只要發出Intent後，只要有某個 Intent Filter 的定義符合 Intent 的要求時，系統就能去呼叫該應用程式，或是讓使用者在數個符合的應用程式中選擇。

### Basic concept

Intent Filter(為避免跟發出的 Intent 搞混，下面開始簡稱為 Filter )下只有三種元素：

* action
* category
* data

每個 Activity 可以設定很多個 Filter；而每個 Filter 也可以設定多個 action、category 和 data。

> Intent Filter 雖然也有一個 IntentFilter Class，但實際上 Intent Filter 都是在 AndroidManifest.XML 裡定義的，而不是用程式產生。只有 BroadcastReceiver 的 receivers 是例外

當Intent發出的時候，會開始在Manifest裡定義的Filter裡面三個元素做比對，比對會進行三個test，三個test都通過的時候，才會確認這個元件可以處理這個Intent；如果不只一個Activity/Service通過Test的話，那系統就會問你要啟動哪一個，都不符合的話就會發生錯誤。

1. Action Test
  * 如果 Filter 至少要有一個 Action 才會做這個 Test；如果 Filter 沒有 Action，那它就收不到任何 Intent
  * 發出的 Intent 沒有指定 Action，那這個 Test 就 pass
2. Category Test
3. Data Test

### Action

定義 intent 抽象的動作，比方說顯示資料給 user 時，可以用預設的 `android.intent.action.VIEW`；編輯用 `android.intent.action.EDIT` 等等。

Intent FAQ
----------

### 開啟外部App

使用 getPackageManager().getLaunchIntentForPackage()，它會自動去取得該 package 的 Launch intent。

以 Chrome 為例，Chrome 的 package name 是 `com.android.chrome`

```java
Intent intent = getPackageManager().getLaunchIntentForPackage("com.android.chrome");
startActivity(intent);
```

### 開啟 Google Play 至指定的 App

以 Chrome 為例，Chrome 的 package name 是`com.android.chrome`，再來就是先試著開 Google Play App，如果不行就開網頁版的 Google Play。

```java
String package = "com.android.chrome";

try {
    intent = new Intent(Intent.ACTION_VIEW, Uri.parse("market://details?id=" + package));
    startActivity(intent);
} catch (android.content.ActivityNotFoundException e) {
    intent = new Intent(Intent.ACTION_VIEW, Uri.parse("http://play.google.com/store/apps/details?id=" + package));
    startActivity(intent);
}
```

References
----------

* [Intent Filters@Android Developers](http://developer.android.com/guide/components/intents-filters.html#Receiving)
* http://blog.csdn.net/nei504293736/article/details/7479554
* http://www.pocketdigi.com/20110406/232.html
* http://blog.sina.com.cn/s/blog_5f599e1d01011tyn.html
* http://www.jollen.org/blog/2009/07/jollen-android-programming-26.html
* http://ysl-paradise.blogspot.tw/2008/12/intent.html
