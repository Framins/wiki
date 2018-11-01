# 指令小技巧

## 改目錄下所有檔案的屬性

從 Windows 複製過來的檔案預設都會是 0777 ，對強迫症的人來說，是件很要命的事。但只要執行下面兩行指令就能全部調整正常了：

    find . -type d -print -exec chmod 755 {} \;
    find . -type f -print -exec chmod 644 {} \;

## 查目錄所佔的容量

查目錄或檔案所佔的容量可以使用 `du` ：

    du -sh /path/to/directory

> `-s` 是只 show 整個目錄的容量， `-h` 是顯示人類習慣看的單位。

## 只顯示目錄

    ls -d */
