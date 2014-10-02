# Link
- https://github.com/barbushin/php-console
- [live demo](http://php-console.com/instance/examples/)

# Usage
- 初始化：插入以下 code
```php
require_once(__DIR__ . '/../libraries/PhpConsole/__autoload.php');
PhpConsole\Helper::register();
```

- 即可印出想印的 variable
```php
PC::debug($var);
```
