# 📚 Hexo 博客完全操作手册

> 基于 Maxkore 亲身经历的完整总结
> 涵盖日常操作、Git 工作流、各类报错解决方案
> **最后更新：2026年2月24日**

---

## 📖 目录

- [一、博客日常操作](#一博客日常操作)
- [二、文章管理](#二文章管理)
- [三、自定义域名配置](#三自定义域名配置)
- [四、Git 工作流](#四git-工作流)
- [五、常见错误解决](#五常见错误解决)
- [六、配置文件详解](#六配置文件详解)
- [七、常用命令速查](#七常用命令速查)
- [八、经验总结](#八经验总结)

---

## 一、博客日常操作

### 1.1 进入博客目录

```bash
# 博客本地路径
cd /e/MyBlog

# 确认当前目录
pwd
# 应显示：/e/MyBlog
```

### 1.2 写新文章

```bash
# 创建新文章（标题可以用中文）
hexo new "文章标题"

# 编辑文章（用 Typora）
"D:/Typora/Typora.exe" source/_posts/文章标题.md

# 或用记事本
notepad source/_posts/文章标题.md
```

### 1.3 文章头部格式

每篇文章开头都需要有 YAML 格式的 Front-matter：

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
updated: 2026-02-24 15:30:00
tags: 
  - 标签1
  - 标签2
categories:
  - 分类1
  - 分类2
keywords: [关键词1, 关键词2]
description: 文章描述
comments: true
toc: true
---
```

### 1.4 本地预览

```bash
# 启动本地服务器
hexo server

# 或指定端口（如果4000被占用）
hexo s -p 4001

# 生成并预览
hexo generate && hexo server
```

访问 `http://localhost:4000` 查看效果
按 `Ctrl + C` 停止预览

### 1.5 部署上线

```bash
# 标准三步曲
hexo clean      # 清理缓存
hexo generate   # 生成静态文件
hexo deploy     # 部署到 GitHub

# 一键完成（最常用）
hexo clean && hexo g -d
```

### 1.6 修改文章

```bash
# 直接编辑源文件
"D:/Typora/Typora.exe" "source/_posts/文章标题.md"

# 重新部署
hexo clean && hexo g -d
```

### 1.7 删除文章

```bash
# 删除源文件
rm "source/_posts/要删除的文章.md"

# 清理并重新部署
hexo clean && hexo g -d
```

---

## 二、文章管理

### 2.1 查看所有文章

```bash
# 列出所有文章
ls -la source/_posts/

# 按时间排序
ls -lt source/_posts/

# 统计文章数量
ls source/_posts/ | wc -l
```

### 2.2 搜索文章

```bash
# 按标题搜索
find source/_posts -name "*关键词*"

# 按内容搜索
grep -r "关键词" source/_posts/

# 按日期搜索
find source/_posts -newermt "2026-02-01"
```

### 2.3 批量修改

```bash
# 批量替换文本（将所有文章中的"旧词"替换为"新词"）
sed -i 's/旧词/新词/g' source/_posts/*.md

# 用 VS Code 批量编辑
code source/_posts/
```

### 2.4 草稿管理

```bash
# 创建草稿
hexo new draft "草稿标题"

# 查看所有草稿
ls source/_drafts/

# 发布草稿
hexo publish "草稿标题"

# 编辑草稿
"D:/Typora/Typora.exe" source/_drafts/草稿标题.md
```

### 2.5 页面管理

```bash
# 创建独立页面
hexo new page about
hexo new page tags
hexo new page categories

# 编辑页面
"D:/Typora/Typora.exe" source/about/index.md
```

---

## 三、自定义域名配置

### 3.1 首次配置

1. 进入 GitHub 仓库：**Settings → Pages**
2. 在 **Custom domain** 输入：`maxkore.bbroot.com`
3. 点击 **Save**
4. 等待几分钟后勾选 **Enforce HTTPS**

### 3.2 创建 CNAME 文件（防止域名被清空）

```bash
# 进入博客目录
cd /e/MyBlog

# 创建 CNAME 文件（-n 参数避免多余换行）
echo -n "maxkore.bbroot.com" > source/CNAME

# 验证文件内容
cat source/CNAME
# 应该只显示：maxkore.bbroot.com
```

### 3.3 提交 CNAME 到 Git

```bash
git add source/CNAME
git commit -m "Add CNAME for custom domain"
git push origin master
```

### 3.4 检查域名状态

```bash
# 测试域名解析
nslookup maxkore.bbroot.com

# 应该返回 GitHub Pages 的 IP：
# 185.199.108.153
# 185.199.109.153
# 185.199.110.153
# 185.199.111.153
```

---

## 四、Git 工作流

### 4.1 日常同步

```bash
# 查看当前状态
git status

# 添加所有更改
git add .

# 提交更改
git commit -m "更新说明"

# 推送到 GitHub
git push origin master

# 拉取远程更新
git pull origin master
```

### 4.2 完整推送流程

```bash
git add .
git commit -m "更新博客"
git pull origin master
git push origin master
```

### 4.3 分支管理

```bash
# 查看当前分支
git branch

# 创建新分支
git branch feature/new-post

# 切换分支
git checkout feature/new-post

# 合并分支
git checkout master
git merge feature/new-post
```

### 4.4 查看提交历史

```bash
# 查看提交日志
git log --oneline -10

# 查看某个文件的修改历史
git log -p source/_posts/文章标题.md

# 查看某次提交的详细信息
git show commit_id
```

### 4.5 撤销操作

```bash
# 撤销工作区的修改
git checkout -- filename

# 撤销暂存区的文件
git reset HEAD filename

# 撤销最后一次提交（保留修改）
git reset --soft HEAD~1

# 撤销最后一次提交（不保留修改）
git reset --hard HEAD~1
```

---

## 五、常见错误解决

### 5.1 YAML 解析错误

**错误信息**：
```
YAMLException: can not read a block mapping entry
```

**原因**：文章开头的配置格式错误

**解决方法**：
- 检查 `:` 后面是否有空格
- 确保缩进一致（用2个空格）
- 检查是否有特殊字符

✅ 正确格式：
```yaml
title: 文章标题  # 冒号后有空格
tags: 
  - 标签1      # 缩进一致
  - 标签2
```

❌ 错误格式：
```yaml
title:文章标题   # 冒号后没空格
tags:
- 标签1        # 缩进错误
  - 标签2      # 缩进不一致
```

### 5.2 部署失败 - 网络问题

**错误信息**：
```
fatal: unable to access '...': Recv failure: Connection was reset
```

**解决方法**：
```bash
# 方法1：稍后重试
hexo clean && hexo g -d

# 方法2：手动 Git 推送
git add .
git commit -m "更新"
git push origin master

# 方法3：切换网络（WiFi换热点）
```

### 5.3 Git 推送被拒绝

**错误信息**：
```
! [rejected] master -> master (fetch first)
```

**原因**：远程有本地没有的更新

**解决方法**：
```bash
git pull origin master
git push origin master
```

### 5.4 合并冲突

**错误信息**：
```
Automatic merge failed; fix conflicts and then commit the result.
```

**现象**：处于 `(master|MERGING)` 状态

**解决方法**：
```bash
# 1. 查看冲突文件
git status

# 2. 打开冲突文件解决
notepad CNAME  # 或其他冲突文件

# 3. 解决后添加文件
git add .

# 4. 完成合并
git commit -m "解决合并冲突"

# 5. 推送
git push origin master
```

### 5.5 子模块错误

**错误信息**：
```
fatal: No url found for submodule path '.deploy_git' in .gitmodules
```

**解决方法**：
```bash
# 彻底清理
rm -rf .gitmodules
git rm --cached .deploy_git
git add .
git commit -m "移除子模块配置"
git push
```

### 5.6 SSH 密钥问题

**错误信息**：
```
git@github.com: Permission denied (publickey)
```

**解决方法**：
```bash
# 1. 生成新密钥
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
# 一直按回车（不设密码）

# 2. 查看公钥
cat ~/.ssh/id_rsa.pub

# 3. 复制公钥添加到 GitHub
# 访问：https://github.com/settings/keys
# 点击 New SSH key，粘贴保存
```

### 5.7 Token 认证问题

**错误信息**：
```
remote: Invalid username or token.
```

**解决方法**：
```bash
# 1. 在 GitHub 生成新 Token
# Settings → Developer settings → Personal access tokens → Tokens (classic)

# 2. 配置 Git 使用 Token
git remote set-url origin https://用户名:token@github.com/用户名/仓库名.git

# 3. 推送
git push
```

### 5.8 本地预览端口被占用

**错误信息**：
```
Error: listen EADDRINUSE
```

**解决方法**：
```bash
# 换端口启动
hexo s -p 4001

# 或者杀掉占用端口的进程
netstat -ano | findstr :4000
taskkill /PID 进程号 /F
```

### 5.9 文章不显示

**现象**：部署成功但文章没出现

**可能原因**：
- 文章日期是未来时间
- 文章头部格式错误
- 文件名有问题

**解决方法**：
```bash
# 1. 检查文章日期
cat source/_posts/文章标题.md | grep "date"

# 2. 检查文章头部
head -20 source/_posts/文章标题.md

# 3. 清理缓存重新生成
hexo clean
hexo generate
hexo server
```

### 5.10 404 错误

**现象**：访问文章显示 404

**可能原因**：
- 文件名大小写问题
- 文件不在正确位置
- GitHub Pages 未更新

**解决方法**：
```bash
# 1. 检查文件是否存在
ls -la public/文章路径/

# 2. 等待 2-5 分钟
# 3. 按 Ctrl+F5 强制刷新
# 4. 检查 GitHub Pages 设置
```

---

## 六、配置文件详解

### 6.1 主配置文件 `_config.yml`

```yaml
# 网站信息
title: Maxkore的博客
subtitle: 代码之外，思考之上。
description: 科技博客 / 程序博客
author: Maxkore
language: zh-CN
timezone: Asia/Shanghai

# URL 设置
url: https://maxkore.bbroot.com
root: /
permalink: :year/:month/:day/:title/
permalink_defaults:

# 目录设置
source_dir: source
public_dir: public
tag_dir: tags
archive_dir: archives
category_dir: categories
code_dir: downloads/code
i18n_dir: :lang
skip_render:

# 写作设置
new_post_name: :title.md
default_layout: post
titlecase: false
external_link:
  enable: true
  field: site
  exclude: ''
filename_case: 0
render_drafts: false
post_asset_folder: false
relative_link: false
future: true
highlight:
  enable: true
  line_number: true
  auto_detect: false
  tab_replace: ''
  wrap: true
  hljs: false

# 主题设置
theme: next

# 部署配置
deploy:
  type: git
  repo: git@github.com:Maxkore-Geek/Maxkore-Geek.github.io.git
  branch: master
```

### 6.2 NexT 主题配置 `themes/next/_config.yml`

```yaml
# 菜单
menu:
  home: / || fa fa-home
  archives: /archives/ || fa fa-archive
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  about: /about/ || fa fa-user

# 头像
avatar:
  url: /images/avatar.gif
  rounded: true
  rotated: false

# 社交链接
social:
  GitHub: https://github.com/Maxkore-Geek || fab fa-github
  Twitter: https://twitter.com/username || fab fa-twitter
  Weibo: https://weibo.com/username || fab fa-weibo

# 友情链接
links:
  Docs: https://docs.bbroot.com
  Wiki: https://maxkore-wiki.bbroot.com

# 版权信息
creative_commons:
  license: by-nc-sa
  sidebar: true
  post: true
  language:
```

---

## 七、常用命令速查

| 命令                            | 作用         | 场景        |
| ------------------------------- | ------------ | ----------- |
| `hexo new "标题"`               | 新建文章     | 写作        |
| `hexo new draft "标题"`         | 新建草稿     | 写作        |
| `hexo publish "标题"`           | 发布草稿     | 发布        |
| `hexo server`                   | 本地预览     | 检查效果    |
| `hexo clean`                    | 清理缓存     | 解决异常    |
| `hexo generate`                 | 生成静态文件 | 部署前      |
| `hexo deploy`                   | 部署         | 上线        |
| `hexo clean && hexo g -d`       | 一键部署     | 日常发布    |
| `hexo list post`                | 列出所有文章 | 管理        |
| `hexo list draft`               | 列出所有草稿 | 管理        |
| `git status`                    | 查看状态     | 检查更改    |
| `git add .`                     | 添加更改     | 提交前      |
| `git commit -m "说明"`          | 提交         | 本地记录    |
| `git push`                      | 推送         | 同步 GitHub |
| `git pull`                      | 拉取         | 获取更新    |
| `git log --oneline`             | 查看历史     | 查看记录    |
| `echo -n "域名" > source/CNAME` | 创建 CNAME   | 域名配置    |

---

## 八、经验总结

### 8.1 黄金法则

1. **写文章前**：先 `git pull` 确保最新
2. **部署前**：先 `hexo clean` 避免缓存问题
3. **遇到错误**：先看错误日志，再搜解决方案
4. **重要操作前**：先备份 `source/` 文件夹
5. **域名配置**：永远在 `source/` 下放 `CNAME` 文件

### 8.2 创建文章注意事项

| 注意点                | 正确做法                                |
| --------------------- | --------------------------------------- |
| **标题包含 `&` 符号** | 用引号括起来，或分步执行                |
| **标题包含空格**      | 用引号括起来                            |
| **同时打开编辑器**    | 分两步执行：先 `hexo new`，再 `notepad` |
| **文件名过长**        | 用短横线连接，避免特殊字符              |

### 8.3 常见误区

- ❌ 直接在 GitHub 网页修改文件
- ❌ 忘记 `:` 后的空格
- ❌ 提交 `node_modules/` 到仓库
- ❌ 推送前不拉取远程更新
- ❌ 忘记检查 CNAME 文件（导致域名消失）
- ❌ 命令中包含 `&` 等特殊字符不加处理

### 8.4 最佳实践

- ✅ 每次写文章前 `git pull`
- ✅ 每次部署用 `hexo clean && hexo g -d`
- ✅ 定期备份 `source/` 文件夹
- ✅ 写提交信息时用中文说明
- ✅ 每月检查一次 CNAME 文件
- ✅ 创建文章时分两步执行

### 8.5 日常写作流程

```bash
# 1. 更新代码
cd /e/MyBlog
git pull origin master

# 2. 创建新文章
hexo new "今日笔记"

# 3. 编辑文章
"D:/Typora/Typora.exe" source/_posts/今日笔记.md

# 4. 本地预览
hexo server

# 5. 确认无误后部署
hexo clean && hexo g -d

# 6. 备份源文件
git add source/_posts/
git commit -m "添加新文章：今日笔记"
git push origin master
```

### 8.6 快速发布

```bash
# 一条命令完成全部
cd /e/MyBlog && \
hexo new "新文章" && \
"D:/Typora/Typora.exe" source/_posts/新文章.md && \
hexo clean && hexo g -d && \
git add . && git commit -m "更新博客" && git push
```

---

## 🔗 相关链接

- [Hexo 官方文档](https://hexo.io/zh-cn/)
- [NexT 主题文档](https://theme-next.js.org/)
- [GitHub Pages 文档](https://pages.github.com/)
- [Markdown 语法指南](https://markdown.com.cn/)
- [Maxkore 博客](https://maxkore.bbroot.com)
- [Maxkore Wiki](https://maxkore-wiki.bbroot.com)
- [Maxkore Docs](https://docs.bbroot.com)

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
> **版本**：v2.0
>
> *本手册会持续更新，欢迎收藏！*
