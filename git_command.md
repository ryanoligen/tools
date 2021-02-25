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
```
## 远程仓库
## 分支管理
## 标签管理

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