# 指令小技巧

## 改目錄下所有檔案的屬性

從 Windows 複製過來的檔案預設都會是 0777 ，對強迫症的人來說，是件很要命的事。但只要執行下面兩行指令就能全部調整正常了：

    find . -type d -print -exec chmod 755 {} \;
    find . -type f -print -exec chmod 644 {} \;

> `Chmod` change attributes from a file/folder

 * chmod 666 means that all users can read and write but cannot execute
 * chmod 777 allows all actions for all users
 * chmod 744 allows only owner to do all actions; group and other users are allowed only to read
    
        permission to:  owner      group      other     
                        /¯¯¯\      /¯¯¯\      /¯¯¯\
        octal:            6          6          6
        binary:         1 1 0      1 1 0      1 1 0
        what to permit: r w x      r w x      r w x
    
        binary         - 1: enabled, 0: disabled
    
        what to permit - r: read, w: write, x: execute
    
        permission to  - owner: the user that create the file/folder
                         group: the users from group that owner is member
                         other: all other users



## 查目錄所佔的容量

查目錄或檔案所佔的容量可以使用 `du` ：

    du -sh /path/to/directory

> `-s` 是只 show 整個目錄的容量， `-h` 是顯示人類習慣看的單位。

## 只顯示目錄

    ls -d */
