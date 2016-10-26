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

References
----------

* [鳥哥的Linux私房菜](http://linux.vbird.org/linux_basic/0320bash.php#variable_var)
