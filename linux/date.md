# date

最常見的日期顯示方式

```bash
date "+%Y/%m/%d %H:%M:%S"
```

單改日期

```bash
date -s 2014/01/01
```

單改時間

```bash
date -s 23:59:59
```

直接改全部

```bash
date "+%Y%m%d%H%M.%S"  # 產生 201401012359.59 ，這個格式可以再拿來當 input
date 201401012359.59
```

網路直接校時

```bash
ntpdate watch.stdtime.gov.tw
ntpdate time.stdtime.gov.tw
```

## Reference

 * http://maxding.blogspot.tw/2009/07/linux.html
