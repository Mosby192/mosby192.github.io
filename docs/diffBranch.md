#git比较分支差异

##*查看提交日志
使用git log查看提交日志，并可以更具需要设置参数以便更友好的显示；
```
git log --graph --pretty=oneline --abbrev-commit --all
```
其中：
- `--graph` 为显示树状结构
- `--pretty=oneline` 在一行显示（只显示哈希及说明）
- `--abbrev-commit` 仅显示哈希的前一部分
- `--all` 显示所有分支
也可以通过别名设置命令，例如
```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```
使用`git lg`调用；

##查看分支1有而分支2没有的提交

```
git log branch1 ^branch2 //分支1有而分支2没有的提交
```

##查看分支1比分支2多的提交

```
git log branch2...branch1 //分支1比分支2多的提交
```
##对比两个分支的差异

```
git log branch1...branch2 //对比分支1与分支2之间的差异
```
可以使用下列命令查看对应提交属于哪个分支
```
git log --left-right branch1...branch2 //<属于分支1的提交,>属于分支2的提交
```
##*IntelliJ IDEA中查看分支差异

鼠标右击项目 -> git -> compare with branch -> 选择对比分支