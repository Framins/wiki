# Variable

## All System Variables

```bash
env
```

## User Defined Variables

```bash
# 等號兩邊不能直接接空白字元
myhome="/home/v/vivek"

echo "$myhome"
# or
echo "${myhome}"
```

指令

```bash
version=$(uname -r)
# or
version=`uname -r`

echo $version
```

## Built-in shell variables

    Variable 	Use
    $? 	  the exit value of the last command that was executed.
    $# 	  the number of command-line arguments that were passed to the shell program.
    $* 	  all the arguments that were entered on the command line ($1 $2 ...).
    $@ 	  all the arguments that were entered on the command line, individually quoted ("$1" "$2" ...).
    $0 	  the first word of the entered command (the name of the shell program).
    
e.g.

    ./command -yes -no /home/username

* $# = 3
* $* = -yes -no /home/username
* $@ = array: {"-yes", "-no", "/home/username"}
* $0 = ./command
* $1 = -yes

## Delete

`#` 基本的用法

```bash
$(variable#string)
```

* `variable` 是變數名
* `string` 是欲刪除的字串，可以搭配萬用字元 `?` `*` 使用

實際的作用是：由左至右，刪除符合字串中**最短的**那一個（因為有萬用字元）

舉例：

```bash
SOME_FILE=some_file.png
ANOTHER_FILE=another${SOME_FILE#some}

echo ${ANOTHER_FILE}
# See 'another_file.png'
```

`%` 則是相反

舉例：

```bash
PNG_FILE=somefile.png
SVG_FILE=${PNG_FILE%.png}.svg

echo ${SVG_FILE}
# See 'somefile.svg'
```

## Replace

## References

* http://benjr.tw/96951
* [鳥哥的Linux私房菜](http://linux.vbird.org/linux_basic/0320bash.php#variable_var)
