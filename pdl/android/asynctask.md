# AsyncTask

[AsyncTask](http://developer.android.com/reference/android/os/AsyncTask.html) 可以處理後台耗時任務。所謂的耗時任務包括：

* Downloading / Uploading
* Mass access database
* List sorting
* Progress loading

當然這些任務也可以使用 Thread 實作，只是寫 Thread 會有缺點：

* 只有 UI Thread 可以直接改 UI ，而新開的 Thread 不能直接在 `run()` 裡面更新 UI ，要寫 Handler 去更新 UI 。
* 開 Thread 會給系統帶來很大的負擔，然後就會有性能的問題。

因此，有些比較簡單的任務還是在 AsyncTask 實作就好了，不需要寫 Thread 。

## Base Concept

AsyncTask 是一個抽象類別，並定義了三個泛型類型。

另外泛型類型如下

* `params` - 啟動任務執行時，要輸入的參數
* `progress` - 任務進度
* `result` - 後台執行任務要返回的結果

抽象類需要實作的 Method 只有一個：

    doInBackground(Params...) // 實際要做的任務，這裡不可做UI操作。可呼叫 `publishProgress()` 作進度更新

但通常還會再實作下面三個，這三個也都可以做UI操作：

    onPreExecute() // 執行 doInBackground() 任務前，要先做的準備工作。如顯示進度條。
    onProgressUpdate(Progress...) // publishProgress 被呼叫後，會執行這個 callback ，然後就可以更新 UI 進度條。
    onPostExecute(Result) // 執行 doInBackground() 任務完成後，會執行這個 callback ，即可把結果顯示在 UI 上。

取消時的 callback ：

    onCancelled() // 當主執行緒呼叫 cancel() 時，任務會呼叫的 callback 。

而 AsyncTask 要正確執行，必須滿足下面的條件：

* Task 要在 UI Thread中 建立。
* `execute()` 方法必須要在 UI Thread 中呼叫。
* 不可自己手動呼叫上述 callback 。
* Task 只能被執行一次。

## Example

### 單純執行一個花時間的操作

```java
public class Task extends AsyncTask<Void, Void, Void> {
    @Override
    protected Void doInBackground(Void... params) {
        // do something
        return null;
    }
}
```
