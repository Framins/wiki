# Queue

Queue，佇列，資料就會像排隊看電影片一樣，維持前後順序等待處理。即然是像排隊，那就會有進入等排隊的地方，稱作 *rear*；資料出來處理的地方，稱作 *front*。

如果某一筆資料想看電影（處理），就必須從 Queue 的 rear 進入等候處理。前面的資料會一筆一筆的從 front 出來處理，直到輪到這筆資料。

Queue 在資料結構的定義如下：

* 必須使用有順序性的結構實作，所以 Array 和 Linked Lists 都能實作出 Queue。但 Array 實作上會比較複雜。
* 具有 FIFO 先進先出的特性。
* 插入、刪除的時間複雜度為 O(1)，搜尋的時間複雜度為 O(N)，不過通常都不討論搜尋。
* Queue 具備暫存的特性。

Queue 具備的操作如下：

* *enqueue* 資料放入 rear。此為必要實作。
* *dequeue* 資料由 front 取出。此為必要實作。
* *peek* 可以看 rear 資料而不取出。
* *size* 取得資料數目。
* *isEmpty* 回傳 Queue 是否為空。
* *isFull* 回傳 Queue 是否滿載。

## Circular Queue

Circular Queue 可做為記憶體循環使用。

http://120.118.165.132/LMS/Content/C010/Tbank/Read/CH4/4-3/4-3.htm

## Priority Queue

Priority Queue 為有優先順序性的 Queue。

## References

* http://emn178.pixnet.net/blog/post/93475832-%E4%BD%87%E5%88%97(queue)
* http://www.csie.ntnu.edu.tw/~u91029/Data.html#4
