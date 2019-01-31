# Config

第一次安裝 git 一定要設定使用者名稱和 email才能做 commit

    git config --global user.name "username"
    git config --global user.email "username@example.com"

另外可以加上一些顏色的設定，會比單色更清楚

    git config --global color.diff auto
    git config --global color.status auto
    git config --global color.branch auto
    git config --global color.log auto

指定 commit 時的預設編輯器

    git config --global core.editor vim

指定 merge 工具

    git config --global merge.tool vimdiff

建議設定大小寫敏感，原因請參考[這裡](https://blog.avisi.nl/2013/03/27/stop-ignoring-my-capitals-git/)

    git config --global core.ignorecase false

設定下 push 指令的預設方法：

    git config --global push.default matching # 沒指定分支的話，會把所有 fetch 下來名稱 match 的全 push 上去，聽起來很可怕
    git config --global push.default current # 只 push 目前所在的 branch
    git config --global push.default simple # 如果有設 upstream 會優先執行，如果沒有才會使用 current，看起來比較適合

檢查目前設定值的列表

    git config --list

查詢設定值，如查看目前使用首的名稱

    git config user.name

設定值的檔案會存在 `/etc/gitconfig` 及 `~/.gitconfig`，差別只是一個是所有使用者的 global，另一個是使用者個人的 global。

## .gitignore

某些檔案可能不需要被 git 記錄下來，如暫存檔、編譯後的執行檔等，這時可以加入此檔，並記錄哪些類型檔案，git 就會自動跳過不去 add

如不同系統裡，都會出現一些特殊的 cache 檔，可以寫這個檔來自動忽略。

```gitignore
# Global/OSX.gitignore
.DS_Store

# Global/Windows.gitignore
Thumbs.db
Desktop.ini
```

.gitignore 參考：

* [Rails](/framework/ror/gitignore.md)
* [Zend Framework 1](/framework/zf1/gitignore.md)

## .gitconfig

修改 `~/.gitconfig` 的範例：

```ini
[user]
	name = MilesChou
	email = jangconan@gmail.com
[core]
	editor = vim
	ignorecase = false
[push]
	default = simple
[color]
	diff = auto
	status = auto
	branch = auto
	log = auto
[alias]
	lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cblueby %an %Cgreen(%cr)%Creset'
```

## .bash_profile

參考 [iHower 的 blog](http://ihower.tw/blog/archives/5436) 上的好東西，Linux/MAC 系統修改家目錄的 `~/.bash_profile`

```bash
function git_branch {
    ref=$(git symbolic-ref HEAD 2> /dev/null) || return;
    echo "("${ref#refs/heads/}") ";
}

function git_since_last_commit {
    now=`date +%s`;
    last_commit=$(git log --pretty=format:%at -1 2> /dev/null) || return;
    seconds_since_last_commit=$((now-last_commit));
    minutes_since_last_commit=$((seconds_since_last_commit/60));
    hours_since_last_commit=$((minutes_since_last_commit/60));
    minutes_since_last_commit=$((minutes_since_last_commit%60));

    echo "${hours_since_last_commit}h${minutes_since_last_commit}m ";
}

PS1="[\[\033[1;32m\]\w\[\033[0m\]] \[\033[0m\]\[\033[1;36m\]\$(git_branch)\[\033[0;33m\]\$(git_since_last_commit)\[\033[0m\]$ "
```

## Auto Completion

Ubuntu 預設會裝，Mac 的裝法如下：

    brew install bash-completion

然後在修改 `~/.bash_profile` 加入下面程式碼：

```bash
if [ -f $(brew --prefix)/etc/bash_completion ]; then
    . $(brew --prefix)/etc/bash_completion
fi
```

接著重開終端機即可
