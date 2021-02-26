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
```bash
ssh-keygen -t rsa -C "ryanoligen@gmail.com" # 生成ssh key，需将公钥添加到github中

# 本地已初始化仓库，现在github上建立仓库，不要勾选readme.md
git remote add origin git@github.com:ryanoligen/tools.git # 将本地仓库与远程做连接
git push -u origin main # 首次推送main分支
git push origin main # 正常推送本地更新


# 本地没有，从远程clone
git clone git@github.com:ryanoligen/tools.git # 通过ssh方式clone，已添加ssh key，可以放心使用
git clone https://github.com/ryanoligen/tools.git # 通过http方式，需输入用户名密码
```
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
- 本地修改，未git add，然后git checkout -- git_command.md 撤销工作区的修改，想要回到修改怎么办