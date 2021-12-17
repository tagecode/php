### ThinkPHP3.2.3 的模型查询的一个问题

#### 查询数据库的结果集的时候注意查询条件`where`

```php
<?php
$result = D('Student', 'Model')
                ->where(['`pkid`' => array('GT', 0)])
                ->limit(10)
                ->order('pkid asc')
                ->select();
?>
```

#### 如上所示`pkid`，注意是在单引号里面的``pkid``这样查询是无效的。所以应该直接使用`'pkid'`就好。
#### 使用 ` 是为了让自定义表字段跟数据库关键字相同时方便区别开，避免解析查询时引起歧义错误，但使用时应该特别谨慎。

#### 正确查询
```php
<?php
$result = D('Student', 'Model')
                ->where(['pkid' => array('GT', 0)])
                ->limit(10)
                ->order('pkid asc')
                ->select();
?>
```