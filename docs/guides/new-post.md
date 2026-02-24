# 📝 如何新建文章

> 一步步教你如何在 Hexo 博客中创建新文章
> **适用博客**：https://maxkore.bbroot.com

---

## 📖 目录

- [一、准备工作](#一准备工作)
- [二、新建文章（三种方法）](#二新建文章三种方法)
- [三、编辑文章](#三编辑文章)
- [四、文章头部配置](#四文章头部配置)
- [五、写文章内容](#五写文章内容)
- [六、插入图片](#六插入图片)
- [七、本地预览](#七本地预览)
- [八、发布文章](#八发布文章)
- [九、完整流程示例](#九完整流程示例)
- [十、常见问题](#十常见问题)
- [十一、快捷命令](#十一快捷命令)
- [十二、写作技巧](#十二写作技巧)

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

---

## 二、新建文章（三种方法）

### 方法一：命令行创建（最常用）

```bash
# 基本命令
hexo new "文章标题"

# 例如：
hexo new "我的第一篇文章"
hexo new "Hexo 教程"
hexo new "2026年2月总结"
```

### 方法二：指定分类创建

```bash
# 在指定分类下创建文章
hexo new "技术/Python入门"
hexo new "生活/旅行日记"
hexo new "笔记/读书笔记"

# 这会在 source/_posts/技术/ 目录下创建文章
```

### 方法三：手动创建

```bash
# 直接在 _posts 目录创建文件
touch "source/_posts/手动创建的文章.md"

# 用 Typora 打开编辑
"D:/Typora/Typora.exe" "source/_posts/手动创建的文章.md"
```

### 创建后验证

```bash
# 查看刚创建的文件
ls -la source/_posts/

# 应该能看到 文章标题.md 文件
```

---

## 三、编辑文章

### 3.1 用 Typora 编辑（推荐）

```bash
# 用 Typora 打开文章
"D:/Typora/Typora.exe" "source/_posts/文章标题.md"

# Typora 优点：
# - 实时预览
# - 支持表格、图片拖拽
# - 多种主题
# - 导出 PDF/Word
```

### 3.2 用记事本编辑

```bash
# 用记事本打开
notepad "source/_posts/文章标题.md"

# 优点：系统自带，无需安装
# 缺点：无预览功能
```

### 3.3 用 VS Code 编辑

```bash
# 用 VS Code 打开
code "source/_posts/文章标题.md"

# 优点：插件丰富，语法高亮
# 缺点：需要安装
```

### 3.4 快速打开命令

```bash
# 一条命令创建并打开
hexo new "新文章" && "D:/Typora/Typora.exe" "source/_posts/新文章.md"

# 创建后立即打开
hexo new "今日笔记"
start "source/_posts/今日笔记.md"  # Windows 默认程序打开
```

---

## 四、文章头部配置

### 4.1 基本头部格式

每篇文章开头必须有 Front-matter，用 `---` 包裹：

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
---
```

### 4.2 完整头部配置

```yaml
---
title: 我的第一篇文章          # 文章标题（必填）
date: 2026-02-24 14:30:00     # 创建时间（必填）
updated: 2026-02-24 15:30:00  # 更新时间（可选）
tags:                          # 标签（可选）
  - Hexo
  - 博客
  - 教程
categories:                    # 分类（可选）
  - 技术教程
  - 博客搭建
keywords: [Hexo, 博客, 教程]   # 关键词（可选）
description: 这是一篇教程文章   # 描述（可选）
comments: true                 # 是否开启评论（可选）
toc: true                      # 是否显示目录（可选）
top: 1                         # 是否置顶（可选）
cover: /images/cover.jpg       # 封面图（可选）
---
```

### 4.3 快速插入头部模板

在 Typora 中创建代码片段，或使用这个命令：

```bash
# 自动添加头部模板
echo '---
title: '"$1"'
date: '"$(date +"%Y-%m-%d %H:%M:%S")"'
tags: []
categories: []
---

# '"$1"'

## 简介

## 正文

## 总结
' > "source/_posts/$1.md"
```

---

## 五、写文章内容

### 5.1 Markdown 基本语法

```markdown
# 一级标题
## 二级标题
### 三级标题

**粗体文字**
*斜体文字*
~~删除线~~

- 无序列表项1
- 无序列表项2
  - 嵌套列表

1. 有序列表项1
2. 有序列表项2

[链接文字](https://example.com)

![图片描述](/images/图片.jpg)

> 引用文字

`行内代码`

```语言
代码块
```
```

### 5.2 文章结构建议

```markdown
---
title: 文章标题
date: 2026-02-24 14:30:00
tags: []
categories: []
---

# 文章标题

## 引言

简单介绍文章要讲什么...

## 正文

### 第一部分

内容...

### 第二部分

内容...

## 总结

回顾要点，总结收获...

## 参考资料

- [参考链接1](url)
- [参考链接2](url)

---

> 最后更新：2026-02-24
```

### 5.3 使用摘要

在文章中添加 `<!-- more -->` 标记：

```markdown
这里是文章摘要，会显示在首页列表...
<!-- more -->
这里是文章正文，点击"阅读全文"后才显示...
```

---

## 六、插入图片

### 6.1 准备图片

```bash
# 创建图片目录
mkdir -p source/images/文章名

# 将图片复制到目录
cp /path/to/image.jpg source/images/文章名/
```

### 6.2 插入图片语法

```markdown
# 基本插入
![图片描述](/images/文章名/图片.jpg)

# 带尺寸的图片
<img src="/images/文章名/图片.jpg" width="400" height="300">

# 带链接的图片
[![图片描述](/images/文章名/图片.jpg)](https://example.com)
```

### 6.3 使用 Typora 拖拽插入

1. 打开 Typora
2. 直接将图片拖拽到编辑区
3. 自动生成图片语法

### 6.4 批量处理图片

```bash
# 批量压缩图片（需要安装 imagemin）
npx imagemin images/* --out-dir images/optimized
```

---

## 七、本地预览

### 7.1 启动预览

```bash
# 启动本地服务器
hexo server

# 或指定端口
hexo s -p 4001
```

### 7.2 预览时自动刷新

```bash
# 启用 drafts 预览（显示草稿）
hexo server --drafts

# 生成并预览
hexo generate && hexo server
```

### 7.3 检查文章效果

1. 访问 http://localhost:4000
2. 查看首页是否有新文章
3. 点击文章标题查看详情
4. 检查格式是否正确
5. 验证链接是否有效

### 7.4 修改后实时刷新

修改文章后，保存文件，刷新浏览器即可看到更新，无需重启 server。

---

## 八、发布文章

### 8.1 一键部署

```bash
# 清理缓存并部署
hexo clean && hexo g -d
```

### 8.2 分步部署

```bash
# 清理缓存
hexo clean

# 生成静态文件
hexo generate

# 部署到 GitHub
hexo deploy
```

### 8.3 提交源文件到 Git（可选）

```bash
# 添加文章到 Git
git add source/_posts/文章标题.md

# 提交
git commit -m "添加新文章：文章标题"

# 推送到 GitHub
git push origin master
```

### 8.4 等待部署

部署后等待 2-5 分钟，访问：
- https://maxkore.bbroot.com
- 查看新文章是否上线

---

## 九、完整流程示例

### 示例1：写一篇技术文章

```bash
# 1. 进入博客目录
cd /e/MyBlog

# 2. 创建文章
hexo new "Hexo 从入门到精通"

# 3. 用 Typora 编辑
"D:/Typora/Typora.exe" "source/_posts/Hexo 从入门到精通.md"
```

在 Typora 中写：

```markdown
---
title: Hexo 从入门到精通
date: 2026-02-24 14:30:00
tags: [Hexo, 博客, 教程]
categories: [技术教程, 博客搭建]
---

# Hexo 从入门到精通

## 什么是 Hexo？

Hexo 是一个快速、简洁且高效的博客框架...

## 安装 Hexo

```bash
npm install -g hexo-cli
```

## 创建博客

```bash
hexo init myblog
cd myblog
npm install
```
```

```bash
# 4. 本地预览
hexo server
# 访问 http://localhost:4000 检查效果

# 5. 确认无误后部署
hexo clean && hexo g -d

# 6. 备份源文件
git add source/_posts/"Hexo 从入门到精通.md"
git commit -m "添加文章：Hexo 从入门到精通"
git push
```

### 示例2：写一篇日记

```bash
# 一条命令完成
cd /e/MyBlog && \
hexo new "2026-02-24 日记" && \
"D:/Typora/Typora.exe" "source/_posts/2026-02-24 日记.md"
```

在 Typora 中写：

```markdown
---
title: 2026年2月24日 日记
date: 2026-02-24 22:30:00
tags: [日记, 生活]
categories: [生活随笔]
---

# 2026年2月24日 星期二 晴

## 今日完成

- ✅ 写了三篇技术文章
- ✅ 配置了 Wiki 站点
- ✅ 解决了 Git 冲突问题

## 学到的新知识

今天学会了 Docsify 的配置方法...

## 明日计划

- 写一篇关于 Docker 的文章
- 优化博客加载速度
```

---

## 十、常见问题

### 10.1 Q: 新建的文章找不到？

A: 检查以下位置：

```bash
# 查看 _posts 目录
ls -la source/_posts/

# 搜索文件
find source/_posts -name "*标题*"

# 检查 Hexo 是否识别
hexo list post
```

### 10.2 Q: 文章创建后不显示？

A: 可能原因及解决方法：

```bash
# 1. 日期是未来时间
cat source/_posts/文章.md | grep "date"

# 2. 头部格式错误
head -20 source/_posts/文章.md

# 3. 清理缓存
hexo clean
hexo generate
hexo server
```

### 10.3 Q: 标题包含特殊字符怎么办？

```bash
# 用引号括起来
hexo new "文章 & 教程"

# 或者用转义字符
hexo new "文章 \& 教程"
```

### 10.4 Q: 如何在 Typora 中粘贴图片？

A: Typora 支持直接拖拽图片，会自动复制到配置的目录。建议设置：

1. Typora → 文件 → 偏好设置
2. 图像 → 插入图片时 → 复制到 ./images 文件夹
3. 勾选"对本地图片应用上述规则"

### 10.5 Q: 文章发布后样式乱了？

A: 
```bash
# 检查 Markdown 语法
# 确保代码块正确闭合
# 检查标签配对

# 重新生成
hexo clean && hexo generate
hexo server
```

---

## 十一、快捷命令

### 11.1 常用命令速查

| 命令                      | 说明         |
| ------------------------- | ------------ |
| `hexo new "标题"`         | 新建文章     |
| `hexo new draft "标题"`   | 新建草稿     |
| `hexo publish "标题"`     | 发布草稿     |
| `hexo server`             | 本地预览     |
| `hexo clean`              | 清理缓存     |
| `hexo generate`           | 生成静态文件 |
| `hexo deploy`             | 部署上线     |
| `hexo clean && hexo g -d` | 一键部署     |

### 11.2 一键创建并打开

创建 `newpost.sh`：

```bash
#!/bin/bash
# 一键新建文章脚本

if [ -z "$1" ]; then
  echo "请输入文章标题"
  exit 1
fi

cd /e/MyBlog
hexo new "$1"
"D:/Typora/Typora.exe" "source/_posts/$1.md"
```

使用：
```bash
chmod +x newpost.sh
./newpost.sh "我的新文章"
```

### 11.3 批量创建脚本

```bash
#!/bin/bash
# 批量创建文章

titles=("文章1" "文章2" "文章3")

for title in "${titles[@]}"; do
  hexo new "$title"
done
```

---

## 十二、写作技巧

### 12.1 使用模板

编辑 `scaffolds/post.md`：

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

# {
  { title }}

## 简介

在这里写文章简介...

## 正文

### 第一部分

### 第二部分

## 总结

---

> 最后更新：{
  { date }}
```

### 12.2 写作流程

1. **构思** - 确定文章主题和结构
2. **创建** - `hexo new "标题"`
3. **写作** - 用 Typora 写内容
4. **预览** - `hexo server`
5. **修改** - 调整格式和内容
6. **部署** - `hexo clean && hexo g -d`
7. **备份** - `git add && git commit`

### 12.3 提高效率

- 使用 Typora 的快捷键
- 建立常用短语库
- 使用 Markdown 扩展语法
- 定期备份文章
- 分类管理标签

---

## 🔗 相关链接

- [Hexo 博客完全操作手册](/hexo-guide/)
- [文章头部格式详解](/hexo-guide/front-matter)
- [如何修改文章](/guides/edit-post)
- [如何删除文章](/guides/delete-post)
- [如何部署博客](/guides/deploy-blog)

---

## 📝 一句话总结

```bash
cd /e/MyBlog && hexo new "新文章" && "D:/Typora/Typora.exe" "source/_posts/新文章.md" && hexo server
```

写完文章后：
```bash
hexo clean && hexo g -d
```

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
>
> *祝你写作愉快！* 🚀