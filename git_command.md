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
git diff git_command.md
```
## 远程仓库
## 分支管理
## 标签管理

# Q&A
- 如何使创建的主分支默认名为main，而不是master
- 首次提交后，出现.DS_Store的文件，是什么