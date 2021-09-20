# git

## stash

### git stash show

git stash show stash@{1}：查看改了哪些个文件
git stash shwo id ：(这个ID貌似在drop的时候会给出，但是我觉得别的方法应该也能查找到)。查看每个文件改动的细节

### git stash apply

git stash apply：只应用，不pop出去

### git stash drop

git stash drop误操作恢复：git stash apply commitId

### git stash push

`git stash push -m` 暂存某一个文件

### git stash pop

冲突：

````js
git stash pop stash@{1} 
// 解决冲突resolve your conflict(s)
git add 冲突文件
git restore --staged .
git stash drop stash@{1}
````

`git stash pop stash@{1}`

恢复指定的进度到工作区。stash_id是通过`git stash list`命令得到的

## branch

git reflog show --date=iso feature/opt_waybill_batch：查看分支记录与创建时间（最后一行即为初始创建时间）

