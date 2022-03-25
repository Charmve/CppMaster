# Git 的使用

## 连接到 GitLab
请在进行下面的操作前先将 ssh-key 添加到 GitLab
具体方法可以参考教程

- 安装 Git LFS
Git LFS 是 Git 上管理大文件的一个插件，从而避免 Git 对大文件管理效率不高的问题。为了使用 Git LFS，需要在这里安装。

安装方式：https://git-lfs.github.com/
```
git lfs track *.tar // 将tar 文件加入到大文件管理中
git lfs ls-files // 显示管理的文件
```
track 会生成一个track记录在.gitattributes,但有新的tar文件时，需要重新track
track 以后需要重新add上去，git lfs ls-files 才能显示新track的文件

- Git 的基础操作
这部分网上教程很多，请自行搜索。需要学会如下命令：
```
$ git pull
$ git push
$ git add
$ git commit
$ git rebase
$ git rebase -i
$ git merge
$ git submodule update --init
$ git clone
$ git branch
$ git checkout
$ git fetch

```

简略：
```
 git reset --hard HEAD^

 git clone --recurse-submodules https://github.com/chaconinc/MainProject

 git submodule update --init --recursive

 git config --global user.name "nameVal"

 git submodule add https://devops.momenta.works/Momenta/mf/_git/mjson thirdpart/mjson

 git checkout 6173ec6348cdc91aeb637cdf38252cc9bc3b8732
 
 
 git checkout -b [local_name] [origin/remote_name]
 
 git reset --hard 
 git fsck –lost-found  找回删除掉的文件
 
 git cherry-pick
 git rebase
 git commit --amend



手动建立追踪关系
$ git branch --set-upstream master origin/next

$ git fetch origin master
$ git log -p master..origin/master
$ git merge origin/master
```

## 组内 Git 使用要求
- 默认大家没有 dev 分支权限，需要 merge request 合并入 dev；
- 做一个新功能前，必须创建独立分支。分支命名规则为your_name/feature_name，例如zhangsan/add_python_interface；
- git push 时的 commit 信息格式为[brain_name][jira_id] message，例如[zhangsan/add_python_interface][PS-1211] fix issue of detect() crash。可以用正则\[.+\] .*校验是否合标；
- git push 前必须 rebase 到 dev 的最新节点。我们要保持 log 的线性结构，唯一可接受的 graph 形状为"仙人掌形"；
- 对于一次修改，建议本地 squash 好再 push（参看 git rebase -i）；或者在 merge request 时勾选 squash commits；
“仙人掌形” Git 记录
如下图所示，如果将 git commit 直接连接关系想象成节点之间的边的话，则不允许形成环。各个分支仅可以从主干上长出，且不允许通过 merge 的方式合并回主干。相较于环形，仙人掌形结构比较清晰，在回退记录的时候也很容易操作。具体操作方式，可以参考本文最后的“课后练习“部分。

![image](https://user-images.githubusercontent.com/29084184/160098771-11468c19-ea5b-4e46-9977-d2faa664d325.png)
 
附：一些常见的撤销操作
- 撤销文件[修改] :
命令： git checkout file_name
- 撤销暂存区文件（撤销 git add file）
命令： git reset HEAD 全部撤销
命令： git reset HEAD file_name 对某个文件撤销
- 修该上次提交
也可以说是新一次提交代替上一次提交，也可以说git使用amend选项提供了最后一次commit的反悔。
命令： git commit --amend
- 对于历史提交的 commit -- rebase
往往在项目中，我们会创建工作分支来进行开发，开发完毕后需要将工作分支合并，比如当前有
工作分支: X
主流分支(合并到此分支): A
我们在merge request之前，需要把工作分支中老的提交丢弃,使分支看起来更简洁
命令： git rebase -i A
执行之后将会出现类似这样的：

```
pick **** add ***
pick **** add ***
pick **** add ***
pick **** add ***
```

我们可以使用squash，合并此条记录到前一个记录中，并把commit message也合并进去 。
之后还会跳出一个临时文件，修改commit message;
最后保存退出 (ESC wq)
*补: 随时取消 rebase 事务 [ 未push ]
(git rebase –abort)

- git撤销commit（未git push）
使用命令（git log） 找到需要回退的commit id XXX
使用命令（git reset commit_id） 回退版本
