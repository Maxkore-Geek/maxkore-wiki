好的！我来帮你创建完整的"如何修改文章"指南。

## 创建如何修改文章指南

```bash
# 进入 Wiki 目录
cd /e/maxkore-wiki

# 用 Typora 创建修改文章指南
"D:/Typora/Typora.exe" docs/guides/edit-post.md
```

在 Typora 中**复制粘贴**以下完整内容：

````markdown
# ✏️ 如何修改文章

> 一步步教你修改已发布的 Hexo 博客文章
> **适用博客**：https://maxkore.bbroot.com

---

## 📖 快速导航

- [一、查找要修改的文章](#一查找要修改的文章)
- [二、打开文章编辑](#二打开文章编辑)
- [三、修改文章内容](#三修改文章内容)
- [四、修改文章属性](#四修改文章属性)
- [五、修改标题和文件名](#五修改标题和文件名)
- [六、修改日期](#六修改日期)
- [七、修改标签和分类](#七修改标签和分类)
- [八、修改图片](#八修改图片)
- [九、预览修改效果](#九预览修改效果)
- [十、重新部署](#十重新部署)
- [十一、完整示例](#十一完整示例)
- [十二、常见问题](#十二常见问题)

---

## 一、查找要修改的文章

### 1.1 查看所有文章

```bash
# 进入博客目录
cd /e/MyBlog

# 列出所有文章
ls -la source/_posts/

# 按时间排序（最新的在前面）
ls -lt source/_posts/
```

### 1.2 按标题搜索

```bash
# 搜索包含关键词的文章
find source/_posts -name "*关键词*"

# 示例：搜索包含"Hexo"的文章
find source/_posts -name "*Hexo*"
```

### 1.3 按内容搜索

```bash
# 在文章中搜索特定内容
grep -r "要搜索的内容" source/_posts/

# 显示文件名和行号
grep -rn "Docker" source/_posts/

# 只显示文件名
grep -rl "JavaScript" source/_posts/
```

### 1.4 快速查找命令

```bash
# 查找最近修改的文章
ls -lt source/_posts/ | head -10

# 查找特定日期的文章
find source/_posts -name "2026-02-24*"
```

---

## 二、打开文章编辑

### 2.1 用 Typora 打开（推荐）

```bash
# 用 Typora 打开文章
"D:/Typora/Typora.exe" "source/_posts/文章标题.md"

# 如果文件名有空格，一定要用引号
"D:/Typora/Typora.exe" "source/_posts/我的第一篇文章.md"
```

### 2.2 用记事本打开

```bash
# 用记事本打开
notepad "source/_posts/文章标题.md"
```

### 2.3 用 VS Code 打开

```bash
# 用 VS Code 打开
code "source/_posts/文章标题.md"

# 打开整个 posts 目录
code source/_posts/
```

### 2.4 快速打开命令

```bash
# 找到并打开最近修改的文章
ls -t source/_posts/*.md | head -1 | xargs "D:/Typora/Typora.exe"
```

---

## 三、修改文章内容

### 3.1 修改正文

在编辑器中直接修改 Markdown 内容：

```markdown
## 原内容
这是一段旧内容...

## 修改后
这是修改后的新内容...
```

### 3.2 添加新内容

```markdown
## 新增章节
这是新添加的内容...

### 小节
- 要点1
- 要点2
```

### 3.3 删除内容

直接删除不需要的段落或文字。

### 3.4 修改代码块

````markdown
```python
# 旧代码
print("Hello")

# 修改为
print("Hello, World!")
```
````

### 3.5 修改链接

```markdown
# 旧链接
[参考文档](https://old-url.com)

# 新链接
[参考文档](https://new-url.com)
```

---

## 四、修改文章属性

### 4.1 修改标题

在文章头部修改 `title` 字段：

```yaml
---
title: 新标题  # 修改这里
date: 2026-02-24 14:30:00
---
```

### 4.2 添加更新时间

在文章头部添加 `updated` 字段：

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
updated: 2026-02-25 09:15:00  # 添加更新时间
---
```

### 4.3 修改其他属性

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
updated: 2026-02-25 09:15:00
tags: [新标签1, 新标签2]     # 修改标签
categories: [新分类]          # 修改分类
comments: false              # 关闭评论
toc: false                   # 关闭目录
top: 1                       # 置顶
---
```

---

## 五、修改标题和文件名

### 5.1 只修改显示标题

如果只想修改网页上显示的标题，不改文件名：

```yaml
---
title: 新显示标题  # 只改这里
date: 2026-02-24 14:30:00
---
```

### 5.2 同时修改文件名和标题

```bash
# 1. 重命名文件
mv "source/_posts/旧标题.md" "source/_posts/新标题.md"

# 2. 打开文件修改头部标题
"D:/Typora/Typora.exe" "source/_posts/新标题.md"
```

修改头部：
```yaml
---
title: 新标题
date: 2026-02-24 14:30:00
---
```

### 5.3 批量重命名

```bash
# 将所有空格替换为短横线
for file in source/_posts/*.md; do
  mv "$file" "${file// /-}"
done
```

---

## 六、修改日期

### 6.1 修改创建日期

```yaml
---
title: 文章标题
date: 2026-02-25 10:00:00  # 修改这里
---
```

### 6.2 添加或修改更新日期

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
updated: 2026-02-25 15:30:00  # 添加或修改
---
```

### 6.3 批量更新日期

```bash
# 将所有文章的日期改为今天
for file in source/_posts/*.md; do
  sed -i "s/^date:.*/date: $(date +"%Y-%m-%d %H:%M:%S")/" "$file"
done
```

---

## 七、修改标签和分类

### 7.1 修改标签

```yaml
---
title: 文章标题
tags: 
  - 新标签1  # 修改
  - 新标签2  # 添加
---
```

### 7.2 修改分类

```yaml
---
title: 文章标题
categories:
  - 新分类    # 修改
  - 子分类    # 添加
---
```

### 7.3 批量添加标签

```bash
# 为没有标签的文章添加默认标签
for file in source/_posts/*.md; do
  if ! grep -q "^tags:" "$file"; then
    sed -i '/^---$/a tags: [博客]' "$file"
  fi
done
```

---

## 八、修改图片

### 8.1 添加新图片

```bash
# 创建图片目录
mkdir -p source/images/文章名

# 复制新图片
cp /path/to/new-image.jpg source/images/文章名/
```

### 8.2 在文章中插入图片

```markdown
![图片描述](/images/文章名/图片.jpg)
```

### 8.3 替换图片

```bash
# 直接覆盖文件
cp new-image.jpg source/images/文章名/old.jpg
```

### 8.4 删除图片

```bash
# 删除图片文件
rm source/images/文章名/old.jpg

# 删除文章中的图片引用
```

---

## 九、预览修改效果

### 9.1 启动本地预览

```bash
# 启动本地服务器
hexo server

# 访问 http://localhost:4000
```

### 9.2 检查修改内容

1. 找到修改的文章
2. 检查标题是否正确
3. 检查内容是否更新
4. 检查图片是否显示
5. 检查标签和分类
6. 检查日期是否正确

### 9.3 对比修改

```bash
# 查看文件修改历史
git diff source/_posts/文章标题.md
```

---

## 十、重新部署

### 10.1 确认修改无误

```bash
# 预览效果满意后，停止预览
# 按 Ctrl+C 停止 hexo server
```

### 10.2 重新生成并部署

```bash
# 一键部署
hexo clean && hexo g -d
```

### 10.3 提交到 Git（可选）

```bash
# 查看修改的文件
git status

# 添加修改
git add source/_posts/文章标题.md

# 提交
git commit -m "更新文章：文章标题"

# 推送
git push origin master
```

### 10.4 验证线上效果

```bash
# 等待2-5分钟
# 访问博客查看修改是否生效
start https://maxkore.bbroot.com
```

---

## 十一、完整示例

### 示例：修改一篇技术文章

```bash
# 1. 找到要修改的文章
cd /e/MyBlog
find source/_posts -name "*Docker*"

# 输出：source/_posts/Docker入门指南.md

# 2. 用 Typora 打开
"D:/Typora/Typora.exe" "source/_posts/Docker入门指南.md"
```

在 Typora 中修改：

```yaml
---
title: Docker 从入门到精通  # 修改标题
date: 2026-02-24 14:30:00
updated: 2026-02-25 10:30:00  # 添加更新时间
tags: [Docker, 容器, 教程]     # 添加新标签
categories: [技术教程]          # 修改分类
---
```

```markdown
# Docker 从入门到精通

## 新增章节：Docker Compose 使用
添加新内容...
```

```bash
# 3. 保存文件

# 4. 本地预览
hexo server
# 访问 http://localhost:4000 检查效果

# 5. 确认无误后部署
hexo clean && hexo g -d

# 6. 提交 Git
git add source/_posts/"Docker入门指南.md"
git commit -m "更新 Docker 文章，添加 Compose 章节"
git push
```

---

## 十二、常见问题

### 12.1 Q: 修改后文章不显示更新？

**解决方法：**
```bash
# 清理缓存
hexo clean

# 重新生成
hexo generate

# 重新预览
hexo server
```

### 12.2 Q: 修改标题后旧链接无法访问？

**解决方法：**
- 保留旧文件，添加重定向
- 或者在文章中添加 canonical 链接

### 12.3 Q: 如何恢复误删的内容？

**解决方法：**
```bash
# 使用 Git 恢复
git checkout -- source/_posts/文章标题.md

# 或者查看历史版本
git log -p source/_posts/文章标题.md
git checkout commit_id -- source/_posts/文章标题.md
```

### 12.4 Q: 批量修改时出错了？

**解决方法：**
```bash
# 使用 Git 撤销所有修改
git checkout -- source/_posts/
```

---

## 📝 快速命令速查

```bash
# 查找文章
find source/_posts -name "*关键词*"

# 打开编辑
"D:/Typora/Typora.exe" "source/_posts/文件名.md"

# 预览
hexo server

# 重新部署
hexo clean && hexo g -d

# Git 提交
git add source/_posts/文件名.md
git commit -m "更新文章"
git push
```

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
>
> *修改文章就是这么简单！* ✏️