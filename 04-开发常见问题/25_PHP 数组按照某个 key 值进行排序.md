### PHP 数组按照数组的某个 `key` 值进行排序

#### 代码示例
```php
<?php
/**
 * 根据数组的`key`排序
 *
 * @param $array
 * @param $keys
 * @param string $sort
 * @return array
 */
function arraySortByKey($array, $keys, $sort = 'asc'){
    $newArr = $valArr = array();
    foreach ($array as $key => $value) {
        if (!isset($value[$keys])) {
            return $array;
        }
        $valArr[$key] = $value[$keys];
    }
    //先利用keys对数组排序，目的是把目标数组的key排好序
    ($sort == 'asc') ? asort($valArr) : arsort($valArr);
    reset($valArr); //指针指向数组第一个值
    foreach ($valArr as $key => $value) {
        $newArr[$key] = $array[$key];
    }
    return $newArr;
}

//调用排序函数
$arr = [
    ['a'=>1,'b'=>4,'c'=>9],
    ['a'=>5,'b'=>3,'c'=>2],
    ['a'=>2,'b'=>3,'c'=>5],
    ['a'=>8,'b'=>8,'c'=>6],
];

print_r(arraySortByKey($arr,'b'));
```