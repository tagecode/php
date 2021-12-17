### Guzzle Curl Peer's Certificate issuer 请求错误

#### 报错详情
```php
["cURL error 60: Peer's Certificate issuer is not recognized. (see http:\/\/curl.haxx.se\/libcurl\/c\/libcurl-errors.html)"]
```

#### 说明
选项 | 说明
- | -
CURLOPT_SSLCERT | set SSL client certificate
CURLOPT_SSLKEY | specify private keyfile for TLS and SSL client cert
CURLOPT_CAINFO | path to Certificate Authority (CA) bundle


#### 解决办法
> 1. 不验证证书
```php
<?php
$client = new Client(['verify' => false]);
//$response = $client->request('POST', $url, ['form_params' => $params]);
//$response = $client->request('GET', $url);
?>
```

> 2.验证证书
```html
将证书文件内容拷贝到 /etc/pki/tls/certs/ca-bundle.crt 文件之中
```


#### 参考资料
> https://blog.csdn.net/weixin_40006394/article/details/84790775

#### 扩展阅读
> GitHub: https://github.com/guzzle/guzzle

> 中文文档: https://guzzle-cn.readthedocs.io/zh_CN/latest/