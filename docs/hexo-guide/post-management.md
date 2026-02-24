# 📂 文章管理指南

> 全面掌握 Hexo 博客的文章管理技巧
> 涵盖新建、修改、删除、批量操作等所有功能

---

## 📖 目录

- [一、新建文章](#一新建文章)
- [二、编辑文章](#二编辑文章)
- [三、删除文章](#三删除文章)
- [四、批量操作](#四批量操作)
- [五、草稿管理](#五草稿管理)
- [六、页面管理](#六页面管理)
- [七、文章分类管理](#七文章分类管理)
- [八、文章状态管理](#八文章状态管理)
- [九、搜索和查找](#九搜索和查找)
- [十、备份和恢复](#十备份和恢复)
- [十一、高级技巧](#十一高级技巧)
- [十二、常见问题](#十二常见问题)
- [十三、快捷命令速查](#十三快捷命令速查)

---

## 一、新建文章

### 1.1 基本创建方法

```bash
# 进入博客目录
cd /e/MyBlog

# 创建新文章（标题可以用中文）
hexo new "文章标题"
```

### 1.2 创建文章并立即编辑

```bash
# 方法1：分两步执行
hexo new "文章标题"
"D:/Typora/Typora.exe" "source/_posts/文章标题.md"

# 方法2：用记事本
hexo new "文章标题" && notepad "source/_posts/文章标题.md"

# 方法3：一条命令（注意引号）
hexo new "文章标题" && "D:/Typora/Typora.exe" "source/_posts/文章标题.md"
```

### 1.3 创建文章时指定布局

```bash
# 创建普通文章（默认）
hexo new post "文章标题"

# 创建草稿
hexo new draft "草稿标题"

# 创建页面
hexo new page "页面名称"
```

### 1.4 创建文章时指定路径

```bash
# 在指定分类下创建文章
hexo new "技术/文章标题"
hexo new "生活/日记/今天的心情"
```

### 1.5 批量创建文章

```bash
# 创建多篇文章
for i in {1..5}; do
  hexo new "测试文章$i"
done

# 创建系列文章
for title in "入门篇" "进阶篇" "高级篇"; do
  hexo new "Hexo教程-$title"
done
```

### 1.6 文章模板

编辑 `scaffolds/post.md` 设置默认模板：

```yaml
---
title: {
  { title }}
date: {
  { date }}
tags:
categories:
comments: true
toc: true
---

<!-- more -->

# {
  { title }}

## 简介

在这里写文章简介...

## 正文

开始写正文内容...

## 总结

总结文章要点...
```

---

## 二、编辑文章

### 2.1 打开文章编辑

```bash
# 用 Typora 打开（推荐）
"D:/Typora/Typora.exe" "source/_posts/文章标题.md"

# 用记事本打开
notepad "source/_posts/文章标题.md"

# 用 VS Code 打开
code "source/_posts/文章标题.md"
```

### 2.2 查找要编辑的文章

```bash
# 列出所有文章
ls -la source/_posts/

# 按时间排序查看
ls -lt source/_posts/

# 搜索文章
find source/_posts -name "*关键词*"
```

### 2.3 修改文章标题

**方法1：直接修改文件名和内容**

```bash
# 重命名文件
mv "source/_posts/旧标题.md" "source/_posts/新标题.md"

# 编辑文件，修改头部中的 title
"D:/Typora/Typora.exe" "source/_posts/新标题.md"
```

**方法2：只修改头部中的 title**

```yaml
---
title: 新标题  # 修改这里
date: 2026-02-24 14:30:00
---
```

### 2.4 修改文章日期

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00        # 修改创建时间
updated: 2026-02-25 09:15:00      # 添加或修改更新时间
---
```

### 2.5 修改标签和分类

```yaml
---
title: 文章标题
tags: 
  - 新标签1  # 修改或添加标签
  - 新标签2
categories:
  - 新分类    # 修改分类
---
```

### 2.6 批量编辑文章

```bash
# 用 VS Code 打开整个目录批量编辑
code source/_posts/

# 批量替换文本
sed -i 's/旧词/新词/g' source/_posts/*.md

# 批量添加标签到所有文章
for file in source/_posts/*.md; do
  sed -i '/^---$/a tags: [博客]' "$file"
done
```

### 2.7 编辑后重新部署

```bash
# 预览修改效果
hexo server

# 确认无误后部署
hexo clean && hexo g -d
```

---

## 三、删除文章

### 3.1 删除单篇文章

```bash
# 方法1：直接删除
rm "source/_posts/要删除的文章.md"

# 方法2：移动到回收站（安全）
mv "source/_posts/要删除的文章.md" ~/回收站/

# 方法3：移动到草稿（不删除，只是不发布）
mv "source/_posts/要删除的文章.md" source/_drafts/
```

### 3.2 删除后重新部署

```bash
# 清理并重新生成
hexo clean && hexo g -d
```

### 3.3 批量删除

```bash
# 删除所有测试文章
rm source/_posts/*测试*.md

# 删除指定日期的文章
rm source/_posts/2025-*.md

# 删除符合条件的文章（先确认再删除）
ls source/_posts/*备份*.md  # 先列出
rm source/_posts/*备份*.md  # 确认后删除
```

### 3.4 安全删除（先备份）

```bash
# 备份到其他目录
cp source/_posts/重要文章.md ~/backup/

# 确认备份成功后删除
rm source/_posts/重要文章.md
```

### 3.5 从 Git 恢复被删除的文章

```bash
# 如果已经提交到 Git
git log -- "source/_posts/被删除的文章.md"

# 找到 commit_id 后恢复
git checkout commit_id -- "source/_posts/被删除的文章.md"
```

---

## 四、批量操作

### 4.1 批量重命名

```bash
# 将所有空格替换为短横线
for file in source/_posts/*.md; do
  mv "$file" "${file// /-}"
done

# 批量添加前缀
for file in source/_posts/*.md; do
  mv "$file" "source/_posts/2026-${file##*/}"
done
```

### 4.2 批量替换内容

```bash
# 将所有文章中的"旧博客"替换为"新博客"
sed -i 's/旧博客/新博客/g' source/_posts/*.md

# 批量替换标签
for file in source/_posts/*.md; do
  sed -i 's/tags: \[.*\]/tags: [Hexo, 博客]/g' "$file"
done
```

### 4.3 批量添加 Front-matter

```bash
# 为没有 Front-matter 的文章添加默认头部
for file in source/_posts/*.md; do
  if ! grep -q "^---" "$file"; then
    sed -i '1i ---\ntitle: '${file##*/}'\ndate: '$(date +"%Y-%m-%d %H:%M:%S")'\n---\n' "$file"
  fi
done
```

### 4.4 批量导出文章列表

```bash
# 导出所有文章标题
grep "^title:" source/_posts/*.md | sed 's/.*title: //' > 文章列表.txt

# 导出带日期的文章列表
for file in source/_posts/*.md; do
  title=$(grep "^title:" "$file" | sed 's/.*title: //')
  date=$(grep "^date:" "$file" | sed 's/.*date: //')
  echo "$date - $title"
done | sort > 文章列表.txt
```

### 4.5 批量统计

```bash
# 统计文章数量
ls source/_posts/ | wc -l

# 统计标签使用频率
grep -h "^tags:" source/_posts/*.md | sort | uniq -c | sort -nr

# 统计各分类文章数
grep -h "^categories:" source/_posts/*.md | sort | uniq -c | sort -nr

# 统计总字数
wc -w source/_posts/*.md
```

---

## 五、草稿管理

### 5.1 创建草稿

```bash
# 创建草稿
hexo new draft "草稿标题"

# 查看草稿
ls source/_drafts/
```

### 5.2 编辑草稿

```bash
# 编辑草稿
"D:/Typora/Typora.exe" "source/_drafts/草稿标题.md"
```

### 5.3 发布草稿

```bash
# 发布草稿为文章
hexo publish "草稿标题"

# 发布后文章会移到 source/_posts/
```

### 5.4 预览草稿

```bash
# 本地预览时显示草稿
hexo server --drafts

# 或
hexo s --drafts
```

### 5.5 管理多个草稿

```bash
# 列出所有草稿
ls -la source/_drafts/

# 删除草稿
rm source/_drafts/不需要的草稿.md

# 批量发布所有草稿
for draft in source/_drafts/*.md; do
  name=$(basename "$draft" .md)
  hexo publish "$name"
done
```

---

## 六、页面管理

### 6.1 创建独立页面

```bash
# 创建“关于”页面
hexo new page about

# 创建“标签”页面
hexo new page tags

# 创建“分类”页面
hexo new page categories

# 创建“友链”页面
hexo new page links
```

### 6.2 编辑页面

```bash
# 编辑页面内容
"D:/Typora/Typora.exe" "source/about/index.md"
```

### 6.3 页面 Front-matter 示例

```yaml
---
title: 关于我
date: 2026-02-24 14:30:00
type: about  # 页面类型
comments: false  # 页面通常不需要评论
layout: page  # 页面布局
---
```

### 6.4 自定义 HTML 页面

```bash
# 创建自定义 HTML 页面
touch source/自定义页面.html

# 编辑
"D:/Typora/Typora.exe" source/自定义页面.html
```

### 6.5 删除页面

```bash
# 删除页面目录
rm -rf source/about/

# 或只删除文件
rm source/about/index.md
```

---

## 七、文章分类管理

### 7.1 按分类整理

```bash
# 创建分类目录
mkdir -p source/_posts/技术
mkdir -p source/_posts/生活
mkdir -p source/_posts/笔记
mkdir -p source/_posts/教程

# 移动文章到分类目录
mv source/_posts/技术文章.md source/_posts/技术/
mv source/_posts/生活日记.md source/_posts/生活/
```

### 7.2 配置文件支持分类目录

在 `_config.yml` 中设置：

```yaml
# 新文章按分类保存
new_post_name: :categories/:title.md

# URL 包含分类
permalink: :categories/:title/
```

### 7.3 分类统计

```bash
# 查看各分类文章数
ls -la source/_posts/技术/ | wc -l
ls -la source/_posts/生活/ | wc -l

# 或使用脚本统计
for dir in source/_posts/*/; do
  count=$(ls -la "$dir" 2>/dev/null | grep ".md" | wc -l)
  echo "$dir: $count 篇文章"
done
```

---

## 八、文章状态管理

### 8.1 置顶文章

在 Front-matter 中添加：

```yaml
---
title: 置顶文章
top: 1  # 数字越大越靠前
# 或使用 sticky
sticky: 1
---
```

### 8.2 私密/加密文章

```yaml
---
title: 私密文章
password: 123456
abstract: 这是一篇加密文章，请输入密码查看。
message: 密码错误，请重试。
---
```

### 8.3 定时发布

设置未来的日期：

```yaml
---
title: 未来发布的文章
date: 2026-03-01 09:00:00  # 未来的日期
---
```

### 8.4 隐藏文章（不发布）

```bash
# 方法1：移到草稿
mv source/_posts/文章.md source/_drafts/

# 方法2：重命名文件（以下划线开头）
mv source/_posts/文章.md source/_posts/_文章.md

# 方法3：在配置中设置 skip_render
# 在 _config.yml 中添加：
skip_render: _*.md
```

---

## 九、搜索和查找

### 9.1 按标题搜索

```bash
# 查找包含关键词的文章
find source/_posts -name "*关键词*"

# 忽略大小写
find source/_posts -iname "*关键词*"
```

### 9.2 按内容搜索

```bash
# 在文章中搜索内容
grep -r "要搜索的内容" source/_posts/

# 显示文件名和行号
grep -rn "关键词" source/_posts/

# 只显示文件名
grep -rl "关键词" source/_posts/
```

### 9.3 按日期搜索

```bash
# 查找某一天的文章
find source/_posts -name "2026-02-24*"

# 查找某个时间段的文章
find source/_posts -newermt "2026-02-01" ! -newermt "2026-02-28"
```

### 9.4 按标签/分类搜索

```bash
# 查找包含特定标签的文章
grep -r "tags:.*Hexo" source/_posts/

# 查找包含特定分类的文章
grep -r "categories:.*技术" source/_posts/
```

### 9.5 使用脚本高级搜索

创建 `search-posts.sh`：

```bash
#!/bin/bash
# 搜索文章脚本

echo "搜索关键词: $1"
echo "=================="

for file in source/_posts/*.md; do
  if grep -q "$1" "$file"; then
    title=$(grep "^title:" "$file" | sed 's/title: //')
    date=$(grep "^date:" "$file" | sed 's/date: //')
    echo "📄 $title"
    echo "  日期: $date"
    echo "  文件: $file"
    echo "------------------"
  fi
done
```

---

## 十、备份和恢复

### 10.1 手动备份

```bash
# 备份所有文章
cp -r source/_posts source/_posts_backup_$(date +%Y%m%d)

# 创建压缩备份
tar -czf posts_backup_$(date +%Y%m%d).tar.gz source/_posts/
```

### 10.2 使用 Git 备份

```bash
# 提交到 Git
git add source/_posts/
git commit -m "备份文章 $(date +%Y-%m-%d)"
git push
```

### 10.3 自动备份脚本

创建 `backup-posts.sh`：

```bash
#!/bin/bash
# 自动备份脚本

BACKUP_DIR="/e/博客备份"
DATE=$(date +%Y%m%d_%H%M%S)

# 创建备份目录
mkdir -p "$BACKUP_DIR"

# 备份文章
cp -r /e/MyBlog/source/_posts "$BACKUP_DIR/posts_$DATE"

# 备份配置文件
cp /e/MyBlog/_config.yml "$BACKUP_DIR/config_$DATE.yml"

# 压缩
cd "$BACKUP_DIR"
tar -czf "backup_$DATE.tar.gz" "posts_$DATE" "config_$DATE.yml"

# 删除临时文件
rm -rf "posts_$DATE" "config_$DATE.yml"

echo "✅ 备份完成: $BACKUP_DIR/backup_$DATE.tar.gz"
```

### 10.4 恢复备份

```bash
# 解压备份
tar -xzf backup_20260224.tar.gz

# 恢复文章
cp -r posts_20260224/* /e/MyBlog/source/_posts/

# 恢复配置文件
cp config_20260224.yml /e/MyBlog/_config.yml
```

---

## 十一、高级技巧

### 11.1 文章模板变量

在文章中使用变量：

```markdown
---
title: 文章标题
date: 2026-02-24 14:30:00
author: Maxkore
---

本文作者：{ { page.author }}
创建时间：{ { page.date }}
```

### 11.2 条件内容

```markdown
{% if page.tags contains '教程' %}
  <div class="notice">这是一篇教程文章</div>
{% endif %}
```

### 11.3 文章引用

```markdown
<!-- 引用其他文章 -->
{% post_link 其他文章标题 %}

<!-- 引用文章中的图片 -->
![图片描述]({ % asset_path image.jpg % })
```

### 11.4 自定义排序

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
order: 1  # 自定义排序字段
---
```

### 11.5 文章别名

```yaml
---
title: 文章标题
alias: /old-url/  # 旧链接，用于重定向
---
```

### 11.6 文章过期提醒

```yaml
---
title: 旧文章
date: 2024-01-01
expired: true  # 自定义过期标记
---
```

在模板中判断：
```html
{% if page.expired %}
  <div class="warning">⚠️ 本文可能已过时</div>
{% endif %}
```

---

## 十二、常见问题

### 12.1 Q: 新建的文章找不到？

A: 检查是否正确生成：
```bash
# 查看是否在 posts 目录
ls -la source/_posts/

# 查看 Hexo 是否识别
hexo list post
```

### 12.2 Q: 修改文章后不生效？

A: 清理缓存重新生成：
```bash
hexo clean
hexo generate
hexo server
```

### 12.3 Q: 批量操作时误删文件？

A: 用 Git 恢复：
```bash
git checkout -- source/_posts/误删的文件.md
```

### 12.4 Q: 文章太多，管理混乱？

A: 建议：
1. 按年份建立子目录
2. 使用分类和标签
3. 定期归档旧文章
4. 用脚本自动化管理

### 12.5 Q: 如何迁移文章到新博客？

A: 
```bash
# 复制文章文件
cp -r 旧博客/source/_posts/* 新博客/source/_posts/

# 检查并更新 Front-matter
# 可能需要调整日期格式、分类等
```

---

## 十三、快捷命令速查

| 命令                                       | 说明         |
| ------------------------------------------ | ------------ |
| `hexo new "标题"`                          | 新建文章     |
| `hexo new draft "标题"`                    | 新建草稿     |
| `hexo publish "标题"`                      | 发布草稿     |
| `hexo new page "名称"`                     | 新建页面     |
| `hexo list post`                           | 列出所有文章 |
| `hexo list draft`                          | 列出所有草稿 |
| `hexo server --drafts`                     | 预览包含草稿 |
| `rm source/_posts/文章.md`                 | 删除文章     |
| `mv source/_posts/文章.md source/_drafts/` | 转为草稿     |
| `find source/_posts -name "*词*"`          | 搜索文章     |
| `grep -r "词" source/_posts/`              | 内容搜索     |
| `sed -i 's/旧/新/g' *.md`                  | 批量替换     |
| `cp -r source/_posts source/_posts_backup` | 备份文章     |

---

## 📝 一键管理脚本

创建 `manage-posts.sh`：

```bash
#!/bin/bash
# 文章管理脚本

echo "📂 文章管理工具"
echo "================"
echo "1. 统计文章数量"
echo "2. 列出所有文章"
echo "3. 搜索文章"
echo "4. 批量替换文本"
echo "5. 备份文章"
echo "================"
read -p "请选择 [1-5]: " choice

case $choice in
  1)
    count=$(ls source/_posts/*.md 2>/dev/null | wc -l)
    draft=$(ls source/_drafts/*.md 2>/dev/null | wc -l)
    echo "📊 文章统计"
    echo "已发布: $count 篇"
    echo "草稿: $draft 篇"
    ;;
  2)
    echo "📄 所有文章："
    ls -lt source/_posts/ | grep ".md"
    ;;
  3)
    read -p "输入关键词: " keyword
    grep -l "$keyword" source/_posts/*.md
    ;;
  4)
    read -p "输入要替换的文本: " old
    read -p "输入新文本: " new
    sed -i "s/$old/$new/g" source/_posts/*.md
    echo "✅ 替换完成"
    ;;
  5)
    tar -czf "posts_backup_$(date +%Y%m%d).tar.gz" source/_posts/
    echo "✅ 备份完成"
    ;;
esac
```

使用脚本：
```bash
chmod +x manage-posts.sh
./manage-posts.sh
```

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
>
> *本文档会持续更新，欢迎收藏！*