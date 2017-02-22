# Powerline

## Install on MacOS

Install Python & Powerline

```
$ brew install python
$ pip install powerline-status
```

Install Fonts

```
$ git clone https://github.com/powerline/fonts.git
$ cd fonts
$ ./install.sh
```

Add follow command in `~/.bash_profile` file

```
. /usr/local/lib/python2.7/site-packages/powerline/bindings/bash/powerline.sh
```

Edit `~/.vimrc` , add following code:

```vim
set rtp+=/usr/local/lib/python2.7/site-packages/powerline/bindings/vim

" These lines setup the environment to show graphics and colors correctly.
set nocompatible
set t_Co=256

let g:minBufExplForceSyntaxEnable = 1
python from powerline.vim import setup as powerline_setup
python powerline_setup()
python del powerline_setup

if ! has('gui_running')
   set ttimeoutlen=10
   augroup FastEscape
      autocmd!
      au InsertEnter * set timeoutlen=0
      au InsertLeave * set timeoutlen=1000
   augroup END
endif

set laststatus=2 " Always display the statusline in all windows
set guifont=Inconsolata\ for\ Powerline:h14
set noshowmode " Hide the default mode text (e.g. -- INSERT -- below the statusline)
```

Create config directory

```
$ mkdir -p ~/.config/powerline/themes/shell
$ vim ~/.config/powerline/themes/shell/default.json
```

Config Example:

```json
{
  "segments": {
    "left": [
      {
        "function": "powerline.segments.shell.mode"
      },
      {
        "function": "powerline.segments.common.net.hostname",
        "priority": 10
      },
      {
        "function": "powerline.segments.common.env.user",
        "before": "♥ ",
        "priority": 30
      },
      {
        "function": "powerline.segments.common.env.virtualenv",
        "priority": 50
      },
      {
        "function": "powerline.segments.common.time.date",
        "args": {
          "format": "%H:%M"
        },
        "priority": 10
      },
      {
        "function": "powerline.segments.shell.cwd",
        "priority": 10
      },
      {
        "function": "powerline.segments.shell.jobnum",
        "priority": 20
      },
      {
        "function": "powerline.segments.shell.last_pipe_status",
        "priority": 10
      },
      {
        "function": "powerline.segments.common.vcs.branch",
        "priority": 40
      }
    ]
  }
}
```

## Reference

* [Powerline Doc](https://powerline.readthedocs.io/en/latest/installation/osx.html)
* [为Bash和VIM配置一个美观奢华的状态提示栏](http://cenalulu.github.io/linux/mac-powerline/)
* [Powerline：漂亮的 Vim 狀態列與 Bash Shell 命令提示字串外掛](https://blog.gtwang.org/linux/powerline-adds-powerful-statuslines-and-prompts-to-vim-and-bash/)
* [安裝 Powerline](http://bearsu.logdown.com/posts/305312-install-the-powerline)
