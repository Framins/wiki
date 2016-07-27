# Ruby Instruction

裝好 Ruby 開發環境後，就可以下 irb 進入指令互動環境，並可以做一點簡單的練習或實驗。

如果覺得提示字元太長的話，可以加`--simple-prompt`。

```
$ irb --simple-prompt
>> 1 + 1
=> 2
```

在 irb 介面操作的時候，它會自動 print 出剛剛執行的結果，如果要提取上一次的結果，可以用 `_` 一個底線代替上一次的結果

```
$ irb --simple-prompt
>> 2 + 2
=> 4
>> _ + _
=> 8
```

也有時候會沒有結果，如 print 指令就是沒有回傳結果的函數，這就就會出現一個 `nil` 表示是空的。

```
>> print "Hello\n"
Hello
=> nil
```

如果不想玩 irb ，想直接寫檔案的話，可以先把程式用記事本打好，之後再存成 `.rb` 附檔名，再下 ruby 指令即可執行

```
$ ruby hello.rb
```
