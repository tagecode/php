### PHP 通过正则表达式判断中文字符和全角字符

```php
<?php
$string = '这里是中文';
if (
    preg_match("/[\x{4e00}-\x{9fa5}]+/u", $string) //中文正则
    || 
    preg_match("/[\x{3000}\x{ff01}-\x{ff5f}]/ue", $string) //全角正则
) {
    echo '字符串中包含了中文字符或者全角字符';
}
```