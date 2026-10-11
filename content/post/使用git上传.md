+++
title = "了解git"
date = 2026-08-22T09:45:36+08:00
author = "Sola"
keywords = ["", ""]
cover = ""
summary = ""
+++

# Git 基础操作指南

## 1. 什么是 Git

Git 是一个**分布式版本控制系统**，用于跟踪文件的修改历史，方便多人协作和代码管理。

- **仓库（Repository）**：存储项目所有文件及历史记录的空间。
- **工作目录（Working Directory）**：你电脑上能看到的项目文件夹。
- **暂存区（Staging Area）**：提交前临时存放文件改动的地方。
- **本地仓库（Local Repository）**：保存在本地的提交历史。
- **远程仓库（Remote Repository）**：托管在服务器上的仓库，如 GitHub、GitLab。

## 2. 安装与配置

首次使用 Git 前需要设置用户信息：

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱"
```

查看当前配置：

```bash
git config --list
```

## 3. 初始化仓库

进入项目根目录，执行：

```bash
git init #初始化仓库  
git add . #暂存所有文件
git commit -m "版本信息" #创建提交
#如果是首次创建还应在此次关联仓库↓
git remote add origin <你的仓库地址> #关联远程仓库
git push -u origin main   # 如果默认分支是 main
# 或 git push -u origin master
```

这会在当前目录创建隐藏的 `.git` 文件夹，表示本地仓库初始化完成。

## 4. 基本工作流程

```bash
git status          # 查看当前状态：哪些文件被修改、哪些未跟踪
git add <文件名>    # 将指定文件添加到暂存区
git add .           # 将当前目录下所有未忽略的文件添加到暂存区
git commit -m "提交说明"  # 将暂存区的内容提交到本地仓库
```

**注意**：`git add .` 不会添加被 `.gitignore` 忽略的文件。

## 5. 关于 `git commit -a`

`git commit -a` 可以跳过手动 `git add`，自动暂存**已跟踪文件**的修改和删除，然后提交。

```bash
git commit -a -m "提交说明"
```

**限制**：

- 只对**已跟踪文件**（之前至少 `git add` 过一次的文件）有效。
- 新建的未跟踪文件不会被自动提交，需要先手动 `git add` 一次。
- 相当于先执行 `git add -u`，再执行 `git commit`。

**建议**：初学者尽量使用 `git add` + `git commit` 两步，明确要提交的内容。

## 6. 远程仓库操作

### 添加远程仓库

```bash
git remote add origin <远程仓库URL>
```

`origin` 是远程仓库的默认别名，可以自定义。URL 可在 GitHub 仓库页面点击 “Code” 按钮复制。

### 推送本地提交到远程

```bash
git push -u origin main
```

- `-u` 参数设置本地分支跟踪远程分支，之后可直接使用 `git push`。
- 分支名可能是 `main` 或 `master`，可用 `git branch` 查看当前分支。

### 拉取远程更新

```bash
git pull origin main
```

或直接 `git pull`（如果已设置跟踪）。

### 克隆远程仓库

```bash
git clone <远程仓库URL>
```

无需 `git init`，克隆后自动关联远程。

## 7. 分支基础

```bash
git branch              # 查看本地分支
git branch <分支名>     # 创建新分支
git switch <分支名>     # 切换到指定分支（Git 2.23+）
git checkout <分支名>   # 切换分支（旧命令）
git merge <分支名>      # 将指定分支合并到当前分支
git branch -d <分支名>  # 删除分支
```

## 8. 查看历史

```bash
git log                 # 查看提交历史
git log --oneline       # 简洁显示，一行一条
git log --graph --all   # 图形化显示所有分支历史
```

## 9. 忽略文件

在项目根目录创建 `.gitignore` 文件，写入需要忽略的文件或目录：

```
node_modules/
*.log
.env
```

这些文件不会被 `git add .` 添加，也不会被 Git 跟踪。

### 1. 为什么要忽略这些文件？

| 文件/目录           | 原因                                                         |
| ------------------- | ------------------------------------------------------------ |
| `.env`、`.flaskenv` | 通常包含敏感配置（数据库密码、API 密钥等），泄露会造成安全风险。 |
| `.idea/`            | PyCharm 的项目配置，与个人开发环境相关，不应共享。           |
| `__pycache__/`      | Python 编译缓存，无版本价值，且会频繁变动。                  |
| `venv312/`          | 虚拟环境目录，体积大且依赖可通过 `requirements.txt` 重建。   |

### 2. 如何创建 `.gitignore`

在项目根目录（`D:\QA`）新建一个名为 `.gitignore` 的文件（注意没有扩展名），然后根据你的项目添加规则。以下是一个常见 Python 项目的 `.gitignore` 示例：

gitignore

```
# Python 缓存
__pycache__/
*.py[cod]
*$py.class

# 虚拟环境
venv/
venv312/
.venv/

# 环境变量文件
.env
.flaskenv

# IDE 配置
.idea/
.vscode/

# 其他常见忽略
*.log
.DS_Store
```

你可以直接复制上面的内容到 `.gitignore` 文件里，然后保存。

### 3. 创建后如何提交

1. **先创建 .gitignore 文件**（如上）。

2. **执行 git add .**：此时 Git 会自动忽略 `.gitignore` 中指定的文件和目录，不会将它们加入暂存区。

3. **确认忽略生效**：运行 `git status`，你会看到那些被忽略的文件不再出现在 “Untracked files” 列表中。

4. **正常提交和推送**：

   bash

   ```
   git commit -m "Initial commit"
   git push -u origin master
   ```

   ​

   ​

### 4. 注意事项

#### 4.1 如果已经提交过敏感文件（本次不需要，但以后可能遇到）

如果 `.env` 等文件已经提交过，仅仅加入 `.gitignore` 不会让 Git 停止跟踪它们。你需要执行：

bash

```
git rm --cached .env    # 从 Git 索引中移除，但保留本地文件
```

然后提交这个删除操作，并在 `.gitignore` 中添加 `.env`。如果敏感信息已经推送到远程，还需要考虑修改密钥或清理历史。

#### 4.2 检查其他可能被忽略的文件

- `*.pyc` 文件、`build/`、`dist/` 等构建产物。
- 你的项目可能还有 `requirements.txt` 或 `pipfile`，这些**应该提交**，而不是忽略。
- 如果有 `.env.example` 或 `.flaskenv.example` 文件，可以作为模板提交，但不要提交真实的 `.env`。

## 10. 常见问题

### 提交失败：`Aborting commit due to empty commit message.`

原因：使用 `git commit` 时没有提供 `-m "信息"`，且未输入提交信息。

解决：始终使用 `git commit -m "说明"`。

### 推送失败：`Everything up-to-date`

表示本地没有新的提交需要推送，远程已和本地同步。检查是否成功执行了 `git commit`。

### 推送失败：网络错误（如 `Failed to connect to github.com port 443`）

网络环境不稳定或无法访问 GitHub。可尝试：

- 检查代理设置；
- 切换 HTTPS 为 SSH 方式；
- 网络好转后重试。

### 如何撤销未提交的修改？

```bash
git checkout -- <文件名>   # 丢弃工作区中指定文件的修改
git reset HEAD <文件名>    # 将文件从暂存区移出，但保留工作区修改
```
