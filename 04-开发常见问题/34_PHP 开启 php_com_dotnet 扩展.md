### PHP Windows 开启 php_com_dotnet 扩展

> 查看`php.ini`中是否已经开启了`com.allow_dcom = true`

> 从`php/ext`/里面查找一下有没有这个`php_com_dotnet.dll`这个文件

> 然后查找这个`php.ini`里面查找下`#extension=php_com_dotnet.dll` 把前面的#号去掉,如果找不到就复制,手动添加一下然后重新开启`php`

> 输出`phpinfo()`或者`php -i|grep com_dotnet` 有返回`com_dotnet`表示安装成功

> 应用示例:
```php
<?php
// 注意word.application 是电脑中必须有word文档才可以的
// 如果没错的话应该会显示`Microsoft Word`说明COM扩展已经安装完成了!
$com = new COM('word.application');
echo $com;
```