# Lecture 2 - Git

**1. Git 基础配置和初始化**

```bash
# 配置用户信息
git config --global user.name "Your Name"
git config --global user.email youremail@example.com

# 查看配置
git config --list
cat .git/config  # 查看当前仓库配置
cat ~/.gitconfig  # 查看全局配置

# 设置.gitignore文件
vim .gitignore
# 在文件中添加需要忽略的文件或目录

# 初始化仓库
git init

# 克隆远程仓库
git clone <repository_url>
```

在项目开始时就创建`.gitignore`文件，可以防止将不必要的文件添加到版本控制中。对于常见的项目类型，可以使用网站如gitignore.io生成合适的.gitignore文件。

**2. 文件操作和提交**

```bash
# 检查仓库状态
git status

# 查看文件变化
git diff

# 添加文件到暂存区
git add <file_name>  # 添加指定文件
git add .  # 添加所有更改的文件

# 提交更改
git commit -m "提交信息"

# 推送到远程仓库
git push origin main

# 从远程仓库拉取更新
git pull origin main
```

使用`git add -p`可以交互式地选择要暂存的代码块，这对于创建更精确的提交非常有用。提交信息遵循"动词 + 简要描述"的格式（如"Fix login bug"）可以使提交历史更清晰。

**3. 查看历史和版本回退**

```bash
# 查看提交历史
git log
git log --pretty=oneline  # 简化输出

# 查看命令历史
git reflog

# 回退到之前版本
git reset --hard HEAD^  # 回退到上一个版本
git reset --hard HEAD~2  # 回退到前两个版本
git reset --hard <commit_id>  # 回退到指定版本

# 撤销暂存区的修改
git reset HEAD <file>

# 撤销工作区的修改
git checkout -- <file>
```

使用`git log --graph --oneline --all`可以以图形方式显示分支历史。如果误删了某个提交，可以通过`git reflog`找到该提交的ID，然后使用`git reset --hard`恢复。

**4. 分支管理**

```bash
# 创建分支
git branch <branch_name>

# 切换分支
git checkout <branch_name>

# 创建并切换分支
git checkout -b <branch_name>

# 合并分支
git merge <branch_name>

# 删除分支
git branch -d <branch_name>
```

使用描述性的分支名称（如feature/login-page或bugfix/header-alignment）可以更好地组织你的工作。在合并前，可以使用`git merge --no-ff`保留分支历史，这对于了解功能开发过程很有帮助。

**5. 远程仓库管理**

```bash
# 添加远程仓库
git remote add origin <repository_url>

# 查看远程仓库
git remote -v

# 从远程获取最新代码
git fetch origin

# 推送到远程仓库
git push -u origin main  # 首次推送使用-u
git push  # 后续推送
git push --force # 或者是-f 强行合并到remote repository
```

使用`git fetch`而不是`git pull`可以让你在合并前先查看更改。这在处理复杂项目时特别有用。`-u`参数设置上游分支，之后可以直接使用`git push`和`git pull`而不需要指定分支名。

**6. 解决冲突**

当合并分支出现冲突时：

1. 使用 `git status` 查看冲突文件
2. 手动编辑冲突文件，解决冲突
3. 使用 `git add <conflict_file>` 标记冲突已解决
4. 使用 `git commit -m "解决冲突"` 提交更改

在解决复杂冲突时，使用`git mergetool`可以调用可视化工具帮助解决冲突。设置`git config --global merge.tool vimdiff`可以使用vim作为默认的合并工具。
