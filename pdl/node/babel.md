# Babel

## `.babelrc`

首先要準備這個檔案，讓 Babel 知道專案要怎麼轉碼

```json
{
  "presets": [],
  "plugins": []
}
```

`presets` 代表要載入的轉碼規則，可以參考[官方文件](https://babeljs.io/docs/plugins/preset-latest/)安裝對應的外掛

比方說：

```json
{
  "presets": [
    "es2015"
  ]
}
```

## References

* http://guoyongfeng.github.io/my-gitbook/index.html
