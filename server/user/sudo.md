# sudo

`sudo` 的意思就是 super-user do (something) ，意指超級使用者處理某個指令。

sudo 並不是人人都能用，誰能用、怎麼用，全都被規範在 `/etc/sudoers` 這個檔案裡。因為這個檔案有設定語法，所以要用 `visudo` 去修改。

## Example 1

讓 `john` 可以使用 `root` 的任何指令：

```
root    ALL=(ALL:ALL) ALL  # 原本就有的的
john    ALL=(ALL:ALL) ALL  # 在它後面加這行
```

這裡有三個主要欄位：

* `root` - 使用者帳號
* `ALL=(ALL:ALL)` - 登入來源=(可切換身份)
* `ALL` - 可下達的指令

## References

* http://linux.vbird.org/linux_basic/0410accountmanager.php#visudo