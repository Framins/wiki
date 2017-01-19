Variable
=====

All System Variables
-------------

```bash
env
```

User Defined Variables
-------------

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

Built-in shell variables
-------------

    Variable 	Use
    $? 	  Stores the exit value of the last command that was executed.
    $# 	  Stores the number of command-line arguments that were passed to the shell program.
    $* 	  Stores all the arguments that were entered on the command line ($1 $2 ...).
    $@ 	  Stores all the arguments that were entered on the command line, individually quoted ("$1" "$2" ...).
    $0 	  Stores the first word of the entered command (the name of the shell program).
    
e.g.

    ./command -yes -no /home/username

- $# = 3
- $* = -yes -no /home/username
- $@ = array: {"-yes", "-no", "/home/username"}
- $0 = ./command
- $1 = -yes


References
----------

* [鳥哥的Linux私房菜](http://linux.vbird.org/linux_basic/0320bash.php#variable_var)
