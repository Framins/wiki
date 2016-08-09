# Slim Framework 3.x

* Hello World

## Dependency Container

Slim built-in container 是 [Pimple][] ，官方也有提到可以用其他的像 [Acclimate][] 或 [PHP-DI][]

Slim container 除了 Pimple 外，其他都需要實作必要 service ，可以參考[官網](http://www.slimframework.com/docs/concepts/di.html)

### Environment

Environment 是 Slim/App 跑 run 所需的環境參數，如 HTTP method / uri 等等。

Environment 可以利用自己建立的 Mock 去取代原本程式會讀取的，可以用這個方法來完成 REST API 測試

> 可參考： http://blog.framins.com/implement-slim-rest-unit-test/

## References

* [User Guide](http://www.slimframework.com/docs/)

[Pimple]: /pdl/php/pimple.md
[Acclimate]: https://github.com/jeremeamia/acclimate-container
[PHP-DI]: http://php-di.org/doc/frameworks/slim.html
