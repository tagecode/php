### Git 合并某个提交 commit 到指定的分支上

#### 合并单个`commit`到指定的分支上
```text
git log  //查看提交的日志，复制要合并的那个分支的commit id</span>
git checkout 要合并的分支  // 切换到要合并的分支上
git cherry-pick 上面复制的那个要合并的commit id  // 提交该commit到当前分支
```