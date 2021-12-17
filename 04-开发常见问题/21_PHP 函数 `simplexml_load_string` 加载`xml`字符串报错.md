### php 函数 `simplexml_load_string` 加载`xml`字符串报错


#### 报错详情
```text
Warning: simplexml_load_string(): Entity: line 1: parser error : switching encoding: encoder error 

PHP Warning:  simplexml_load_string(): input conversion failed due to input error, bytes 0x80 0xE5 0x85 0xB7

```

#### 这是因为字符串编码问题导致的 , 要注意 `simplexml_load_string()` 所在文件的编码以及字符串`xml`的编码 , 必要时使用 `mb_convert_encoding()` 函数进行转码 , 详情请查看 https://www.php.net/manual/en/function.mb-convert-encoding.php