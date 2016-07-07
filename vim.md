Vim
=======

[Cheat Sheet](http://vim.rtorr.com/)

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
    
