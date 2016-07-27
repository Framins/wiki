Vim
====

[Vim][] 是 Vi 的進階版

[Cheat Sheet](http://vim.rtorr.com/)

Mode
----

Vim 模式

|  Mode  |  Description  |  How to Enter  |
|  ----  |  -----------  |  ------------  |
| Normal Mode | 正常模式，平常進來也是這個模式 | 其他模式按 Esc 或 Ctrl + [ |
| Insert Mode | 編輯模式，也就是平常要輸入的時候會使用的模式 | Normal Mode 按 i |
| Replace Mode | 取代模式 | Normal Mode 按 R |
| Visual Mode | 視覺標記模式，就很像平常用滑鼠選取文字一樣 | Normal Mode 按 v |
| Visual Line Mode | 視覺整行標記模式，同 Visual Mode ，差別它是以行為單位 | Normal Mode 按 V |

Install
-----------

    apt-get update && apt-get install vim -y


Command
-----------

#### Cursor movement

    e   jump to the end of a word

    0   jump to the start of the line  
    $   jump to the end of the line

    {   jump to previous paragraph
    }   jump to next paragraph

    gg  go to the first line of the document
    G   go to the last line of the document

#### Cut and paste

    yy  copy a line

    p   paste the clipboard after cursor

    x   delete character
    D   delete to the end of the line
    dd  delete a line

#### Edit

    u       undo
    Ctrl+r  redo

#### Insert mode

    i   insert before the cursor
    A   insert at the end of the line
    o   append a new line below the current line    



#### Visual mode    
    v   start visual mode
    V   start linewise visual mode

    >   shift text right
    <   shift text left

References
----------

* http://www.study-area.org/tips/vim/
* http://blog.vgod.tw/2009/12/08/vim-cheat-sheet-for-programmers/
* http://www.vixual.net/blog/archives/234
* http://linux.vbird.org/linux_basic/0310vi.php
* http://blog.eddie.com.tw/2011/12/26/vim/
* http://blog.eddie.com.tw/2012/04/27/screencast-1-learning-vim-from-the-beginning/
* http://blog.chh.tw/posts/vim-vundle/
* http://stackoverflow.com/questions/3275449/can-a-makefile-have-a-directory-as-a-target

VIM as IDE

* http://blog.csdn.net/wooin/article/details/1858917
* https://github.com/yangyangwithgnu/use_vim_as_ide

`.vimrc` 設定：

參考網頁：

* http://blog.roga.tw/2010/01/%E6%88%91%E7%9B%AE%E5%89%8D%E4%BD%BF%E7%94%A8%E7%9A%84-vimrc-%E8%A8%AD%E5%AE%9A%E6%AA%94/
* http://note.drx.tw/2008/01/vimrc-config.html
* http://blog.longwin.com.tw/2013/03/favorite-vim-vimrc-setup-2013/

Tree 外掛

* http://blog.longwin.com.tw/2009/02/vim-tree-explorer-nerdtree-plugin-2009/

Vundle:

* https://github.com/gmarik/Vundle.vim
* http://www.gtwang.org/2014/04/vundle-vim-bundle-plugin-manager.html

[Vim]: https://zh.wikipedia.org/wiki/Vim
