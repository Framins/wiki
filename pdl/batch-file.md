Batch File
==========

DOS 因為指令不分大小寫，跟 Unix-like 不一樣；為了表示彼此不同，所以 DOS 的指令通常會用全大寫表示

批次檔的副檔名可以為 `.BAT` 或 `.CMD`，BAT 是 DOS 下的批次檔，CMD 是 NT 內核命令列下的另一種批次檔案，所以必需在有 NT 內核的 Windows 下才能用( NT/2000/XP/2003 等)。

ECHO
----

    ECHO [ON/OFF/string]

ON/OFF 是設定 `C:\>` 和批次檔的指令要不要顯示  
不加參數是查看目前狀況  
string 的話就會回傳 string 訊息  
總合以上所說....你不能只傳 ON/OFF 訊息....

此指令設定的部分通常使用在批次檔的一開始先把指令關掉，就不會有雜七雜八的目錄在煩你了。

#### e.g.

```batch
ECHO OFF
ECHO 程式執行中...請稍候....
```

第一個 ECHO OFF 指令可以使用 @ 符號來抑止它出現：

```batch
@ECHO OFF
ECHO 程式執行中...請稍候....
```

REM
---

批次檔的註解

#### e.g.

```batch
REM 批次檔 test1-1
@ECHO OFF
ECHO 程式執行中...請稍候....
```

PAUSE
-----

程式暫停

#### e.g.

```batch
REM 批次檔 test1-1
@ECHO OFF
ECHO 程式執行中...請稍候....
REM 輸出一些東西：
ECHO 1 + 1 = 2
PAUSE
```

SHIFT
-----

有時會需要給批次檔一點引數做處理，批次檔使用時可以使用參數標記 %0 ~ %9，分別代表了第1個引數~第10個引數，其中%0代表的是指令本身。

但有時候要需要用超過 10 引數該怎麼辦？  
這時可以用 SHIFT  
它做的動作就是：丟掉 ← %0 ← %1 ← %2 ← %3 ← %4 ......  
可加上 `/n` 選項，方向會是相反的

#### e.g.

```batch
REM 批次檔 test1-1
@ECHO OFF
ECHO 程式執行中...請稍候....
REM 輸出你輸入的東西：
ECHO %1 和 %2
PAUSE
```

IF
---

三種格式：

一、

    IF [NOT] "parameters/string" == "parameters/string" COMMAND

`NOT` 代表不等於；`COMMAND` 代表成立時會做的命令

注意到這裡的雙引號其實是非必要  
它可以避免輸入含有空白的參數  
相對的輸入時，如果需要含空白的話，可以使用雙引號括著

#### e.g.

```batch
REM 批次檔 test1-1
@ECHO OFF
ECHO 程式執行中...請稍候....
REM 輸出你輸入的東西：
ECHO %1 和 %2
IF "%1" == "%2" ECHO 相等
IF NOT "%1" == "%2" ECHO 不等
PAUSE
```

二、

    IF [NOT] EXIST [PATH]FILE COMMAND

`NOT` 同上；`PATH` 可以是相對也可以是絕對；`FILE` 為檔名；`COMMAND` 同上

#### e.g.

```batch
REM 批次檔 test1-2
REM TYPE為顯示檔案內容
IF EXIST "%1" TYPE "%1"
```

三、

    IF ERRORLEVEL VALUE COMMAND

用來測試它的上一個 DOS 命令的返回值

`ERRORLEVEL` 為程式執行結束後的返回值，應該是指像 C 語言程式最後的return吧。
`VALUE` 返回值 
`COMMAND` 執行命令

GOTO
----

無條件跳至某一個標記繼續執行，標記為一個:(冒號)和字元所組成。

#### e.g.

```batch
REM 批次檔 test1-2
REM TYPE為顯示檔案內容
IF EXIST "%1" GOTO E
IF NOT EXIST "%1" GOTO NE
:E
TYPE "%1"
GOTO END
:NE
ECHO 沒這個檔
GOTO END
:END
```

CHOICE
------

    CHOICE [/C choices] [/N] [/CS] [/T timeout /D choice] [/M text]

參數列表: 

* /C choices 指定要創建的選項列表。預設為"YN"。
* /N 在提示符中隱藏選項列表。提示前面的消息得到顯示，選項依舊處於啟用狀態。
* /CS 分大小寫的選項。在預設是不分大小寫的。
* /T timeout 選擇前暫停的秒數。0 到 9999。如果指定了 0，就不會有暫停。
* /D choice 指預設認選項。字元必須在用 /C 選項指定的一組選擇中; 同時，必須用 /T 指定 nnnn。
* /M text 指定提示之前要顯示的消息。如果沒有指定，工具只顯示提示。

此語法需配合IF ERRORLEVEL做使用

#### e.g.

```batch
CHOICE /? 
CHOICE /C YNC /M "確認請按 Y，否請按 N，或者取消請按 C。" 
CHOICE /T 10 /C ync /CS /D y 
CHOICE /C ab /M "選項 1 請選擇 a，選項 2 請選擇 b。" 
CHOICE /C ab /N /M "選項 1 請選擇 a，選項 2 請選擇 b。"
```

FOR
---

重覆執行

    FOR %%a IN (file1 file2 file3) DO COMMAND

虛擬變數必須以兩個百分號（%%）起頭，IN後面為參數列，DO 後面跟著要執行的命令

#### e.g.

```batch
@echo off
FOR %%a IN (test_a.bat test_b.bat test_c.bat) DO DEL %%a
```

CALL
----

呼叫其他批次檔
