# make

[make](https://www.gnu.org/software/make/) 是 Unix-like 環境下，一個功能強大的輔助編譯工具。

## Concept

隱含規則:

> make 會按照這種“慣例”心照不喧地來運行，那怕 Makefile 中沒有書寫這樣的規則。例如，把 `.c` 文件編譯成 `.o` 文件這一規則，make 會自動推導出這種規則，並生成我們需要的 `.o` 文件

## Make的工作流程

在默認的方式下，也就是我們只輸入make命令。那麼，

* make 會在當前目錄下找名字叫 `Makefile` 或 `makefile` 的文件。
* 如果找到，它會找文件中的第一個目標文件 (target)，並把這個文件作為最終的目標文件。
* 如果目標文件不存在，或是目標文件所依賴的後面的 `.o` 文件的文件修改時間要比目標文件新，那麼他就會執行後面所定義的命令來生成這個文件，如此迭代下去找文件的依賴關係，直到最終編譯出第一個目標文件。

## Structure

```
targets : prerequisites
<tab>command
```

- 命令必須要以 Tab 鍵開始，可以使用 `\` 表示續行。注意，`\` 之後不能有空格！
- 在 makefile 中，行尾如果有一個空白，會造成 make 命令執行錯誤
- Makefile是設計是當有錯誤發生時停止。以`tab`開頭的，都會用shell執行，若失敗，即停止編譯。也因此所有指令需在一行完成。
on general principles makefiles should always `&&` rather than `;`

## SUFFIXS & PHONY

* `.SUFFIXS` 是跟 make 說，有哪些副檔名要加入隱含規則中。
* `.PHONY` 相反，它是跟 make 說，哪些東西是標記，而不是檔案。Only have a list of commands and no dependencies. 
* `$@` 代表 target 本身
* `$<` 代表第一個 dependency

## If statement

make 可以根據條件不同，執行不同的分支。

語法如下：

```
[conditional-directive]
[text-if-true]
else
<text-if-false>
endif
```

第一個 `[conditional-directive]` 表示判斷條件的關鍵字，有四個：

```
ifeq (a, b)   # 比較 a, b 是否相同
ifneq (a, b)  # 比較 a, b 是否不同
ifdef <var>   # 測試 var 是否有設定值
ifndef <var>  # 測試 var 是否沒有設定值
```

> **注意**：在 `[conditional-directive]` 這一行上，多餘的空格是被允許的，但是不能以 `Tab` 鍵做為開始（不然就被認為是命令）。`[else]` 和 `[endif]` 也一樣，只要不是以 `Tab` 鍵開始就行了。

## References

* [A short intro of Makefile](https://www3.nd.edu/~zxu2/acms60212-40212/Makefile.pdf)
* [kezeodsnx:MakeFile介紹](https://kezeodsnx.pixnet.net/blog/post/25125766-makefile)
* http://maxubuntu.blogspot.tw/2010/02/makefile.html
* [How to Use Variables](https://ftp.gnu.org/old-gnu/Manuals/make-3.79.1/html_chapter/make_6.html)
* http://dywang.csie.cyut.edu.tw/moodle23/dywang/linuxProgram/node39.html
* http://stackoverflow.com/questions/3275449/can-a-makefile-have-a-directory-as-a-target

