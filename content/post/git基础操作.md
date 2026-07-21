+++
title = "首次推送本地项目到 GitHub"
date = 2026-07-18T14:01:17+08:00
author = "Sola"
keywords = ["git", ""]
cover = ""
summary = "Git是一个开源的版本控制器，速度快，性能高。学习git基础操作对程序员的生产生活有很大帮助。"
+++
Git 是一个分布式版本控制系统，而“仓库（repository）”是 Git 用来存储项目所有文件及历史记录的空间。  
你可以把代码提交到本地仓库，再将本地仓库的变更推送到远程仓库（如 GitHub），也可以从远程仓库拉取最新代码。  
## 1. 初始化仓库  init 
要使用仓库先得建仓库。  
首先，进入你的项目根目录，执行 `git init`，这会在当前目录下创建一个隐藏的 `.git` 文件夹，标志着本地仓库初始化完成。  
```
git init
```
## 2. 添加文件并提交 add 
仓库有了就可以提交内容。  
使用 `git add <文件>` 将文件添加到暂存区，然后使用 `git commit -m "提交信息"` 将暂存内容保存为一个新版本。  
例如：  
```
git add .               # 暂存所有改动的文件
git commit -m "first commit"
```
首次推送前，至少需要一次提交，否则推送会因没有可推送的分支而失败。  
## 3. 关联远程仓库 remote 
为了将本地仓库与 GitHub 上的远程仓库关联，使用：  
`git remote add origin <远程仓库URL>`
`origin` 是默认的远程仓库别名，你可以替换成其他名字。URL 可以在 GitHub 仓库页面点击 “Code” 按钮复制。
## 4.推送 push 
使用 `git push -u origin main` 将本地的 `main` 分支推送到远程仓库，并通过 `-u` 设置上游跟踪。  
设置跟踪后，后续只需执行 `git push` 即可。  
推送前，先用 `git branch` 确认当前分支名（可能是 `master`），确保与远程分支对应。  
```
git push -u origin main
git push
git branch
```
## 5.修改与更新 commit 
首次提交以后，需要修改和更新。  
添加文件到暂存区：
```
git add .  #将当前目录下所有未被忽略的文件（包括新文件、修改过的文件）添加到暂存区
```
提交到本地仓库：  
```
git commit -m[message] #把暂存区的文件添加到本地仓库，message是备注信息
git commit [file1][file2]... -m[message] #指定暂存区文件添加到仓库
git commit -a -m #直接提交新修改的文件（不包括新文件）
```