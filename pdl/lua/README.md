Lua
===

[Lua 官方網站](http://www.lua.org/about.html)所提到的特色：

* Lua 既小且快又不用錢。
* Lua 是非常易學易用的的一種語言。
* Lua 與 C/C++ 的整合性很好。
* Lua 的可移植性極高。
* Lua 是用 ANSI C 寫的

LuaJIT
------

[LuaJIT][] 全名是 *Lua Just-In-Time Compiler* 它跟 Lua 5.1 相容，重要的是它的效能比 Lua 改善很多。

Basic
-----

目前官方網站看到有三個分支：

* [5.1](http://www.lua.org/manual/5.1/)
* [5.2](http://www.lua.org/manual/5.2/)
* [5.3](http://www.lua.org/manual/5.3/)

安裝好後，直接打 `lua` 即可啟動 Lua 的指令互動環境，再按 Ctrl + C 即可離開

    $ lua
    Lua 5.1.5  Copyright (C) 1994-2012 Lua.org, PUC-Rio
    >

此筆記是以 5.1 做測試的

* [Lexical Conventions](lexical-conventions.md)
* [Values and Types](values-and-types.md)
* Statements
* Expressions
* Visibility Rules

Reference
---------

* [Scripting 系統概論與 Lua 簡介](http://blog.monkeypotion.net/gameprog/beginner/introduction-of-scripting-system-and-lua)
* [官方 Manual](http://www.lua.org/manual/5.1/)
* [Lua教學](http://www2.kimicat.com/lua%E6%95%99%E5%AD%B8)
* [LuaUnit](http://luaunit.readthedocs.io/en/latest/)
* [Lua coding style](http://wuzhiwei.net/lua_style_guide/)

[LuaJIT]: http://luajit.org/luajit.html
