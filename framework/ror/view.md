# View

`erb` 樣版到底是什麼鬼

## link_to

link_to 是 rails 內建的方法，可以輸出超連結

```erb
<%= link_to title, link %>
```

link 如果是首頁的話，要打 root_path (router 也必須要設 root 才行)
