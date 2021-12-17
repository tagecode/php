### Git 合并单个文件到某个分支

#### 如果需要`merge`单独文件, 可采用打补丁方式来比较不同分支上的文件差异。 

>命令
>>```
>>git checkout -p <branch> 文件名
>>    Apply this hunk to index and worktree [y,n,q,a,d,/,e,?]? (是否将补丁加入暂存区, 键入y 加入)
>>```

>实例

>在当前分支(比如目前是在`master`分支)上去拉`test`分支上的`config.php`文件
>>```
>>git checkout -p test App/Api/Conf/config.php
>>```

#### 这样就只将该文件的最新内容拉取下来, 然后再从当前分支`commit & push`即可只将该文件推送至远程分支。
#### 一般应用场景是有**个别**代码已经改好了跟其他修改在`dev`或者`test`上,但是这个代码修改比较急要先上而其他的在一起的修改还在测试。
#### 处理紧急需要上线的修改比较好的方式是从`master`分支拉`hotfix`，改完再合并回`master`。