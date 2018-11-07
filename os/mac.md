MAC
===

Homebrew 管理器

http://homebrew-file.readthedocs.io/en/latest/index.html

---

MacOS 冷知識

## 輸入 Emoji、超特殊符號

    Control + Command + 空白鍵

## 開關動畫效果

### Mission Control

打開

    defaults delete com.apple.dock expose-animation-duration;killall Dock

關閉

    defaults write com.apple.dock expose-animation-duration -int 0;killall Dock

### Launchpad

打開

    defaults delete com.apple.dock springboard-show-duration
    defaults delete com.apple.dock springboard-hide-duration;killall Dock

關閉

    defaults write com.apple.dock springboard-show-duration -int 0
    defaults write com.apple.dock springboard-hide-duration -int 0;killall Dock

版面
    
    defaults write com.apple.dock springboard-rows -int 6
    defaults write com.apple.dock springboard-columns -int 8;killall Dock
     
重排App順序
   
    defaults write com.apple.dock ResetLaunchPad -bool true; killall Dock

## Terminal

刪除整行指令

    ⌃+A ⌃+K    // move the cursor at the beginning of the line and delete all after Cursor.
    ⌃+E ⌃+U    // move the cursor to the end of the line and delete all before Cursor.

## 睡眠模式設定

Mac 無法從介面上得知或設定睡眠模式，使用用下面的指令可以確認目前的電源設定：

    pmset -g

其中 `hibernatemode` 即為睡眠模式設定值，有下列三種選項

* 0 - 會把目前的狀態保存到記憶體（RAM），而記憶體的資料是要靠電力維持的，因此這會是比較耗電的模式
* 3 - 會把目前的狀態，同時保存到記憶體與硬碟，相較於 0，這個模式當斷電時，還有辦法從硬碟救回狀態
* 25 - 會把目前的狀態保存到硬碟，是相較省電的模式，但還原狀態的速度就會比較慢

## References

* [macOS 合盖休眠掉电快的解决办法](http://www.macgg.com/index.php/archives/47.html) | macGG
* [macOS Sierra 睡眠方式設置](http://www.xiaocrab.net/posts/f8a16df0/) | xiaocrab.net
