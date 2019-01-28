# Class Diagram

類別圖的主要目的是用圖形表示類別間的結構，範例圖形如下：

![](http://plantuml.com/plantuml/png/RO-n3e8m48Ptd-8I5eo1E9iuiEdYmk1SobaQe6tQKwD6dzssGGE4zUxx__lEjL8PPbaFl6FE5KHMLbV28zUgb4-4xIekmA0s7S9h1P3dOAvL9paOgmrQUlYHds-02OGTI4K3PUMD4Swm31gKeY5FNZhD_gmcv8JrZ4v0iJwqEc-cn00ptePRK_G3ztdnVZ_nxP4QNVzi1L8XC5qlAO_9B927M1tXHUjn8067TFBQQHcbumiXUTEoddumZdt2dVFypliB)

```uml
@startuml
skinparam classAttributeIconSize 0
class people {
  .. public property ..
  + age : int
  .. private property ..
  - height : float
  .. protected property ..
  # name : string
  .. package property ..
  ~ weight : float
  ==
  .. public method ..
  + getAge() : int
  .. private method ..
  - getHeight() : float
  .. protected method ..
  # setName(String name) : void
  .. package method ..
  ~ getWeight() : float
}
@enduml
```

能見度的表示說明：

* `+` public
* `-` private
* `#` protected
* `~` package

## Relationships

五種關係

* Shared aggregation
* Composite aggregation
* Association
* Generalization
* Implementation

### Shared aggregation

聚合關係，聚合代表的是兩邊生命週期可以不一致，以下例來說，B 結束了，A 還是可以讓其他類別使用

![](http://plantuml.com/plantuml/png/AqvEp4bLC38mK2ZFJ2d9u4hEIImkLd24qavSZWgw-GfE0000)

```uml
@startuml
scale 200 width
class A
class B
A -o B
@enduml
```

### Composite aggregation

組合關係，組合代表的是兩邊生命週期一致，以下例來說，B 結束了，A 也會跟著結束

![](http://plantuml.com/plantuml/png/AqvEp4bLC38mK2ZFJ2d9u4hEIImkLd24qavSZWgwMWfE0000)

```uml
@startuml
scale 200 width
class A
class B
A -* B
@enduml
```

### Association

結合關係，表示兩邊是有關係的，比方說 A 使用了 B，B 不能使用 A ：

![](http://plantuml.com/plantuml/png/AqvEp4bLC38mK2ZFJ2d9u4hEIImkLd24qavSZWgwTWfE0000)

```uml
@startuml
scale 200 width
class A
class B
A -> B
@enduml
```

### Generalization

一般化，或是物件導向常說的「繼承」，比方說 A 繼承 B ：

![](http://plantuml.com/plantuml/png/AqvEp4bLC38mK2ZFJ2d9u4hEIImkLd3aIamgBYbAJ2vHW0WuSJagwDROAJW10000)

```uml
@startuml
scale 200 width
class A
abstract class B
A -|> B
@enduml
```

### Implementation

實作關係，比方說 A 實作 B ：

![](http://plantuml.com/plantuml/png/AqvEp4bLC38mK2ZFJ2d9u4hEIImkLd3aoimhIIrAIqnELN3YSbJGgx5JS080)

```uml
@startuml
scale 200 width
class A
interface B
A .|> B
@enduml
```
