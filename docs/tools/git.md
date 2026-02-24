# Git 教程

## 一、Git 简介

Git 是一个分布式版本控制系统，由 Linus Torvalds 创建，用于高效地管理项目版本。与集中式版本控制不同，每个开发者都拥有完整的代码仓库历史。

### 核心概念
- **仓库（Repository）**：存储项目文件和完整历史的地方
- **提交（Commit）**：项目的一个快照
- **分支（Branch）**：独立的开发线
- **HEAD**：指向当前分支最新提交的指针
- **远程（Remote）**：托管在其他地方的仓库副本
- **暂存区（Staging Area）**：准备提交的文件列表

## 二、安装与配置

### 安装 Git

#### Windows
1. 下载 [Git for Windows](https://git-scm.com/download/win)
2. 运行安装程序，使用默认选项
3. 安装完成后，使用 Git Bash 或命令提示符

#### macOS
```bash
# 使用 Homebrew
brew install git

# 或下载安装包
# https://git-scm.com/download/mac
```

#### Linux (Ubuntu/Debian)
```bash
sudo apt update
sudo apt install git
```

### 初始配置
```bash
# 设置用户名和邮箱（提交时会用到）
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# 设置默认编辑器
git config --global core.editor "vim"

# 查看配置
git config --list

# 设置别名（可选）
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.lg "log --oneline --graph --all"

# 启用颜色显示
git config --global color.ui auto
```

## 三、基础操作

### 创建仓库
```bash
# 在当前目录初始化新仓库
git init

# 克隆远程仓库
git clone https://github.com/username/repo.git
git clone git@github.com:username/repo.git  # SSH 方式

# 克隆到指定目录
git clone https://github.com/username/repo.git myfolder
```

### 基本工作流
```bash
# 查看仓库状态
git status

# 添加文件到暂存区
git add filename.txt        # 添加单个文件
git add .                   # 添加所有文件
git add *.js                # 添加所有 JS 文件

# 提交更改
git commit -m "提交说明"

# 跳过暂存区直接提交（仅对已跟踪文件）
git commit -a -m "提交说明"

# 查看提交历史
git log
git log --oneline           # 简洁模式
git log --graph             # 图形化显示分支
git log -p                  # 显示详细更改
```

### 比较差异
```bash
# 查看工作区与暂存区差异
git diff

# 查看暂存区与最新提交的差异
git diff --staged
git diff --cached

# 查看两个提交之间的差异
git diff commit1 commit2

# 查看当前文件与特定提交的差异
git diff commit -- filename
```

## 四、分支管理

### 分支操作
```bash
# 列出分支（* 表示当前分支）
git branch
git branch -r               # 远程分支
git branch -a               # 所有分支

# 创建分支
git branch feature-login

# 切换分支
git checkout feature-login
git switch feature-login    # 新版本 Git

# 创建并切换分支
git checkout -b feature-login
git switch -c feature-login  # 新版本 Git

# 合并分支（先切换到目标分支）
git checkout main
git merge feature-login

# 删除分支
git branch -d feature-login  # 删除已合并分支
git branch -D feature-login  # 强制删除未合并分支

# 重命名分支
git branch -m old-name new-name
```

### 分支合并策略
```bash
# 普通合并（创建合并提交）
git merge feature

# 快进合并（不创建合并提交）
git merge --ff-only feature

# 压缩合并（将所有提交压缩成一个）
git merge --squash feature

# 变基合并（保持线性历史）
git rebase feature          # 在 feature 分支上执行
git checkout main && git merge feature
```

## 五、远程仓库

### 远程操作
```bash
# 查看远程仓库
git remote -v

# 添加远程仓库
git remote add origin https://github.com/username/repo.git

# 修改远程仓库地址
git remote set-url origin https://github.com/username/new-repo.git

# 删除远程仓库
git remote remove origin

# 推送到远程
git push origin main
git push -u origin main     # 设置上游分支（首次推送）
git push --all              # 推送所有分支

# 从远程拉取
git pull origin main        # 拉取并合并
git fetch origin            # 只拉取不合并

# 查看远程分支
git branch -r

# 删除远程分支
git push origin --delete feature-login
```

### 处理冲突
```bash
# 拉取代码时可能遇到冲突
git pull origin main

# 手动解决冲突后
git add <冲突文件>
git commit -m "解决冲突"

# 放弃合并（回到合并前状态）
git merge --abort

# 使用工具解决冲突
git mergetool
```

## 六、撤销与回退

### 撤销操作
```bash
# 撤销工作区的修改（未暂存）
git checkout -- filename
git restore filename        # 新版本 Git

# 撤销暂存区的文件
git reset HEAD filename
git restore --staged filename  # 新版本 Git

# 修改最近一次提交
git commit --amend -m "新的提交说明"

# 添加漏掉的文件到上次提交
git add forgotten-file
git commit --amend --no-edit

# 撤销提交（保留更改）
git reset --soft HEAD~1      # 撤销提交，保留暂存区

# 撤销提交（不保留更改）
git reset --hard HEAD~1      # 完全撤销提交和更改

# 恢复到特定提交
git reset --hard commit_hash

# 撤销某次提交（创建新的反向提交）
git revert commit_hash
```

### 恢复删除的分支或提交
```bash
# 查看所有操作历史
git reflog

# 恢复删除的分支
git checkout -b recovered-branch commit_hash

# 找回丢失的提交
git cherry-pick commit_hash
```

## 七、标签管理

```bash
# 创建标签
git tag v1.0.0              # 轻量标签
git tag -a v1.0.0 -m "版本1.0发布"  # 附注标签

# 为历史提交打标签
git tag -a v1.0.0 commit_hash -m "版本说明"

# 查看标签
git tag
git show v1.0.0

# 推送标签到远程
git push origin v1.0.0
git push origin --tags      # 推送所有标签

# 删除标签
git tag -d v1.0.0           # 删除本地
git push origin --delete v1.0.0  # 删除远程
```

## 八、暂存与隐藏

### Stash 操作
```bash
# 暂存当前工作
git stash
git stash save "正在开发登录功能"

# 查看暂存列表
git stash list

# 应用暂存（不删除）
git stash apply
git stash apply stash@{2}   # 应用指定暂存

# 应用并删除暂存
git stash pop

# 删除暂存
git stash drop stash@{0}
git stash clear             # 清空所有暂存

# 查看暂存差异
git stash show -p stash@{0}
```

## 九、高级技巧

### 交互式变基
```bash
# 修改最近3个提交
git rebase -i HEAD~3

# 交互式变基选项：
# p, pick = 使用该提交
# r, reword = 使用该提交但修改说明
# e, edit = 使用该提交但停下来修改
# s, squash = 合并到前一个提交
# f, fixup = 类似 squash，但丢弃提交说明
# d, drop = 删除提交
```

### Cherry-pick
```bash
# 选择性地合并提交
git cherry-pick commit_hash

# 连续 cherry-pick
git cherry-pick A..B        # 从 A 到 B 的所有提交（不包括 A）

# 解决冲突后继续
git cherry-pick --continue
git cherry-pick --abort
```

### Bisect 二分查找
```bash
# 开始二分查找
git bisect start

# 标记当前为坏版本
git bisect bad

# 标记某个历史为好版本
git bisect good commit_hash

# Git 会自动检出中间版本供测试
# 测试后标记：
git bisect good  # 如果当前是好版本
git bisect bad   # 如果当前是坏版本

# 找到问题后结束
git bisect reset
```

### 子模块
```bash
# 添加子模块
git submodule add https://github.com/username/library.git libs/library

# 克隆包含子模块的项目
git clone --recursive https://github.com/username/project.git

# 更新子模块
git submodule update --init --recursive

# 子模块的更多操作
git submodule foreach git pull origin main
```

## 十、Git 工作流

### 常用工作流模式

#### 1. 集中式工作流
```bash
# 适合小团队，所有人都在 main 分支开发
git pull origin main
# 修改代码
git add .
git commit -m "功能完成"
git push origin main
```

#### 2. 功能分支工作流
```bash
# 创建功能分支
git checkout -b feature/user-auth

# 开发功能，多次提交
git commit -m "添加用户模型"
git commit -m "实现登录接口"

# 合并回主分支
git checkout main
git pull origin main
git merge feature/user-auth
git push origin main

# 删除功能分支
git branch -d feature/user-auth
```

#### 3. Git Flow 工作流
```bash
# 主要分支：main, develop
# 辅助分支：feature, release, hotfix

# 创建 develop 分支（从 main）
git checkout -b develop main

# 创建功能分支
git checkout -b feature/new-feature develop

# 完成功能后合并到 develop
git checkout develop
git merge --no-ff feature/new-feature
git branch -d feature/new-feature

# 创建发布分支
git checkout -b release/1.0.0 develop
# 修复 bug 后
git checkout main
git merge --no-ff release/1.0.0
git tag -a 1.0.0 -m "版本 1.0.0"
git checkout develop
git merge --no-ff release/1.0.0
git branch -d release/1.0.0
```

## 十一、.gitignore 文件

```gitignore
# 忽略特定文件
secret.txt
config.json

# 忽略文件夹
node_modules/
dist/
build/

# 忽略特定扩展名
*.log
*.tmp
*.swp

# 忽略但排除特定文件
!important.log

# 系统文件
.DS_Store
Thumbs.db

# IDE 文件
.vscode/
.idea/
*.sublime-*

# 环境文件
.env
.env.local

# 编译文件
*.pyc
__pycache__/
*.class
```

## 十二、常用命令速查表

| 命令                    | 说明         |
| ----------------------- | ------------ |
| `git init`              | 初始化仓库   |
| `git clone <url>`       | 克隆仓库     |
| `git status`            | 查看状态     |
| `git add <file>`        | 添加文件     |
| `git commit -m "msg"`   | 提交         |
| `git push`              | 推送         |
| `git pull`              | 拉取         |
| `git fetch`             | 获取远程更新 |
| `git branch`            | 分支管理     |
| `git checkout <branch>` | 切换分支     |
| `git merge <branch>`    | 合并分支     |
| `git rebase <branch>`   | 变基         |
| `git log`               | 查看历史     |
| `git diff`              | 查看差异     |
| `git reset`             | 重置         |
| `git revert`            | 撤销提交     |
| `git stash`             | 暂存         |
| `git tag`               | 标签管理     |
| `git remote -v`         | 查看远程     |

## 十三、常见问题解决

### 1. 误操作恢复
```bash
# 找回误删的文件
git checkout HEAD -- filename

# 找回误删的提交
git reflog
git cherry-pick lost_commit_hash

# 撤销已推送的提交
git revert HEAD
git push origin main
```

### 2. 合并冲突处理
```bash
# 查看冲突文件
git status

# 手动解决后
git add resolved-file
git commit

# 使用外部工具
git mergetool
```

### 3. 提交信息写错
```bash
# 修改最近提交
git commit --amend -m "正确的提交说明"

# 修改更早的提交
git rebase -i HEAD~3
# 将需要修改的提交前的 pick 改为 reword
```

### 4. 忽略已跟踪的文件
```bash
# 停止跟踪文件（保留在工作区）
git rm --cached filename

# 添加到 .gitignore 后提交
echo "filename" >> .gitignore
git add .gitignore
git commit -m "停止跟踪 filename"
```

## 十四、Git GUI 工具

- **GitKraken** - 功能强大的跨平台 GUI
- **Sourcetree** - 免费的 Git 图形客户端
- **GitHub Desktop** - GitHub 官方客户端
- **VS Code** - 内置 Git 支持
- **TortoiseGit** - Windows 资源管理器集成

## 十五、学习资源

- [官方文档](https://git-scm.com/doc)
- [Pro Git 中文版](https://git-scm.com/book/zh/v2)
- [Git 飞行规则](https://github.com/k88hudson/git-flight-rules)
- [Learn Git Branching](https://learngitbranching.js.org/)（交互式学习）

