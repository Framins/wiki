# fish

Mac 安裝

```
brew install fish
```

執行 `fish` 即可啟動，但如果要改成預設的話，要先把下面這行加入 `/etc/shells`

```
/usr/local/bin/fish
```

然後下 `chsh` 指令

```bash
chsh -s /usr/local/bin/fish
```

套件管理系統 [Fisher](https://github.com/jorgebucaran/fisher)

* [fish-nvm](https://github.com/FabioAntunes/fish-nvm) - nvm wrapper，因為只是 wrapper，所以 nvm 還是得自己裝，並要設定 NVM_DIR 與 nvm_prefix 兩個環境變數

使用 fish-nvm 還有可能會造成 JetBrains 的 terminal 發生錯誤，因為它先呼叫 conf.d 的設定後，才載 function 裡的設定，目前 workaround 解是改 JetBrains 的的 plugin ，把兩個順序對調即可。

## 自動補全提示

預設會提示上一次執行的指令

## 語法

基本上可以參考[官方文件](https://fishshell.com/docs/current/tutorial.html#tut_conditionals)

## References

# [Fish shell 入门教程](http://www.ruanyifeng.com/blog/2017/05/fish_shell.html)
