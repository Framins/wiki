Bitbucket
=========

[Bitbucket][] 是一個用於使用版本控制系統項目的共享虛擬主機服務。與 [GitHub][] 提供的服務特點不大相同，如：

* 除了支援 Git 外，還有 Mercurial
* 無限制的私人檔案庫
* 無限制空間
* 免費帳號只能 5 人共同管理同個專案，不過這可以利用 pull request 的方法解決
* 可以匯入 GitHub 的檔案庫或 SSH Key 等 (限使用 GitHub 帳號註冊的情況)

其他功能都大同小異，如 wiki 、 issues tracker 和其他模組等。

申請帳號
--------

申請帳號除了可以建立全新的帳號外，也能透過 GitHub 等其他帳號登入。

比較需要注意的是，如果是建立全新帳號，會有兩種選擇：一個是個人帳號，一個是團隊帳號。而 GitHub 則是不需要建立團隊帳號，是直接以個人帳號名義做管理的。

新增SSH Key
-----------

先產生 SSH Key

打開 public key 檔，把內容全部copy。

再來連到官網登入後，點右上角個人頭像 > `Manage account` > 左邊列表的 `SSH keys` > 右邊 `Add key` 按鈕

Label 是打上一個名稱方便日後管理。public key 的內容全部複製後貼到 Key 的欄位中。最後再按 `Add key` 即可新增新的一組 SSH key 。

如果有用 TortoiseGit 的話，記得到 Setting > Network 把下面的 ssh 程式改為 C:\Program Files\Git\bin\ssh.exe ，它才會去找剛剛建立的 SSH keys 。

[Bitbucket]: https://bitbucket.org/
[GitHub]: github.md
