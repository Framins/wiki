# Console

* http://symfony.com/doc/current/components/console/introduction.html
* http://symfony.com/doc/current/components/console/single_command_tool.html

## Installation

Composer 安裝：

```javascript
{
    "require": {
        "symfony/console": "*"
    }
}
```

## Trick

Symfony Console 有提供類似 [Docker](/docker/README.md) / [Git](/vcs/git/README.md) 的偷懶別名功能

比方說 [Artisan](/framework/laravel/5.0/README.md) 有一個 `key:generate` 的指令的話，可以用下面這些指令代替

    php artisan k:g
    php artisan ke:g
    php artisan k:ge

> 依 `:` 分隔，只要前面比對是唯一的， Symfony Console 都會認可

## Coloring

用 tag 控制輸出的顏色

```php
// green text
$output->writeln('<info>foo</info>');

// yellow text
$output->writeln('<comment>foo</comment>');

// black text on a cyan background
$output->writeln('<question>foo</question>');

// white text on a red background
$output->writeln('<error>foo</error>');
```

自定義 tag

```php
use Symfony\Component\Console\Formatter\OutputFormatterStyle;

$style = new OutputFormatterStyle('red', 'yellow', array('bold', 'blink'));
$output->getFormatter()->setStyle('fire', $style);
$output->writeln('<fire>foo</fire>');
```

## Using Packages Command

https://akrabat.com/using-doctrine-migrations-outside-of-doctrine-orm-or-symfony/
