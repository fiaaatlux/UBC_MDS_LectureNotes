# Lecture 2 - Git

**1. Git 基础命令**

```bash
# 初始化 Git 仓库
git init  # 在本地创建一个新的 Git 仓库

# 检查仓库状态
git status  # 查看当前工作目录的状态

# 查看提交历史
git log  # 显示项目的提交历史
```

`git init` 用于初始化本地仓库，适合新项目开始时使用。
`git status` 显示工作目录状态，包括未跟踪文件和未提交的更改。
`git log` 展示提交历史，帮助跟踪项目变动。

#### **2. 提交与版本管理**

```
# 添加文件到暂存区
git add <file_name>  # 添加指定文件
git add .  # 添加所有更改的文件

# 提交更改
git commit -m "提交信息"  # 提交暂存区的更改并附带说明

# 推送到远程仓库
git push origin main  # 推送到远程仓库的 main 分支
```

`git add` 将文件添加到暂存区，`git commit` 将更改提交到本地仓库，`git push` 用于将更改推送到远程仓库。

#### **3. 分支管理**

```
# 创建新分支
git branch <branch_name>  # 创建新分支

# 切换到指定分支
git checkout <branch_name>  # 切换到指定分支

# 合并分支
git merge <branch_name>  # 将指定分支合并到当前分支
```

`git branch` 创建新分支，`git checkout` 用于切换分支，`git merge` 合并分支。

#### **4. 克隆与拉取**

```
# 克隆远程仓库
git clone <repository_url>  # 从远程仓库克隆项目

# 拉取远程更新
git pull origin main  # 从远程 main 分支拉取最新的更改
```

`git clone` 克隆远程仓库到本地，`git pull` 同步远程更新。

#### **5. 合并与解决冲突**

```
# 合并分支
git merge <branch_name>  # 合并指定分支到当前分支

# 解决合并冲突
git status  # 查看冲突文件
git add <conflict_file>  # 添加解决冲突后的文件
git commit -m "解决冲突"  # 提交解决冲突后的更改
```

`git merge` 合并分支，冲突时需要手动解决并提交。

#### **6. 远程仓库管理**

```
# 添加远程仓库
git remote add origin <repository_url>  # 添加远程仓库

# 查看远程仓库
git remote -v  # 查看远程仓库的详细信息
```

`git remote add` 添加远程仓库，`git remote -v` 查看远程仓库地址。
