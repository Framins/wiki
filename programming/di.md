# Dependency injection

[Dependency injection][] 譯名有很多，最常聽到的叫 **依賴注入** 。

## Foreword

> 以下用 Pokémon Go 當情境來寫程式

對寫程式的直覺而言，會寫到哪 new 到哪。

```php
// 神奇寶貝大師
class Master
{
    public function command()
    {
        $pokemon = new Pikachu();
        $pokemon->skill();
    }
}

// 皮卡丘
class Pikachu
{
    public function skill() {
        // Thunder Attack
    }
}
```

但，哪天你拿到一隻 Bulbasaur 想用它的技能，程式勢必得這麼改

```php
// 神奇寶貝大師
class Master
{
    public function command()
    {
        // $pokemon = new Pikachu();
        $pokemon = new Bulbasaur();
        $pokemon->skill();
    }
}

// 皮卡丘
class Pikachu
{
    public function skill() {
        // Thunder Attack
    }
}

// 妙蛙種子
class Bulbasaur
{
    public function skill() {
        // Solar Beam
    }
}
```

這裡會發現，程式裡 Master 跟 Pikachu 是直接相依 (不可能都當 Master 了只能馴服 Pikachu 吧)，因此當想換 Bulbasaur 時，會發生要改程式的問題。這是違反物件導向的 [Loose coupling][] 原則。因為也不可能每換一隻 Pokémon 就得改一次程式，所以比較合理的做法是，要由外部來控制 Master 要用哪隻 Pokémon 。

使用流程控制是其中一種解決方法，而依賴注入是另一種：對 Master 而言，它需要的 Pokémon (依賴)是由其他模組給它的(注入)，而不是自己產生。


```php
// 神奇寶貝大師
class Master
{
    public function command(Pokemon $pokemon)
    {
        $pokemon->skill();
    }
}

// 所有 Pokémon 都有技能
interface Pokemon
{
    public function skill();
}

// 皮卡丘
class Pikachu
{
    public function skill() {
        // Thunder Attack
    }
}

// 妙蛙種子
class Bulbasaur
{
    public function skill() {
        // Solar Beam
    }
}
```

改成這樣，當 Master 下指令的那一刻前，再決定要用哪隻 Pokémon 就行了，

> Master 能指揮所有 Pokémon 才合理啊！

[Dependency injection]: http://en.wikipedia.org/wiki/Dependency_injection
[Loose coupling]: https://en.wikipedia.org/wiki/Loose_coupling
