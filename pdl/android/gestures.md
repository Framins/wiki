# Gestures

麻煩的手勢

## Screen Touch Events

螢幕 Touch 事件順序：

* ACTION_DOWN
* ACTION_MOVE
* ACTION_MOVE
* ...
* ACTION_MOVE
* ACTION_UP

## View Touch Event Callback

View 的 Touch 事件相關方法：

* public boolean dispatchTouchEvent(MotionEvent ev) 用來分發 TouchEvent
* public boolean onInterceptTouchEvent(MotionEvent ev) 用來攔截 TouchEvent
* public boolean onTouchEvent(MotionEvent ev) 用來處理 TouchEvent

實際執行順序：

1. TouchEvent 發生時，會先傳給最頂層的 View 裡的 dispatchTouchEvent()
2. dispatchTouchEvent() 先進行分發，如果 return true 就交給這個 view 的 onTouchEvent() 處理
3. 如果 return false，會交給 onInterceptTouchEvent() 決定是否攔截。
4. 如果 return true 就交給它的 onTouchEvent()
5. 如果 return false 才會傳給子 view然後再從子 view的dispatchTouchEvent() 繼續
6. 如果子 view 的 onTouchEvent() 回傳了 false，那它就會再往上傳
7. 如果傳到最上層還是 false 的話，這個事件就會消失

## GestureDetector

簡單 GestureDetector.SimpleOnGestureListener 的例子：

```java
public class MainActivity extends Activity {
    private static final String TAG = MainActivity.class.getSimpleName();
    private Handler mHandler;
    private GestureDetector mGesture;

    private GestureDetector.OnGestureListener mGestureListener = new GestureDetector.SimpleOnGestureListener() {
        @Override
        public boolean onFling(MotionEvent e1, MotionEvent e2, float velocityX, float velocityY) {
            Log.d(TAG, "" + velocityY);
            return super.onFling(e1, e2, velocityX, velocityY);
        }
    };

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        mGesture = new GestureDetector(this, mGestureListener, mHandler, false);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event) {
        return mGesture.onTouchEvent(event);
    }
}
```

只要在 OnGestureListener 覆寫想要偵測的方法即可：

| Method | Description |
| ------ | ----------- |
| boolean onDoubleTap(MotionEvent e) | |
| boolean onDoubleTapEvent(MotionEvent e) | |
| boolean onDown(MotionEvent e) | |
| boolean onFling(MotionEvent e1, MotionEvent e2, float velocityX, float velocityY) | |
| void onLongPress(MotionEvent e) | |
| boolean onScroll(MotionEvent e1, MotionEvent e2, float distanceX, float distanceY) | |
| void onShowPress(MotionEvent e) | |
| boolean onSingleTapConfirmed(MotionEvent e) | |
| boolean onSingleTapUp(MotionEvent e) | |

References
----------

* [官方說明](http://developer.android.com/training/gestures/index.html)
* [GestureDetector.SimpleOnGestureListener@Android Developers](http://developer.android.com/reference/android/view/GestureDetector.SimpleOnGestureListener.html)
