YAML
====

[YAML][] 是一個可讀性比較高，表達資料的格式。它可以使用縮排來表達資料結構，或是設定檔等。也因為這樣的格式，在 Python / Ruby 裡就很好操作使用

[JSON][] 是它的子集，所以有些東西會跟 JSON 很像。

Usage
-----

基本元素

### hash

使用冒號 `:` 當作是 key-value ，這點跟 JSON 蠻像的，只是 YAML 是用了縮排來表示層級不同， JSON 是用 {} 表示。

```yaml
student:
  name: Miles
  age: 18
```

### list

在 list 元素前，加一個減號 `-` ，表示是 list 的項目：

```yaml
student:
  - Miles
  - Tails
```

### block literal

文字區塊，使用 `|` 然後下一行開始，就可以放入一堆文字了，記得要縮排

```yaml
text: |
  This is a long text,
  Right?
```


[YAML]: http://www.yaml.org/
[JSON]: json.md
