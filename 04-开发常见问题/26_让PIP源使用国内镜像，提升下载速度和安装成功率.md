### 让`pip`源使用国内镜像，提升下载速度和安装成功率。

> 转载: https://www.cnblogs.com/wdz1226/p/10532941.html


#### 对于`Python`开发用户来讲，`pip`安装软件包是家常便饭。但国外的源下载速度实在太慢，浪费时间。而且经常出现下载后安装出错问题。所以把`pip`安装源替换成国内镜像，可以大幅提升下载速度，还可以提高安装成功率。


#### 国内源：新版`ubuntu`要求使用`https`源，要注意。

> 清华：https://pypi.tuna.tsinghua.edu.cn/simple

> 阿里云：http://mirrors.aliyun.com/pypi/simple/

> 中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/

> 华中理工大学：http://pypi.hustunique.com/

> 山东理工大学：http://pypi.sdutlinux.org/

> 豆瓣：http://pypi.douban.com/simple/

### 临时使用：
可以在使用`pip`的时候加参数-i https://pypi.tuna.tsinghua.edu.cn/simple
例如：
```text
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple pyspider
```
这样就会从清华这边的镜像去安装`pyspider`库。
 

#### 永久修改，一劳永逸：

##### Linux 下，修改 ~/.pip/pip.conf (没有就创建一个文件夹及文件。文件夹要加“.”，表示是隐藏文件夹)
```text
[global]
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
 
[install]
trusted-host=mirrors.aliyun.com
```


#### Windows下

##### 找到你 `python` 的安装目录下的文件
##### 注意虚拟环境的话还需要改虚拟环境里的`index.py`
##### `D:\soft\PY\Lib\site-packages\pip_internal\models` 下面的 `index.py` 文件里面将 `PYPI` 的值改为你所需要的源即可，例如改为清华的源。
```text
PyPI = PackageIndex(
'https://pypi.tuna.tsinghua.edu.cn/simple', file_storage_domain='files.pythonhosted.org'
)
```