### MySQL 把多个字段合并成一条记录的方法

#### 表`user`的结构
```mysql
CREATE TABLE `user` (
  `id` INT(11) UNSIGNED NOT NULL AUTO_INCREMENT,
  `name` VARCHAR(255) DEFAULT NULL COMMENT '姓名',
  `id_number` VARCHAR(20) NOT NULL COMMENT '身份证号码',
  `birthday` VARCHAR(20) DEFAULT NULL COMMENT '生日',
  `status` TINYINT(1) DEFAULT 1 COMMENT '状态,1:有效,2:无效',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8 ROW_FORMAT=DYNAMIC COMMENT='用户表';
```

#### 姓名和身份证号码合并
```mysql
SELECT GROUP_CONCAT(concat_ws(', ',`name`,`id_number`)) FROM `user` WHERE id IN(11,12) AND `status`=1;
```


#### 姓名和身份证号码合并并排序
```mysql
SELECT GROUP_CONCAT(concat_ws(', ',`name`,`id_number`) ORDER BY id DESC) FROM `user` WHERE id IN(11,12) AND `status`=1;
```