Installation
============

[官方網站](http://git-scm.com/)

安裝在 Windows
--------------

Windows 的主程式官方網站上就有了，基本上就下一步猛按即可。不過以下還是講幾個小設定 (版本1.8.1.2)：

1. 下載完後點擊兩下安裝
2. **Welcome to the Git Setup Wizard** 按 Next。
3. **Information** 按 Next。
4. **Select Components** 這裡要注意一點： Git 預設會整合檔案總管的右鍵功能表，如果想用其他的 GUI，可以 [Windows Explorer integration] 取消掉；如果想要用文字模式的話，可以只選 [Git Bash Here] 就好。
5. **Adjusting your PATH environment** 這是要用文字模式的話才會考慮選哪個的問題，第一個是用自帶的Git Bash，用起來跟Linux的Bash很像；第二個是用 Windows 的命令列；第三個是使用 Windows 命令列，但也能使用 Unix-like 的指令。
6. **Choosing the SSH executable** 選擇 SSH 加密執行檔要用哪一個，第一個是用 Git 自帶的 OpenSSH；第二個是外部軟體。
7. **Configuring the line ending conversions** 檔尾換行字元要如何轉換，第一個是 checking out 會自動轉成 Windows 格式，committing 會自動轉成 Unix 格式；第二個是全都會轉成 Unix 格式；第三個是不做任何轉換。
8. 安裝檔案完後就是問要不要看 Releaselog

文字模式只要打開 Git Bash 即可開始下命令操作了。

GUI 的部分，除了 Git 自帶的之外，還有幾種可以參考：

* [TortoiseGit](https://code.google.com/p/tortoisegit/)
* [SmartGit](http://www.syntevo.com/smartgithg/)
* [EGit for Eclipse](http://www.eclipse.org/egit/)
* [Git Extensions](https://code.google.com/p/gitextensions/)
* [GitHub for Windows](http://windows.github.com/)
* [SourceTree](http://www.sourcetreeapp.com/)

GUI 大部分應該都會推薦 TortoiseGit，當然這部分還是自己使用喜歡比較重要。

以下用 TortoiseGit 1.8.1.0 64bit 安裝做說明，先假設 Git 主程式已經裝好了之後：

1. 下載完後點擊兩下安裝
2. **Welcome to the TortoiseGit 1.8.1.0 (64 bit) Setup Wizard**，按Next。
3. **Information**，按Next。
4. **Choose SSH Client**，選擇SSH加密執行檔要用哪一個，第一個是用TortoiseGit自帶，第二個是Git預設的OpenSSH，這要看產生key是由哪個執行檔產生，再選那個即可。
5. **Custom Setup**，設定安裝位置。
6. **Ready to Install**，按Install下去吧。
7. 安裝檔案完後就是問要不要看Changlog而已，結束。

安裝在 Linux
------------

Linux 麻煩在於很多不同的 Distributions，不過還是可以小小歸類一下啦！

### Debian/Ubuntu

主程式安裝指令：

    sudo apt-get install git-core

GUI安裝指令：

    sudo apt-get install gitk

apt 上也有很多 Git 相關的 GUI 也可以多去試試，像 giggle 等。

### Fedora

主程式安裝指令：

    yum install git-core

GUI 部分沒找到相關文件...

安裝在 Mac
----------

文字模式就沒什麼好說了，GUI大概找了一下有下面這些可以選

* [GitHub for Mac](http://mac.github.com/)
* [GitX (L)](http://gitx.laullon.com/)
* [git-cola](http://git-cola.github.io/)
* [SourceTree](http://www.sourcetreeapp.com/)
