# Variable

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