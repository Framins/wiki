# Callable

## Example

```php
// Define function test
function test($title, Callable $callable) {
    $callable($title);
}

// Define callable function
$func = function($title) {
    echo $title;
};

// Execute
test("hi", $func);
```

The above example will output:

```
hi
```
