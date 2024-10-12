# DSCI 521

### Bash 基础

**1. 文件系统导航**

```bash
pwd  # 打印当前工作目录
ls   # 列出当前目录内容
ls -F  # 列出内容并显示类型指示符
ls -a  # 列出所有文件，包括隐藏文件
cd <directory>  # 改变目录
cd ..  # 移动到上一级目录
cd ~   # 移动到主目录
```

**2. 文件和目录操作**

```bash
mkdir <directory>  # 创建新目录
touch <filename>   # 创建新文件
mv <source> <destination>  # 移动或重命名文件/目录
cp <source> <destination>  # 复制文件/目录
rm <file>          # 删除文件
rm -r <directory>  # 删除目录及其内容
```

**3. 查看文件内容**

```bash
head <file>     # 查看文件前几行
tail <file>     # 查看文件最后几行
cat <file>      # 显示整个文件内容
less <file>     # 分页查看文件内容
```

**4. 命令历史和帮助**

```bash
history         # 查看命令历史
man <command>   # 显示命令的手册页
<command> --help  # 显示命令的帮助信息
```

### Git 和 GitHub

**1. 设置 Git**

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

git config --list # 查看配置
cat .git/config  # 查看当前仓库配置
cat ~/.gitconfig  # 查看全局配置

# 设置.gitignore文件
vim .gitignore
```

**2. 基本 Git 工作流**

```bash
git init            # 初始化新的 Git 仓库
git clone <url>     # 克隆远程仓库
git status          # 检查工作目录状态
git add <file>      # 暂存更改以准备提交
git commit -m "Message"  # 提交暂存的更改
git push            # 推送提交到远程仓库
git pull            # 从远程获取并合并更改
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
git log --oneline # 查看提交历史
git log --oneline --patch # 查看简洁的提交历史
git diff # 显示提交之间、提交和工作树之间等的更改
```

**5. 撤销更改**

```bash
git reset <commit>   # 将当前 HEAD 重置到指定提交
git revert <commit>  # 创建新提交以撤销指定提交的更改
git stash            # 临时存储修改过的、已跟踪的文件
```

**6. 生成 SSH 密钥**

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

### Quarto

**1. 创建 Quarto 项目**

```bash
quarto create project website  # 创建新的 Quarto 网站项目
```

**2. 渲染 Quarto 文档**

```bash
quarto preview            # 预览 Quarto 项目并实时更新
quarto render             # 渲染 Quarto 项目
quarto publish
```

**3. Quarto YAML 配置**

```yaml
project:
  type: website
output-dir: docs  # 渲染文件的输出目录
```

**4. 其他功能**

```bash
quarto render filename.ipynb --to pdf
quarto render filename.rmd --to md
```



### Key Concepts

**1. Command Line Interface (CLI) 命令行界面**

- Text-based interface for computer interaction
  基于文本的计算机交互界面
- Operations performed by typing commands
  通过输入命令执行操作
- More flexible and powerful than Graphical User Interfaces (GUIs)
  比图形用户界面(GUI)更灵活和强大

**2. Version Control 版本控制**

- System for managing changes to files and projects over time
  管理文件和项目随时间变化的系统
- Enables collaboration and tracking of modification history
  允许协作和跟踪修改历史
- Git is a popular distributed version control system
  Git是一个流行的分布式版本控制系统

**3. Git Repository Git仓库**

- Directory containing project files and complete history
  包含项目文件和完整历史记录的目录
- Can be local or hosted on remote servers (e.g., GitHub)
  可以是本地的，也可以托管在远程服务器上（如GitHub）

**4. Working Directory, Staging Area, and Repository 工作目录、暂存区和仓库**

- Working Directory: Files currently being edited
  工作目录：当前正在编辑的文件
- Staging Area: Changes prepared for commit
  暂存区：准备提交的更改
- Repository: All committed versions of the project
  仓库：项目的所有已提交版本

**5. Branches 分支**

- Independent lines of development in Git
  Git中的独立开发线
- Allow multiple feature development without affecting main code
  允许同时进行多个特性开发而不影响主代码

**6. Merging 合并**

- Integrating changes from one branch into another
  将一个分支的更改整合到另一个分支
- May result in conflicts requiring manual resolution
  可能导致冲突，需要手动解决

**7. SSH Keys SSH密钥**

- Cryptographic key pair for secure remote access
  用于安全远程访问的加密密钥对
- Public key shared with servers, private key kept secret
  公钥分享给服务器，私钥保密

**8. Quarto**

- Open-source scientific and technical publishing system
  开源科技写作和发布系统
- Supports multiple programming languages and output formats
  支持多种编程语言和输出格式

**9. GitHub Pages**

- Static site hosting service provided by GitHub
  GitHub提供的静态网站托管服务
- Generates websites directly from GitHub repositories
  直接从GitHub仓库生成网站
