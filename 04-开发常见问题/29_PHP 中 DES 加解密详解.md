### PHP 中 DES 加解密详解

###### 转载: https://www.jianshu.com/p/546137b8ac7a

一、简介
DES 是对称性加密里面常见一种，全称为 Data Encryption Standard，即数据加密标准，是一种使用密钥加密的块算法。密钥长度是64位(bit)，超过位数密钥被忽略。所谓对称性加密即加密和解密密钥相同，对称性加密一般会按照固定长度，把待加密字符串分成块，不足一整块或者刚好最后有特殊填充字符。

跨语言做 DES 加密解密经常会出现问题，往往是填充方式不对、编码不一致或者加密解密模式没有对应上造成。常见的填充模式有： pkcs5、pkcs7、iso10126、ansix923、zero。加密模式有：DES-ECB、DES-CBC、DES-CTR、DES-OFB、DES-CFB。

作为一个软件开发者，可以通过工具测试 DES 加密解密，这里推荐一个在线工具：
http://tool.chacuo.net/cryptdes

二、实现
PHP 提供了 Mcrypt 系列函数来实现 DES 的加解密，但该扩展中的函数陆续被废弃，自 PHP 7.2.0 起，会移到 PECL。

所以本代码用了更通用的 OPENSSL 方式实现 DES 的加解密，具体的实现和使用代码如下：
```php
<?php

/**
 * openssl 实现的 DES 加密类，支持各种 PHP 版本
 */
class DES
{
    /**
     * @var string $method 加解密方法，可通过 openssl_get_cipher_methods() 获得
     */
    protected $method;

    /**
     * @var string $key 加解密的密钥
     */
    protected $key;

    /**
     * @var string $output 输出格式 无、base64、hex
     */
    protected $output;

    /**
     * @var string $iv 加解密的向量
     */
    protected $iv;

    /**
     * @var string $options
     */
    protected $options;

    // output 的类型
    const OUTPUT_NULL = '';
    const OUTPUT_BASE64 = 'base64';
    const OUTPUT_HEX = 'hex';


    /**
     * DES constructor.
     * @param string $key
     * @param string $method
     *      ECB DES-ECB、DES-EDE3 （为 ECB 模式时，$iv 为空即可）
     *      CBC DES-CBC、DES-EDE3-CBC、DESX-CBC
     *      CFB DES-CFB8、DES-EDE3-CFB8
     *      CTR
     *      OFB
     *
     * @param string $output
     *      base64、hex
     *
     * @param string $iv
     * @param int $options
     */
    public function __construct($key, $method = 'DES-ECB', $output = '', $iv = '', $options = OPENSSL_RAW_DATA | OPENSSL_NO_PADDING)
    {
        $this->key = $key;
        $this->method = $method;
        $this->output = $output;
        $this->iv = $iv;
        $this->options = $options;
    }

    /**
     * 加密
     *
     * @param $str
     * @return string
     */
    public function encrypt($str)
    {
        $str = $this->pkcsPadding($str, 8);
        $sign = openssl_encrypt($str, $this->method, $this->key, $this->options, $this->iv);

        if ($this->output == self::OUTPUT_BASE64) {
            $sign = base64_encode($sign);
        } else if ($this->output == self::OUTPUT_HEX) {
            $sign = bin2hex($sign);
        }

        return $sign;
    }

    /**
     * 解密
     *
     * @param $encrypted
     * @return string
     */
    public function decrypt($encrypted)
    {
        if ($this->output == self::OUTPUT_BASE64) {
            $encrypted = base64_decode($encrypted);
        } else if ($this->output == self::OUTPUT_HEX) {
            $encrypted = hex2bin($encrypted);
        }

        $sign = @openssl_decrypt($encrypted, $this->method, $this->key, $this->options, $this->iv);
        $sign = $this->unPkcsPadding($sign);
        $sign = rtrim($sign);
        return $sign;
    }

    /**
     * 填充
     *
     * @param $str
     * @param $blocksize
     * @return string
     */
    private function pkcsPadding($str, $blocksize)
    {
        $pad = $blocksize - (strlen($str) % $blocksize);
        return $str . str_repeat(chr($pad), $pad);
    }

    /**
     * 去填充
     * 
     * @param $str
     * @return string
     */
    private function unPkcsPadding($str)
    {
        $pad = ord($str{strlen($str) - 1});
        if ($pad > strlen($str)) {
            return false;
        }
        return substr($str, 0, -1 * $pad);
    }

}


$key = 'key123456';
$iv = 'iv123456';

// DES CBC 加解密
$des = new DES($key, 'DES-CBC', DES::OUTPUT_BASE64, $iv);
echo $base64Sign = $des->encrypt('Hello DES CBC');
echo "\n";
echo $des->decrypt($base64Sign);
echo "\n";

// DES ECB 加解密
$des = new DES($key, 'DES-ECB', DES::OUTPUT_HEX);
echo $base64Sign = $des->encrypt('Hello DES ECB');
echo "\n";
echo $des->decrypt($base64Sign);
```

三、相关链接
> DES 加解密工具：http://tool.chacuo.net/cryptdes

> Mcrypt 官方文档：http://php.net/manual/zh/book.mcrypt.php

>OPENSSL 加解密函数官方文档：

>> openssl_encrypt：http://php.net/manual/zh/function.openssl-encrypt.php

>> openssl_decrypt：http://php.net/manual/zh/function.openssl-decrypt.php