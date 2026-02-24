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

> 全面指南：教你如何修改已发布的 Hexo 博客文章
> **适用博客**：https://maxkore.bbroot.com

---

## 📖 目录

- [一、准备工作](#一准备工作)
- [二、查找要修改的文章](#二查找要修改的文章)
- [三、打开文章编辑](#三打开文章编辑)
- [四、修改文章内容](#四修改文章内容)
- [五、修改文章属性](#五修改文章属性)
- [六、修改文章标题和文件名](#六修改文章标题和文件名)
- [七、修改文章日期](#七修改文章日期)
- [八、修改标签和分类](#八修改标签和分类)
- [九、添加或修改图片](#九添加或修改图片)
- [十、本地预览修改效果](#十本地预览修改效果)
- [十一、重新部署](#十一重新部署)
- [十二、完整修改流程示例](#十二完整修改流程示例)
- [十三、批量修改技巧](#十三批量修改技巧)
- [十四、常见问题](#十四常见问题)
- [十五、快捷命令](#十五快捷命令)

---

## 一、准备工作

### 1.1 进入博客目录

```bash
# 打开 Git Bash，进入博客目录
cd /e/MyBlog

# 确认当前目录
pwd
# 应该显示：/e/MyBlog
```

### 1.2 确保博客环境正常

```bash
# 检查 Hexo 是否可用
hexo -v

# 确保可以本地预览
hexo server
# 访问 http://localhost:4000 查看博客
# 按 Ctrl+C 停止
```

### 1.3 拉取最新代码（如果是多人协作）

```bash
# 确保本地代码是最新的
git pull origin master
```

---

## 二、查找要修改的文章

### 2.1 查看所有文章

```bash
# 列出所有文章
ls -la source/_posts/

# 按时间排序（最新的在前面）
ls -lt source/_posts/

# 按大小排序
ls -lS source/_posts/
```

### 2.2 按标题搜索

```bash
# 搜索包含关键词的文章
find source/_posts -name "*关键词*"

# 忽略大小写
find source/_posts -iname "*关键词*"

# 示例：搜索包含"Hexo"的文章
find source/_posts -name "*Hexo*"
```

### 2.3 按内容搜索

```bash
# 在文章中搜索特定内容
grep -r "要搜索的内容" source/_posts/

# 显示文件名和行号
grep -rn "Docker" source/_posts/

# 只显示文件名
grep -rl "JavaScript" source/_posts/

# 搜索并显示上下文
grep -r -A 3 -B 3 "关键词" source/_posts/
```

### 2.4 按日期搜索

```bash
# 查找某一天的文章
find source/_posts -name "2026-02-24*"

# 查找某个时间段的文章
find source/_posts -newermt "2026-02-01" ! -newermt "2026-02-28"

# 查找最近7天修改的文章
find source/_posts -mtime -7
```

### 2.5 使用 Hexo 命令查看

```bash
# 列出所有文章
hexo list post

# 列出最近的文章
hexo list post | head -10
```

### 2.6 创建搜索脚本

创建 `search-post.sh`：

```bash
#!/bin/bash
# 搜索文章脚本

if [ -z "$1" ]; then
  echo "请输入搜索关键词"
  exit 1
fi

echo "🔍 搜索关键词: $1"
echo "=================="

cd /e/MyBlog
for file in source/_posts/*.md; do
  if grep -q "$1" "$file"; then
    title=$(grep "^title:" "$file" | sed 's/title: //')
    date=$(grep "^date:" "$file" | sed 's/date: //')
    echo "📄 $title"
    echo "  日期: $date"
    echo "  文件: $(basename "$file")"
    echo "------------------"
  fi
done
```

---

## 三、打开文章编辑

### 3.1 用 Typora 打开（推荐）

```bash
# 用 Typora 打开文章
"D:/Typora/Typora.exe" "source/_posts/文章标题.md"

# 如果文件名有空格，一定要用引号
"D:/Typora/Typora.exe" "source/_posts/我的第一篇文章.md"
```

### 3.2 用记事本打开

```bash
# 用记事本打开
notepad "source/_posts/文章标题.md"

# 记事本优点：系统自带，无需安装
```

### 3.3 用 VS Code 打开

```bash
# 用 VS Code 打开
code "source/_posts/文章标题.md"

# 打开整个 posts 目录
code source/_posts/
```

### 3.4 快速打开命令

```bash
# 创建别名
alias edit="cd /e/MyBlog && \"D:/Typora/Typora.exe\""

# 使用别名
edit "source/_posts/文章标题.md"

# 一条命令打开最近修改的文章
ls -t source/_posts/*.md | head -1 | xargs "D:/Typora/Typora.exe"
```

---

## 四、修改文章内容

### 4.1 修改正文

在编辑器中直接修改 Markdown 内容：

```markdown
# 原内容
## 简介
这是一段旧内容...

# 修改后
## 简介
这是修改后的新内容...
```

### 4.2 添加新内容

```markdown
## 新增章节
这是新添加的内容...

### 小节
- 要点1
- 要点2
```

### 4.3 删除内容

直接删除不需要的段落或文字。

### 4.4 修改代码块

````markdown
```python
# 旧代码
print("Hello")

# 修改为
print("Hello, World!")
```
````

### 4.5 修改链接

```markdown
# 旧链接
[参考文档](https://old-url.com)

# 新链接
[参考文档](https://new-url.com)
```

---

## 五、修改文章属性

### 5.1 修改标题

在文章头部修改 `title` 字段：

```yaml
---
title: 新标题  # 修改这里
date: 2026-02-24 14:30:00
tags: [Hexo, 博客]
categories: [技术教程]
---
```

### 5.2 添加更新时间

在文章头部添加 `updated` 字段：

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
updated: 2026-02-25 09:15:00  # 添加更新时间
tags: [Hexo, 博客]
categories: [技术教程]
---
```

### 5.3 修改其他属性

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
updated: 2026-02-25 09:15:00
tags: [Hexo, 博客, 教程]        # 修改标签
categories: [技术教程]           # 修改分类
comments: false                 # 关闭评论
toc: false                      # 关闭目录
top: 1                          # 置顶
cover: /images/new-cover.jpg    # 修改封面图
---
```

### 5.4 批量修改属性脚本

创建 `update-frontmatter.sh`：

```bash
#!/bin/bash
# 批量更新文章头部

FILE="$1"
if [ ! -f "$FILE" ]; then
  echo "文件不存在"
  exit 1
fi

# 添加更新时间
if ! grep -q "^updated:" "$FILE"; then
  sed -i '/^date:/a updated: '"$(date +"%Y-%m-%d %H:%M:%S")" "$FILE"
else
  sed -i 's/^updated:.*/updated: '"$(date +"%Y-%m-%d %H:%M:%S")"/ "$FILE"
fi

echo "✅ 已更新: $FILE"
```

---

## 六、修改文章标题和文件名

### 6.1 只修改显示标题

如果只想修改显示在网页上的标题，不改文件名：

```yaml
---
title: 新显示标题  # 只改这里
date: 2026-02-24 14:30:00
---
```

### 6.2 同时修改文件名和标题

```bash
# 1. 重命名文件
mv "source/_posts/旧标题.md" "source/_posts/新标题.md"

# 2. 打开文件修改头部标题
"D:/Typora/Typora.exe" "source/_posts/新标题.md"
```

修改头部：
```yaml
---
title: 新标题  # 改为新标题
date: 2026-02-24 14:30:00
---
```

### 6.3 批量重命名

```bash
# 将所有空格替换为短横线
for file in source/_posts/*.md; do
  mv "$file" "${file// /-}"
done

# 添加前缀
for file in source/_posts/*.md; do
  mv "$file" "source/_posts/2026-${file##*/}"
done
```

---

## 七、修改文章日期

### 7.1 修改创建日期

```yaml
---
title: 文章标题
date: 2026-02-25 10:00:00  # 修改这里
---
```

### 7.2 添加或修改更新日期

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
updated: 2026-02-25 15:30:00  # 添加或修改
---
```

### 7.3 批量修改日期脚本

```bash
#!/bin/bash
# 批量更新文章日期

for file in source/_posts/*.md; do
  # 获取文件修改时间
  mod_time=$(stat -c %y "$file" | cut -d. -f1 | tr ' ' 'T')
  
  # 更新头部日期
  sed -i "s/^date:.*/date: $mod_time/" "$file"
done
```

---

## 八、修改标签和分类

### 8.1 修改标签

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
tags: 
  - 新标签1  # 修改
  - 新标签2  # 添加
  - 旧标签   # 删除
---
```

### 8.2 修改分类

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
categories:
  - 新分类    # 修改
  - 子分类    # 添加
---
```

### 8.3 批量添加标签

```bash
# 为所有没有标签的文章添加默认标签
for file in source/_posts/*.md; do
  if ! grep -q "^tags:" "$file"; then
    sed -i '/^---$/a tags: [博客]' "$file"
  fi
done
```

### 8.4 批量替换标签

```bash
# 将所有"旧标签"替换为"新标签"
sed -i 's/旧标签/新标签/g' source/_posts/*.md
```

---

## 九、添加或修改图片

### 9.1 准备新图片

```bash
# 创建文章图片目录
mkdir -p source/images/文章名

# 复制新图片
cp /path/to/new-image.jpg source/images/文章名/
```

### 9.2 在文章中插入图片

```markdown
# 旧图片
![旧图](/images/文章名/old.jpg)

# 修改为新图片
![新图](/images/文章名/new.jpg)
```

### 9.3 替换图片

```bash
# 直接覆盖文件
cp new-image.jpg source/images/文章名/old.jpg
```

### 9.4 批量替换图片路径

```bash
# 将所有图片路径从 old/ 改为 new/
sed -i 's/\/images\/old\//\/images\/new\//g' source/_posts/*.md
```

---

## 十、本地预览修改效果

### 10.1 启动预览

```bash
# 启动本地服务器
hexo server

# 或指定端口
hexo s -p 4001
```

### 10.2 检查修改

1. 访问 http://localhost:4000
2. 找到修改的文章
3. 检查：
   - [ ] 标题是否正确
   - [ ] 内容是否更新
   - [ ] 图片是否显示
   - [ ] 标签和分类是否更新
   - [ ] 日期是否正确
   - [ ] 链接是否有效

### 10.3 对比修改

```bash
# 查看文件修改历史
git log -p source/_posts/文章标题.md

# 查看文件差异
git diff source/_posts/文章标题.md
```

### 10.4 预览草稿

```bash
# 如果文章是草稿状态
hexo server --drafts
```

---

## 十一、重新部署

### 11.1 确认修改无误

```bash
# 确保预览效果满意
# 检查所有修改
```

### 11.2 重新生成并部署

```bash
# 一键部署
hexo clean && hexo g -d
```

### 11.3 提交到 Git（可选）

```bash
# 查看修改的文件
git status

# 添加修改
git add source/_posts/文章标题.md
git add source/images/  # 如果有图片修改

# 提交
git commit -m "更新文章：文章标题"

# 推送
git push origin master
```

### 11.4 验证线上效果

```bash
# 等待2-5分钟
# 访问博客查看修改是否生效
start https://maxkore.bbroot.com
```

---

## 十二、完整修改流程示例

### 示例1：修改文章内容

```bash
# 1. 找到要修改的文章
cd /e/MyBlog
find source/_posts -name "*Docker*"

# 2. 用 Typora 打开
"D:/Typora/Typora.exe" "source/_posts/Docker入门指南.md"

# 3. 修改内容
# 在 Typora 中修改文字、添加新内容

# 4. 添加更新时间
# 在头部添加：updated: 2026-02-25 10:30:00

# 5. 保存文件

# 6. 本地预览
hexo server
# 访问 http://localhost:4000 检查效果

# 7. 确认无误后部署
hexo clean && hexo g -d

# 8. 提交 Git
git add source/_posts/"Docker入门指南.md"
git commit -m "更新 Docker 文章，添加新内容"
git push
```

### 示例2：修改文章标题和分类

```bash
# 1. 重命名文件
mv "source/_posts/旧标题.md" "source/_posts/新标题.md"

# 2. 打开文件修改头部
"D:/Typora/Typora.exe" "source/_posts/新标题.md"
```

修改头部为：
```yaml
---
title: 新标题
date: 2026-02-24 14:30:00
updated: 2026-02-25 11:00:00
tags: [新标签1, 新标签2]
categories: [新分类]
---
```

```bash
# 3. 保存并预览
hexo server

# 4. 部署
hexo clean && hexo g -d
```

### 示例3：批量修改多篇文章

```bash
#!/bin/bash
# 批量更新脚本

cd /e/MyBlog

# 1. 找出所有需要修改的文章
for file in source/_posts/*技术*.md; do
  echo "处理: $file"
  
  # 2. 添加更新时间
  sed -i '/^date:/a updated: '"$(date +"%Y-%m-%d %H:%M:%S")" "$file"
  
  # 3. 修改标签
  sed -i 's/tags: \[.*\]/tags: [技术, 更新]/g' "$file"
  
  # 4. 显示修改后的头部
  head -10 "$file"
  echo "-------------------"
done

echo "✅ 批量修改完成"
```

---

## 十三、批量修改技巧

### 13.1 批量替换文本

```bash
# 在所有文章中替换文本
sed -i 's/旧文本/新文本/g' source/_posts/*.md

# 确认替换后再执行
grep -r "旧文本" source/_posts/
sed -i 's/旧文本/新文本/g' source/_posts/*.md
```

### 13.2 批量添加标签

```bash
# 为所有文章添加"博客"标签
for file in source/_posts/*.md; do
  if ! grep -q "tags:" "$file"; then
    sed -i '/^---$/a tags: [博客]' "$file"
  elif ! grep -q "博客" "$file"; then
    sed -i 's/\(tags: \[[^]]*\)/\1, 博客/' "$file"
  fi
done
```

### 13.3 批量更新日期

```bash
# 将所有文章的日期改为文件修改时间
for file in source/_posts/*.md; do
  mod_time=$(stat -c %y "$file" | cut -d. -f1)
  sed -i "s/^date:.*/date: $mod_time/" "$file"
done
```

### 13.4 批量删除文章

```bash
# 先确认要删除的文件
ls source/_posts/*测试*.md

# 确认后删除
rm source/_posts/*测试*.md
```

### 13.5 使用 VS Code 批量编辑

```bash
# 打开整个 posts 目录
code source/_posts/

# 使用 VS Code 的全局替换功能
# 按 Ctrl+Shift+H 进行全局替换
```

---

## 十四、常见问题

### 14.1 Q: 修改后文章不显示更新？

A: 可能原因及解决方法：

```bash
# 1. 清理缓存
hexo clean

# 2. 重新生成
hexo generate

# 3. 重新预览
hexo server

# 4. 检查更新时间
# 确保 updated 字段正确
```

### 14.2 Q: 修改后样式乱了？

A: 
```bash
# 检查 Markdown 语法
# 确保代码块正确闭合
# 检查标签配对

# 重新生成
hexo clean && hexo generate
```

### 14.3 Q: 修改标题后旧链接无法访问？

A: 如果修改了文件名，旧链接会失效。建议：
- 保留旧文件，添加重定向
- 或者在文章中添加 canonical 链接

### 14.4 Q: 如何恢复误删的内容？

A: 使用 Git 恢复：

```bash
# 查看文件修改历史
git log -p source/_posts/文章标题.md

# 找到 commit_id，恢复特定版本
git checkout commit_id -- source/_posts/文章标题.md
```

### 14.5 Q: 批量修改时出错了怎么办？

A: 
```bash
# 使用 Git 撤销修改
git checkout -- source/_posts/

# 或者恢复特定文件
git checkout -- source/_posts/错误的文件.md
```

---

## 十五、快捷命令

### 15.1 常用命令速查

| 命令                              | 说明     |
| --------------------------------- | -------- |
| `find source/_posts -name "*词*"` | 搜索文章 |
| `grep -r "词" source/_posts/`     | 内容搜索 |
| `"D:/Typora/Typora.exe" 文件`     | 打开编辑 |
| `hexo server`                     | 本地预览 |
| `hexo clean && hexo g -d`         | 重新部署 |
| `git diff 文件`                   | 查看修改 |
| `git checkout -- 文件`            | 撤销修改 |

### 15.2 一键编辑脚本

创建 `edit-post.sh`：

```bash
#!/bin/bash
# 一键编辑文章脚本

cd /e/MyBlog

if [ -z "$1" ]; then
  echo "请输入文章标题关键词"
  echo "最近文章："
  ls -lt source/_posts/ | head -5
  exit 1
fi

# 搜索文章
files=$(find source/_posts -name "*$1*" -o -iname "*$1*")

if [ -z "$files" ]; then
  echo "未找到包含 '$1' 的文章"
  exit 1
fi

count=$(echo "$files" | wc -l)
if [ "$count" -gt 1 ]; then
  echo "找到多篇文章："
  echo "$files"
  echo "请选择："
  select file in $files; do
    "D:/Typora/Typora.exe" "$file"
    break
  done
else
  "D:/Typora/Typora.exe" $files
fi
```

### 15.3 修改后快速部署

```bash
# 一条命令完成修改、预览、部署
edit-post.sh "关键词" && \
hexo server & \
sleep 5 && \
echo "预览中，按 Ctrl+C 停止预览后部署" && \
wait && \
hexo clean && hexo g -d
```

---

## 📝 一句话总结

```bash
# 查找文章
find source/_posts -name "*关键词*"

# 打开编辑
"D:/Typora/Typora.exe" "source/_posts/文件名.md"

# 预览修改
hexo server

# 重新部署
hexo clean && hexo g -d
```

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
>
> *修改文章就是这么简单！* ✏️