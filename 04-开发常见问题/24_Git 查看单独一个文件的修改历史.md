### Git 查看单独一个文件的修改历史

#### 通过`git log` 查看`commit id`

#### 1.查看`filename`相关的`commit`记录 
##### 注意分支 , 分支不一样结果不一样

>命令
>>```
>>git log filename
>>```


#### 2.显示每次提交的`diff`

>命令
>>```
>>git log -p filename
>>```


#### 3.只看某次提交中的某个文件变化，可以直接加上`filename`

>命令
>>```
>>git show abde9804bbd9725b5dece57f8cbece4a96b9f80b filename
>>```