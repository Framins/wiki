# Laravel 5.0

* http://zhuzhichao.com/post/2015/03/laravel-5-and-4-difference/

## Basic

* [Started](started.md)

## Event

Event trigger Handler

> 類似 [Observer Pattern](/design-pattern/observer-pattern.md)

如果有 Queue 的話，它會把 Handler 一個一個丟進去照順序執行；但如果沒有的話就會直接 trigger
