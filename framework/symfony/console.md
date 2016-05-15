Console
=======

* http://symfony.com/doc/current/components/console/introduction.html
* http://symfony.com/doc/current/components/console/single_command_tool.html

Installation
------------

Composer 安裝：

```javascript
{
    "require": {
        "symfony/console": "*"
    }
}
```

Coloring
--------

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
