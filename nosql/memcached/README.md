Memcached
=========

參考： 

使用 telnet 連接 server 就可以操作了

    telnet 127.0.0.1 11211

stats
-----

stats 可以看各種狀態

    > stats
    STAT pid 1048
    STAT uptime 102991  # 系統已運行的時間
    STAT time 1427872847  # 系統上的時間
    STAT version 1.4.14 (Ubuntu)
    STAT libevent 2.0.21-stable
    STAT pointer_size 64
    STAT rusage_user 7.986106
    STAT rusage_system 4.737812
    STAT curr_connections 5
    STAT total_connections 8315  # 曾經建立的連線累計
    STAT connection_structures 8
    STAT reserved_fds 20
    STAT cmd_get 4599  # 下 get 指令的次數
    STAT cmd_set 896  # 下 set 指令的次數
    STAT cmd_flush 0  # 下 flush_all 指令的次數
    STAT cmd_touch 0
    STAT get_hits 2927
    STAT get_misses 1672
    STAT delete_misses 13
    STAT delete_hits 57
    STAT incr_misses 0
    STAT incr_hits 0
    STAT decr_misses 0
    STAT decr_hits 0
    STAT cas_misses 0
    STAT cas_hits 0
    STAT cas_badval 0
    STAT touch_hits 0
    STAT touch_misses 0
    STAT auth_cmds 0
    STAT auth_errors 0
    STAT bytes_read 355369
    STAT bytes_written 7959350
    STAT limit_maxbytes 67108864
    STAT accepting_conns 1
    STAT listen_disabled_num 0
    STAT threads 4
    STAT conn_yields 0
    STAT hash_power_level 16
    STAT hash_bytes 524288
    STAT hash_is_expanding 0
    STAT expired_unfetched 191
    STAT evicted_unfetched 0
    STAT bytes 71564  # 快取資料大小(bytes)
    STAT curr_items 214  # 目前儲存的item數
    STAT total_items 828  # 從運行到現在,曾有過的item數累計
    STAT evictions 0  # 為了取得空間，而剔除item的數量
    STAT reclaimed 261
    END

add
---

新增快取資料，資料不存在的時候，才會執行成功

    add [key] [] [過期時間] [資料長度]

輸入 enter 後，第二行是要打資料的內容，這裡的長度要跟上面的資料長度一模一樣才行

> 回傳 `STORED` 代表儲存成功；回傳 `NOT_STORED` 代表儲存失敗。

    > add data 0 60 5
    miles
    STORED

get
---

由 key 取得資料

    get [key]

如果 key 裡面沒資料的話，會直接回傳 `END`

    > get data
    VALUE data 0 5
    miles
    END

Reference
---------

* http://xyz.cinc.biz/2015/02/memcached-command-example.html?m=1
