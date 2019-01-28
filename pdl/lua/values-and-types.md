# Values and Types

Lua 是動態型別語言，所以變數並不會指定型別，值才會有型別。Lua 也支援第一類函數，所以函數也可以當作是變數傳遞。

Lua 有八種基本型別：

* [nil](#nil)
* [boolean](#boolean)
* number
* string
* function
* userdata
* thread
* table

Lua 有提供字串到數字的自動轉換，也就是隱性轉型。

Lua 變數的影響區域有分三種，全域、區域，table 域。預設直接定義變數的話，它會是全域變數。如果想要區域變數的話，需要加上 `local` 修飾

```lua
-- a 是全域變數
a = 10

-- 存取全域變數
print(a)

-- b 是區域變數
local b = 15

-- 存取區域變數
print(b)
```

## nil

`nil` 只有一個值，就是 **nil**，跟大部分語言的 null 一樣，變數的預設值，或是給什麼值都不對的時候，就給 nil 吧。

```lua
-- print 'nil'
local a
print(type(a))

-- print 'nil'
local b = nil
print(type(b))
```

## boolean

`boolean` 有兩個值，**true** / **false**，跟大部分語言一樣。做條件判斷時，`nil` 跟 `false` 都會是假，其他的全都會是真。

```lua
-- print 'boolean'
local a = true
print(type(a))

-- Print 'a is true'
if a then
  print('a is true')
else
  print('a is false')
end

local b = nil
-- Print 'b is false'
if b then
  print('b is true')
else
  print('b is false')
end
```
