Config
======

第一次安裝 git 一定要設定使用者名稱和 email才能做 commit

```bash
git config --global user.name "username"
git config --global user.email "username@example.com"
```

另外可以加上一些顏色的設定，會比單色更清楚

```bash
git config --global color.diff auto
git config --global color.status auto
git config --global color.branch auto
git config --global color.log auto
```

指定 commit 時的預設編輯器

```bash
git config --global core.editor vim
```

指定 merge 工具

```bash
git config --global merge.tool vimdiff
```

設定下 push 指令的預設方法：

```bash
git config --global push.default matching # 沒指定分支的話，會把所有 fetch 下來名稱 match 的全 push 上去，聽起來很可怕
git config --global push.default current # 只 push 目前所在的 branch
git config --global push.default simple # 如果有設 upstream 會優先執行，如果沒有才會使用 current ，看起來比較適合
```

檢查目前設定值的列表

```bash
git config --list
```

查詢設定值，如查看目前使用首的名稱

```bash
git config user.name
```

設定值的檔案會存在 `/etc/gitconfig` 及 `~/.gitconfig` ，差別只是一個是 global ，一個是使用者的

.gitignore
----------

某些檔案可能不需要被 git 記錄下來，如暫存檔、編譯後的執行檔等，這時可以加入此檔，並記錄哪些類型檔案， git 就會自動跳過不去 add

如不同系統裡，都會出現一些特殊的 cache 檔，可以寫這個檔來自動忽略。

```gitignore
# Global/OSX.gitignore
.DS_Store

# Global/Windows.gitignore
Thumbs.db
Desktop.ini
```

.gitconfig
----------

修改 `~/.gitconfig` 的範例：

```ini
[user]
	name = MilesChou
	email = jangconan@gmail.com
[core]
	editor = vim
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

.bashrc
-------

此設定檔放在 `~/.bashrc` ，是進入 CLI 時，會先執行的檔案：

```
alias ls='ls --color -F'
alias grep='grep --color=auto'
alias fgrep='fgrep --color=auto'
alias egrep='egrep --color=auto'

export CLICOLOR='true'
export LSCOLORS='Gxfxaxdxcxegedabagacad'
# colorful man page
export PAGER="`which less` -s"
export BROWSER="$PAGER"
export LESS_TERMCAP_mb=$'\E[38;5;167m'
export LESS_TERMCAP_md=$'\E[38;5;39m'
export LESS_TERMCAP_me=$'\E[38;5;231m'
export LESS_TERMCAP_se=$'\E[38;5;231m'
export LESS_TERMCAP_so=$'\E[38;5;167m'
export LESS_TERMCAP_ue=$'\E[38;5;231m'
export LESS_TERMCAP_us=$'\E[38;5;167m'
# git & PS1
export GIT_PS1_SHOWDIRTYSTATE=1
#=============================

if [ $EUID = 0 ]; then
        export PS1='\[\033[01;31m\]\u\[\033[01;37m\]@\[\033[01;32m\]\h\[\033[00m\]: \[\033[01;31m\]\W\[\033[00m\]$(__git_ps1) \[\033[01;35m\]\$ \[\033[39m\] '
else
        export PS1='\[\033[01;34m\]\u\[\033[01;37m\]@\[\033[01;32m\]\h\[\033[00m\]: \[\033[01;31m\]\W\[\033[00m\]$(__git_ps1) \[\033[01;35m\]\$ \[\033[39m\] '
fi

export PATH='/usr/bin:/bin:/usr/sbin:/sbin:/usr/local/bin:/usr/local/sbin'

# 顯示預設 git diff 結果
function git_diff() {
        git diff --no-ext-diff -w "$@" | vim -R -
}
```

在 [iHower 的 blog](http://ihower.tw/blog/archives/5436) 上看到的一個好東西， Linux/MAC 系統修改家目錄的 `~/.bash_profile`

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

Auto Completion
---------------

Ubuntu 預設會裝， Mac 的裝法如下：

```bash
brew install bash-completion
cp /usr/local/etc/bash_completion.d/git-completion.bash ~/.git-bash-completion.sh
```

然後在修改 `~/.bash_profile` 最下面加入這一行

```bash
[ -f ~/.git-bash-completion.sh ] && . ~/.git-bash-completion.sh
```

或是

```bash
if [ -f $(brew --prefix)/etc/bash_completion ]; then
    . $(brew --prefix)/etc/bash_completion
fi
```

完成，重開終端機即可
