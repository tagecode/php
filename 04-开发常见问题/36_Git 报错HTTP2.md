### Git  报错  HTTP/2

#### HTTP/2 stream 1 was not closed cleanly before end of the underlying stream。



通过排查发现，是 `git` 默认使用的通信协议出现了问题，可以通过将默认通信协议修改为 `http/1.1` 来解决该问题。

```text
 git config --global http.version HTTP/1.1
```

> 参考资料：https://blog.csdn.net/zz00008888/article/details/123529805