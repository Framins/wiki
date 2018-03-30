# Interface Segregation Principle

介面隔離原則。首先要先了解什麼是介面，介面分兩種：

* Object Interface: 宣告一個 class 後，再 new 出一個實例，這實例上會有可用的方法，是在 class 上定義的，所以 class 也是一種介面
* Class Interface: 平常用 interface 定義的就是屬於這種

隔離也分兩種：

> Clients should not be forced to depend upon interfaces that they don't use.

Client 不應該倚賴它不需要的介面。

> The dependency of one class to another one should depend on the smallest possible interface.

類別間的倚賴關係應該建立在最小的介面上。

這兩個要求，其實就是要介面細化，且介面中的方法盡量要少，而不是建立很肥的介面。

這跟 [SRP][] 還蠻像的，但事實上角度是不同的

* SRP 重視的是職責單一，是業務邏輯上的劃分。
* ISP 重視的是介面裡的方法盡量少。

## Example

>  一個業務邏輯有 10 種方法，把這 10 個方法都放在一個介面裡，並提供給多個模組存取，各模組依規定的權限存取不同的方法。

這個情況下，雖然是符合 SRP ，但是不符 ISP 的。如果要符合 ISP 表示不同的模組應該要有專用的存取介面才對。

[SRP]: single-responsibility-principle.md
