# git 命令
## 创建版本库
```bash
git # 显示所有命令

# 设置全局用户 邮箱
git config --global user.name "ryanoligen"
git config --global user.email "ryanoligen@gmail.com"

# 查看当前用户 邮箱
git config user.name
git config user.eamil

git init # 初始化仓库
git add git_command.txt
git commit -m "add git command"

git status # 仓库当前状态
```
## 版本回退
```bash
git diff git_command.md # 工作区与最近一次提交的不同
git diff HEAD -- git_command.md # 工作区与最近一次提交的不同

git log # 提交记录日志
git log --pretty=oneline # 提交记录日志，一行显示
git reflog # 每一次提交的记录

git reset --hard HEAD^ # 退回上一个版本
git reset --hard HEAD^^ # 退回两次以前的提交
git reset --hard HEAD~5 # 退回五次以前的提交
git reset --hard 17fc52b # 退回到提交编号为17fc52b的版本

git checkout <commit-sha1> # HEAD 指向某一个commit-sha1
git switch main # 切换回分支main，也就是让HEAD指针指向main

git switch local # 切换到local分支
git reset <commit-sha1> # local分支指向commit-sha1，指向已有的提交commit-sha1
git switch pushed # 切换到pushed分支
git revert <commit-sha1> # pushed分支撤销commit-sha1提交，但是会生成一次新的提交，提交内容即删除commit-sha1提交的内容


git branch -f dev <commit-sha1> # 强制dev分支指向commit-sha1

git checkout -- git_command.md # 工作区修改，未git add到暂存区，丢弃工作区的修改，相当于退回到最近一次提交的版本
git reset HEAD git_command.md # 已git add到暂存区，未git commit，将暂存区的修改撤销，放回工作区，若要将工作区的修改丢弃，需用上面一条命令

git add test.txt
git commit -m "add test.txt"
# rm test.txt
git checkout -- test.txt # 将删除的文件恢复，本质是用分支上的文件将其恢复
git rm test.txt # 将分支上的对应文件删除
git commit -m "remove test.text"

```

## 远程仓库
[generate an SSH key](https://docs.github.com/en/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
```bash
ssh-keygen -t rsa -C "ryanoligen@gmail.com" # 生成ssh key，需将公钥添加到github中
ssh-keygen -t ed25519 -C "ryanoligen@gmail.com" # ed25519算法生成ssh key

git branch -M main # 将分支名命名为main

# 本地已初始化仓库，现在github上建立仓库，不要勾选readme.md
git remote add origin git@github.com:ryanoligen/tools.git # 将本地仓库与远程做连接
git push -u origin main # 首次推送main分支，远程仓库的默认名为origin
git push origin main # 正常推送本地更新
git push origin on_windows # 推送on_windows分支

git remote # 查看远程库的信息
git remote -v # 查看远程库的详细信息

# 本地没有，从远程clone
git clone git@github.com:ryanoligen/tools.git # 通过ssh方式clone，已添加ssh key，可以放心使用
git clone https://github.com/ryanoligen/tools.git # 通过http方式，需输入用户名密码

```
### 多人协作的规范
- `main` 主分支，时刻与远程同步
- `dev` 开发分支，团队协作，远程同步
- `bug` debug分支，本地
- `feature` 功能分支，视协作方式而定
```bash
git checkout -b dev origin/dev # 创建并切换到dev分支，并与远程的dev分支对应
git branch --set-upstream-to=origin/dev dev # 将本地dev与远程dev关联起来

```

## 分支管理
```bash
git switch -c dev # 创建并切换到分支dev
# git checkout -b dev # 创建并切换到分支dev

git branch dev # 创建新的分支dev
git switch dev # 切换到分支dev上
# git checkout dev # 切换到分支dev上

git branch # 查看所有分支情况

git merge dev # 当前在main分支上，该命令能将dev分支合并到main上
git merge --no-ff -m "merge with no-ff" dev # git merge dev 是fast forward模式合并，参数no-ff，非fast forward合并，在保留dev分支上的提交的基础上会增加一次新的提交，可通过git log --graph查看ff与no-ff的区别


git branch -d dev # 删除dev分支

# 手动解决冲突
git log --graph # 提交历史以及分支图
git log --graph --pretty=oneline --abbrev-commit # 用带参数的git log查看分支合并的情况
```
### 修复bug 暂存工作区修改
[为提交，暂存修改](https://www.liaoxuefeng.com/wiki/896043488029600/900388704535136)
```bash
git stash # 工作区修改，为git add，将修改暂存起来，工作区指向当前分支中最新的提交
git stash list # 查看所有暂存起来的工作区修改
git stach pop # 恢复工作区的修改，并将stash的内容删除
git stash apply # 恢复工作区的修改
git stash apply stash@{0} # 恢复到stash@{0}
git stash drop # 将stash的内容删除

git cherry-pick <commit_sha1> # 在当前分支上，将其他分支上的提交commit_sha1合并过来，会生成一个新的提交

git cherry-pick <commit-sha1>, <commit-sha2> # 可以将不同分支上的若干个提交合并到当前分支上，生成新的提交，内容一致

git switch -c feature # 创建并切换到feature分支
git switch main
git branch -D feature # 未merge的分支，使用参数D，可强行删除

git rebase # 变基操作，能够将分叉的提交历史整理成一条直线，最终的内容保持一致，但提交的commit_sha1会改变

git rebase 
```
## 标签管理
本质上是的某一时刻版本的快照，利用的是commit_sha1
```bash
git branch
git switch on_windows
git tag beta1.0 # 打上beta1.0的标签
git tag beta0.9 commit_sha1 # 在commit_sha1这个版本上打标签
git tag -a beta0.7 -m "version beta0.7 released" commit_sha2 # 在commit_sha2这个版本上打标签，添加注释

git tag # 查看所有的标签
git show beta0.9 # 展示beta0.9版本的详细提交信息

git tag -d beta0.9 # 删除标签beta0.9
git push origin :refs/tags/beta0.9 # 删除远程标签beta0.9

git push origin beta0.7 # 将标签beta0.7推送到远程
git push origin tags # 推送全部标签
```

# Q&A
- 如何使创建的主分支默认名为main，而不是master
- 首次提交后，出现.DS_Store的文件，是什么
- 如何看懂git diff 显示的内容
```bash
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.
-Git tracks changes.
+Git tracks changes of files.
```
- 本地修改，未git add，然后git checkout -- git_command.md 撤销工作区的修改，想要回到修改怎么办
	- 需要将本地修改git stash 暂存起来
- git stash 多次暂存是什么结果
- 在mac上删除on_windows分支，推送远程，windows上pull，会有什么样的结果