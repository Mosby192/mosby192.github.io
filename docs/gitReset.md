#git撤销回滚

##未添加到暂存区

修改未提交到暂存区，撤销工作区所做的修改；
```
git checkout -- filename //撤销filename文件的修改（git checkout filename）
git checkout -- . //撤销所有文件的修改（git checkout .）
```
##已提交到暂存区

修改已提交到暂存区，但是还没有commit；
```
git reset HEAD filename //撤销filename文件的修改
git reset HEAD //撤销所有文件的修改
```
##已commit提交

修改已commit提交到本地仓库，但是还没有push到远端；
```
git reset --hard HEAD^ //回滚到上一次提交记录
git reset --hard commitid //回滚到指定commit记录
```
其中参数的区别：
- `--soft` //撤销commit提交，文件修改仍然保留在暂存区（如果要继续提交，直接commit）
- `--mixed` //撤销commit及暂存区提交，文件修改只保留在工作区（之后提交需要重新add，commit）
- `--hard` //撤销commit，暂存区及本地工作区的修改（慎用，会丢失修改）

如果只想修改最后一次commit的注释信息，或者是合并修改到最后一次commit，可以使用如下命令：
```
git commit --amend -m "commit message"
```
##已push到远端

###不希望保留提交记录

不希望保留commit提交记录，达到回滚修改的目的；
####删除远端分支再提交

回滚本地提交记录到指定commit，删除远端分支（最好先做好备份），再把本地分支推送到远端：
```
git reset --hard HEAD^ //回滚到上一次提交记录（或者git reset --hard commitid）
git push origin :branchname //删除远端分支（等效于git push origin --delete branchname） 
```
####强行push远端分支

回滚本地提交记录到指定commit，之后强行推送到远端：
```
git reset --hard HEAD^ //回滚到上一次提交记录（或者git reset --hard commitid）
git push -f origin branchname //强行推送本地分支到到远端（git push -f）
```
###希望保留提交记录

希望保留提交记录，但是回滚代码到之前的状态；
```
git revert HEAD //回滚上一次提交
git revert commitid //回滚到指定commit提交记录
```
之后执行`git push`,就可以撤销修改，但是会保留修改及回滚的commit记录；这是最安全及推荐的方式。