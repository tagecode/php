### PHP 去除数组里的空值

> array_filter
 
> (PHP 4 >= 4.0.6, PHP 5, PHP 7)
 
> array_filter — 用回调函数过滤数组中的单元 

> 更多的用法,请参考: https://www.php.net/manual/zh/function.array-filter.php

#### 示例
```php
<?php

$entry = array(
             0 => 'foo',
             1 => false,
             2 => -1,
             3 => null,
             4 => ''
          );

print_r(array_filter($entry));
?> 
```

#### 示例输出
```php

以上例程会输出：


Array
(
    [0] => foo
    [2] => -1
)

```