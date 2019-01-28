# fish

## Mac 安裝方法

使用 `brew` 指令安裝：

```bash
brew install fish
```

`brew` 會把 fish 安裝在 `/usr/local/bin/fish` 這個路徑。而 `brew` 並不會自動在 `/etc/shells` 新增新的 shell，因此要先手動在 `/etc/shells` 檔案加入這行：

```
# /etc/shells
/usr/local/bin/fish
```

接著下 `chsh` 指令把預設 shell 改成 fish 即可：

```bash
chsh -s /usr/local/bin/fish
```

## Debian / Ubuntu / Mint 安裝方法

使用 `apt` 指令安裝：

```bash
sudo apt update
sudo apt install -y fish
```

`apt` 會自動把新 shell 加入 `/etc/shells`，接著使用 `chsh` 改成 fish 即可： 

```bash
chsh -s /usr/bin/fish
```

## Fisher 套件管理系統

套件管理系統 [Fisher](https://github.com/jorgebucaran/fisher)

* [fish-nvm](https://github.com/FabioAntunes/fish-nvm) - nvm wrapper，因為只是 wrapper，所以 nvm 還是得自己裝，並要設定 NVM_DIR 與 nvm_prefix 兩個環境變數

> 注意：使用 `fish-nvm` 有可能會造成 JetBrains 的 terminal 發生錯誤，因為它先呼叫 conf.d 的設定後，才載 function 裡的設定，目前 workaround 解是改 JetBrains 的的 plugin，把兩個順序對調即可。

## shell 語法

基本上可以參考[官方文件](https://fishshell.com/docs/current/tutorial.html#tut_conditionals)

## References

* [Fish shell 入门教程](http://www.ruanyifeng.com/blog/2017/05/fish_shell.html)
