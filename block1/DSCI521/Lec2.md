# Git 和 GitHub

**1. 设置 Git**

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

git config --list         # 查看配置
cat .git/config           # 查看当前仓库配置
cat ~/.gitconfig          # 查看全局配置

# 设置.gitignore文件
vim ~/.config/git/ignore  # 全局配置
vim .gitignore            # 当前仓库配置
```

**2. 基本 Git 工作流**

```bash
git init                          # 初始化新的 Git 仓库
git remote add origin <仓库地址>   # 关联远程仓库
# 如果远程分支上有本地没有的内容需要先运行这个
git pull origin main --allow-unrelated-histories --no-rebase 
git remote -v                     # 查看是否关联成功# 推送到远程仓库
git push -u origin main           # 首次推送使用-u
git push                          # 后续推送
git push --force                  # 或者是-f 强行合并到remote repository

git clone <仓库地址>               # 克隆远程仓库
git status                        # 检查工作目录状态
git add <filename>                # 暂存更改以准备提交
git commit -m "Message"           # 提交暂存的更改
git push                          # 推送提交到远程仓库

git fetch origin                  # 从远程获取最新代码
git pull                          # 从远程获取并合并更改
```

**3. 分支和合并**

```bash
git branch                  # 列出分支
git branch <branch-name>    # 创建新分支
git checkout <branch-name>  # 切换到指定分支
git merge <branch-name>     # 将指定分支合并到当前分支
```

**4. 查看历史**

```bash
git diff                        # 显示提交之间、提交和工作树之间等的更改
git reflog                      # 查看命令历史找寻commit id

git log --oneline               # 查看提交历史
git log --oneline --patch       # 查看简洁的提交历史
git log --graph --oneline --all # 可以以图形方式显示分支历史
```

**5. 撤销更改**

```bash
git stash                   # 临时存储修改过的、已跟踪的文件

git checkout -- <filename>  # 撤销工作区的修改
git reset HEAD <filename>   # 撤销已提交到暂存区的内容 放回到工作区

# 回退到之前版本
git reset --hard HEAD^  # 回退到上一个版本
git reset --hard HEAD~2  # 回退到前两个版本
git reset --hard <commit_id>  # 回退到指定版本

git revert <commit-id>      # 创建新提交以撤销指定提交的更改
```

**6. 生成 SSH 密钥**

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
