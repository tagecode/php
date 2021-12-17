### ThinkPHP 框架`could not find driver`错误处理方法

#### 报错如下
```text
:(

could not find driver
错误位置
FILE: D:\myProject\ThinkPHP\Library\Think\Db\Driver.class.php 　LINE: 109

TRACE
#0 D:\myProject\ThinkPHP\Library\Think\Db\Driver.class.php(109): E('could not find ...')
#1 D:\myProject\ThinkPHP\Library\Think\Db\Driver.class.php(1059): Think\Db\Driver->connect()
#2 D:\myProject\ThinkPHP\Library\Think\Db\Driver\Mysql.class.php(50): Think\Db\Driver->initConnect(true)
#3 D:\myProject\ThinkPHP\Library\Think\Model.class.php(134): Think\Db\Driver\Mysql->getFields('auth_rule')
#4 D:\myProject\ThinkPHP\Library\Think\Model.class.php(122): Think\Model->flush()
#5 D:\myProject\ThinkPHP\Library\Think\Model.class.php(1455): Think\Model->_checkTableInfo()
#6 D:\myProject\ThinkPHP\Library\Think\Model.class.php(97): Think\Model->db(0, '', true)
#7 D:\myProject\ThinkPHP\Common\functions.php(586): Think\Model->__construct('AuthRule')
#8 D:\myProject\App\Admin\Service\AuthRuleService.class.php(18): D('AuthRule')
#9 D:\myProject\ThinkPHP\Library\Think\Model.class.php(74): Admin\Service\AuthRuleService->_initialize()
#10 D:\myProject\ThinkPHP\Common\functions.php(586): Think\Model->__construct('AuthRule')
#11 D:\myProject\App\Admin\Controller\AdminController.class.php(131): D('AuthRule', 'Service')
#12 D:\myProject\App\Admin\Controller\IndexController.class.php(37): Admin\Controller\AdminController->_initialize()
#13 D:\myProject\ThinkPHP\Library\Think\Controller.class.php(41): Admin\Controller\IndexController->_initialize()
#14 D:\myProject\ThinkPHP\Common\functions.php(680): Think\Controller->__construct()
#15 D:\myProject\ThinkPHP\Library\Think\App.class.php(89): controller('Index', '')
#16 D:\myProject\ThinkPHP\Library\Think\App.class.php(202): Think\App::exec()
#17 D:\myProject\ThinkPHP\Library\Think\Think.class.php(120): Think\App::run()
#18 D:\myProject\ThinkPHP\ThinkPHP.php(97): Think\Think::start()
#19 D:\myProject\index.php(50): require('D:\\jxjyadmin_gi...')
#20 {main}

ThinkPHP3.2.3 { Fast & Simple OOP PHP Framework } -- [ WE CAN DO IT JUST THINK ]
```

#### 这种情况一般是因为数据库连接的扩展没有打开

#### 修改`php.ini`文件
 > windows 下 `extension=php_pdo_mysql.dll` 删除前面的冒号
 > Linux修改php.ini文件`extension=pdo_mysql.so` 删除前面的冒号, 将前面的分号去掉,问题得到解决

#### 本质：“ 3.2.3 数据库类和驱动采用 PDO 重写了，因此无论是什么数据库都是基于 PDO 实现的”