# ViewPager

## Cancel Swipe

有時候會因需求，而要把滑動功能關閉，不過 ViewPager 並沒有這樣的功能，所以只能繼承並改寫 Touch 相關事件。

```java
public class CancelSwipeViewPager extends ViewPager
{
    private boolean isPagingEnabled = true;

    public CancelSwipeViewPager(Context context)
    {
        super(context);
    }

    public CancelSwipeViewPager(Context context, AttributeSet attrs)
    {
        super(context, attrs);
    }

    @Override
    public boolean onTouchEvent(MotionEvent event)
    {
        if (this.isPagingEnabled) {
            return super.onTouchEvent(event);
        }

        return false;
    }

    @Override
    public boolean onInterceptTouchEvent(MotionEvent event) {
        if (this.isPagingEnabled) {
            return super.onInterceptTouchEvent(event);
        }

        return false;
    }

    public void setPagingEnabled(boolean b) {
        this.isPagingEnabled = b;
    }
}
```
