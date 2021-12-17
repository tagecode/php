###Nginx 出现504 Gateway Time-out的解决方法

#### 1.问题分析
`Nginx`访问出现504 Gateway Time-out，一般是由于程序执行时间过长导致响应超时，例如程序需要执行90秒，而nginx最大响应等待时间为30秒，这样就会出现超时。 
  
通常有以下几种情况导致

1.程序在处理大量数据，导致等待超时。 
2.程序中调用外部请求，而外部请求响应超时。 
3.连接数据库失败而没有停止，死循环重新连。

出现这种情况，我们可以先优化程序，缩短执行时间。另一方面，可以调大nginx超时限制的参数，使程序可以正常执行。

对于访问超时的设定，nginx与php都有相关的设置，可以逐一进行修改。



#### 2.解决方法
> nginx 配置

nginx.conf 中，设置以下几个参数，增加超时时间

fastcgi_connect_timeout 
fastcgi 连接超时时间，默认60秒

fastcgi_send_timeout 
nginx 进程向 fastcgi 进程发送请求过程的超时时间，默认值60秒

fastcgi_read_timeout 
fastcgi 进程向 nginx 进程发送输出过程的超时时间，默认值60秒 


> php 配置

php.ini

`max_execution_time` 
php脚本最大执行时间 
  
php-fpm

`request_terminate_timeout` 
设置单个请求的超时时间

  
php 程序中可加入 `set_time_limit( seconds )` 设置最长执行时间

例如 `set_time_limit(0)` 表示不超时。