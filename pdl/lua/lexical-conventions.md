Lexical Conventions
===================

Lua 在風格上，是屬於自由形式的語言。它忽略了空白、換行和註解。其他會被直譯的部分是 `tokens` `names` `keywords`

*Names* (或叫 *identifiers* ) 在 Lua 裡，可以是任何字母、數字或底線，但不可以是數字開頭

*Keywords* 不能當作 Names 使用：

    and       break     do        else      elseif    end
    false     for       function  goto      if        in
    local     nil       not       or        repeat    return
    then      true      until     while
