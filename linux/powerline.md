# Powerline

## Install on MacOS

#### Install Python & Powerline

```
$ brew install python
$ easy_install pip
$ pip install --user powerline-status
```

#### Find powerline install Location: 
   
```
$ pip show powerline-status
```

there is a line like Location: {path}

#### Install Fonts

```
$ git clone https://github.com/powerline/fonts.git
$ cd fonts
$ ./install.sh
```

> Terminal use `Inconsolata-g for Powerline`

#### Config bash

Add follow command in `~/.bash_profile` file

```
. {path}/powerline/bindings/bash/powerline.sh
```
> Trouble shooting
 ```  
 if appear 
 ../../../scripts/powerline-config: No such file or directory
 need to find where is `powerline-config`
 then add the inlclude path to $PATH
 e.g. PATH=$PATH:/Users/kaihan.chang/Library/Python/3.7/bin
 ```

#### Config Vim

```
brew install vim
```

Edit `~/.vimrc` , add following code:

```vim
set rtp+={path}/powerline/bindings/vim

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

syntax on
```

#### Create config directory

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
      },
      {
         "function": "powerline_svnstatus.svnstatus",
         "args": {
         "branch_format": "r%s",
         "branch_re": "(\\d+)",
         "line_start": "Revision: "
         },
         "priority": 60
      }
    ]
  }
}
```

## References

* [Powerline Doc](https://powerline.readthedocs.io/en/latest/installation/osx.html)
* [为Bash和VIM配置一个美观奢华的状态提示栏](http://cenalulu.github.io/linux/mac-powerline/)
* [Powerline：漂亮的 Vim 狀態列與 Bash Shell 命令提示字串外掛](https://blog.gtwang.org/linux/powerline-adds-powerful-statuslines-and-prompts-to-vim-and-bash/)
* [安裝 Powerline](http://bearsu.logdown.com/posts/305312-install-the-powerline)
* [Powerline with SVN status](https://github.com/justinludwig/powerline-svnstatus)
