#查看git分支

- 查看本地分支`git branch`；
- 查看所有远端分支`git branch -r`；
- 查看所有分支`git branch -a`；

但是远端分支删除后，`git branch -a`命令仍然能够查看到已经删除的分支；

使用`git remote show origin`命令查看远端分支信息，显示本地和远端不同步的地方；
```
* 远程 origin
  获取地址：url
  推送地址：url
  HEAD分支：master
  远程分支：
    master                    已跟踪
    refs/remotes/origin/dev   过时（使用 'git remote prune' 来移除）
  为 'git pull' 配置的本地分支：
    master  与远程 master 合并
  为 'git push' 配置的本地引用：
    master  推送至 master  (最新)
```
使用`git pull`与`git push`同步本地与远端的分支；

使用`git remote prune origin`更新远程的分支到本地，这样远程已经被删除的分支，本地就不会再看见了。