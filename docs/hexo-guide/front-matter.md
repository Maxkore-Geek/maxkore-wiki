# 📄 文章头部格式详解 (Front-matter)

> Front-matter 是文件开头的 YAML 配置块，用 `---` 包裹，用于定义文章的元数据。
> 它是 Hexo 博客的核心配置，控制文章的各种属性和显示方式。

---

## 📖 目录

- [一、什么是 Front-matter](#一什么是-front-matter)
- [二、基本格式](#二基本格式)
- [三、完整字段说明](#三完整字段说明)
- [四、字段详解](#四字段详解)
- [五、各种格式示例](#五各种格式示例)
- [六、注意事项](#六注意事项)
- [七、在文章中使用](#七在文章中使用)
- [八、常见问题](#八常见问题)
- [九、进阶用法](#九进阶用法)

---

## 一、什么是 Front-matter

Front-matter 是文章开头的一段特殊配置，用三个短横线 `---` 包裹，里面是 YAML 格式的键值对。

```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
tags: [标签1, 标签2]
categories: [分类1, 分类2]
---
```

## 二、基本格式

### 最简单的格式
```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
---
```

### 常用格式
```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
tags:
  - 标签1
  - 标签2
categories:
  - 分类1
  - 分类2
---
```

### 完整格式
```yaml
---
title: 文章标题
date: 2026-02-24 14:30:00
updated: 2026-02-24 16:30:00
tags: [标签1, 标签2]
categories: [分类1, 分类2]
keywords: [关键词1, 关键词2]
description: 这是一篇关于某某的文章
comments: true
toc: true
top: 1
cover: /images/cover.jpg
permalink: /custom-url/
password: 123456
abstract: 这是一篇加密文章
---
```

---

## 三、完整字段说明

| 字段          | 必填 | 类型   | 说明           | 示例                           |
| ------------- | ---- | ------ | -------------- | ------------------------------ |
| `title`       | ✅    | 字符串 | 文章标题       | `title: Hello World`           |
| `date`        | ✅    | 日期   | 创建时间       | `date: 2026-02-24 14:30:00`    |
| `updated`     | ❌    | 日期   | 更新时间       | `updated: 2026-02-25 10:00:00` |
| `tags`        | ❌    | 数组   | 文章标签       | `tags: [Hexo, 博客]`           |
| `categories`  | ❌    | 数组   | 文章分类       | `categories: [技术, 教程]`     |
| `keywords`    | ❌    | 数组   | SEO 关键词     | `keywords: [hexo, blog]`       |
| `description` | ❌    | 字符串 | 文章描述       | `description: 这是一篇教程`    |
| `comments`    | ❌    | 布尔值 | 是否开启评论   | `comments: true`               |
| `toc`         | ❌    | 布尔值 | 是否显示目录   | `toc: true`                    |
| `top`         | ❌    | 数字   | 置顶优先级     | `top: 1`                       |
| `cover`       | ❌    | 字符串 | 封面图片       | `cover: /images/cover.jpg`     |
| `permalink`   | ❌    | 字符串 | 自定义链接     | `permalink: /my-post/`         |
| `password`    | ❌    | 字符串 | 文章密码       | `password: 123456`             |
| `abstract`    | ❌    | 字符串 | 密码提示       | `abstract: 输入密码查看`       |
| `layout`      | ❌    | 字符串 | 布局模板       | `layout: post`                 |
| `sticky`      | ❌    | 数字   | 置顶（同 top） | `sticky: 1`                    |
| `thumbnail`   | ❌    | 字符串 | 缩略图         | `thumbnail: /images/thumb.jpg` |
| `photos`      | ❌    | 数组   | 图片集         | `photos: [img1.jpg, img2.jpg]` |
| `copyright`   | ❌    | 布尔值 | 显示版权       | `copyright: true`              |
| `reward`      | ❌    | 布尔值 | 开启打赏       | `reward: true`                 |
| `mathjax`     | ❌    | 布尔值 | 开启数学公式   | `mathjax: true`                |
| `mermaid`     | ❌    | 布尔值 | 开启流程图     | `mermaid: true`                |
| `indexing`    | ❌    | 布尔值 | 是否索引       | `indexing: true`               |

---

## 四、字段详解

### 4.1 标题 (title)

文章标题，会显示在页面标题、文章列表和浏览器标签上。

```yaml
title: 从零开始搭建个人博客
title: "Hexo 博客 & 完全操作手册"  # 包含特殊字符时用引号
```

### 4.2 日期 (date / updated)

- `date`：创建时间，必填
- `updated`：更新时间，可选

```yaml
date: 2026-02-24 14:30:00
updated: 2026-02-25 09:15:00
```

支持的日期格式：
```yaml
date: 2026-02-24 14:30:00
date: 2026-02-24
date: 2026/02/24 14:30:00
date: 2026-02-24T14:30:00.000Z
```

### 4.3 标签 (tags)

标签用于文章分类，一篇文章可以有多个标签。

**数组格式（推荐）**：
```yaml
tags:
  - Hexo
  - GitHub Pages
  - 博客搭建
```

**行内格式**：
```yaml
tags: [Hexo, GitHub Pages, 博客搭建]
```

### 4.4 分类 (categories)

分类用于文章归档，支持多级分类。

**单级分类**：
```yaml
categories:
  - 技术教程
```

**多级分类**：
```yaml
categories:
  - 技术
  - 前端
  - Hexo
```

**行内格式**：
```yaml
categories: [技术, 前端, Hexo]
```

### 4.5 SEO 相关

```yaml
# 关键词（用于搜索引擎优化）
keywords: [Hexo, 博客搭建, GitHub Pages, 教程]

# 文章描述（会显示在搜索结果中）
description: 本文详细介绍如何使用 Hexo 和 GitHub Pages 搭建个人博客，从零开始手把手教学。
```

### 4.6 文章显示控制

```yaml
# 开启评论（默认 true）
comments: true

# 显示目录（默认 false）
toc: true

# 目录深度（配合 toc 使用）
toc_max_depth: 3

# 置顶（数字越大越靠前）
top: 1

# 或使用 sticky（效果相同）
sticky: 1
```

### 4.7 图片相关

```yaml
# 封面图（显示在文章列表）
cover: /images/cover.jpg

# 缩略图
thumbnail: /images/thumbnail.jpg

# 图片集
photos:
  - /images/photo1.jpg
  - /images/photo2.jpg
  - /images/photo3.jpg
```

### 4.8 自定义链接

```yaml
# 自定义永久链接（不设置则使用默认格式）
permalink: /hello-world/

# 或使用变量
permalink: /post/:title/
```

### 4.9 加密文章

```yaml
# 设置密码（访问时需要输入）
password: 123456

# 密码提示（显示在密码框上方）
abstract: 这是一篇加密文章，请输入密码查看。

# 错误提示（密码错误时显示）
message: 密码错误，请重新输入。
```

### 4.10 功能开关

```yaml
# 开启数学公式支持（需要插件）
mathjax: true

# 开启流程图支持（需要插件）
mermaid: true

# 显示版权信息
copyright: true

# 开启打赏功能
reward: true

# 是否被搜索引擎索引
indexing: true
```

---

## 五、各种格式示例

### 5.1 基础示例

最简单的文章配置：

```yaml
---
title: Hello World
date: 2026-02-24 14:30:00
---
```

### 5.2 标准博客文章

```yaml
---
title: 从零开始搭建个人博客
date: 2026-02-24 14:30:00
updated: 2026-02-25 10:00:00
tags: 
  - Hexo
  - GitHub Pages
  - 教程
categories:
  - 技术教程
  - 博客搭建
keywords: [hexo, github pages, 博客, 搭建]
description: 手把手教你用 Hexo + GitHub Pages 搭建免费个人博客
comments: true
toc: true
cover: /images/hexo-cover.jpg
---
```

### 5.3 置顶文章

```yaml
---
title: 重要公告
date: 2026-02-24 14:30:00
top: 1  # 数字越大越靠前
sticky: 1  # 或者用 sticky
tags: [公告]
categories: [站务]
---
```

### 5.4 加密文章

```yaml
---
title: 私密笔记
date: 2026-02-24 14:30:00
tags: [私密, 笔记]
categories: [个人]
password: mysecret123
abstract: 这是一篇私人笔记，请输入密码查看。
message: 密码错误，请重试。
---
```

### 5.5 技术教程（带数学公式）

```yaml
---
title: 机器学习入门
date: 2026-02-24 14:30:00
tags: [机器学习, AI, Python]
categories: [技术教程]
mathjax: true  # 开启数学公式
toc: true
toc_max_depth: 4
---
```

### 5.6 图片集文章

```yaml
---
title: 旅行日记
date: 2026-02-24 14:30:00
tags: [旅行, 摄影]
categories: [生活]
photos:
  - /images/trip/photo1.jpg
  - /images/trip/photo2.jpg
  - /images/trip/photo3.jpg
  - /images/trip/photo4.jpg
---
```

### 5.7 完整示例

```yaml
---
title: Hexo 博客完全操作手册
date: 2026-02-24 14:30:00
updated: 2026-02-25 16:45:00
tags: 
  - Hexo
  - GitHub Pages
  - 博客
  - 教程
categories:
  - 技术教程
  - 博客搭建
  - 工具使用
keywords: [hexo, github pages, 博客搭建, 教程, 操作手册]
description: 最全面的 Hexo 博客操作手册，涵盖日常写作、Git工作流、错误解决等
comments: true
toc: true
toc_max_depth: 3
top: 1
cover: /images/hexo-manual-cover.jpg
copyright: true
reward: true
mathjax: false
---
```

---

## 六、注意事项

### 6.1 格式要求

#### ✅ 正确格式
```yaml
---
title: 文章标题      # ✅ 冒号后有空格
tags: 
  - 标签1          # ✅ 缩进一致
  - 标签2
categories: [分类]  # ✅ 行内格式
---
```

#### ❌ 错误格式
```yaml
---
title:文章标题       # ❌ 冒号后没空格
tags:
- 标签1            # ❌ 缩进错误
  - 标签2          # ❌ 缩进不一致
categories: [分类   # ❌ 括号没闭合
---
```

### 6.2 常见错误

| 错误类型       | 错误示例                    | 正确写法                      |
| -------------- | --------------------------- | ----------------------------- |
| 冒号后无空格   | `title:标题`                | `title: 标题`                 |
| 缩进不一致     | `tags:\n- 标签1\n  - 标签2` | `tags:\n  - 标签1\n  - 标签2` |
| 特殊字符未转义 | `title: Hello & World`      | `title: "Hello & World"`      |
| 日期格式错误   | `date: 2026.02.24`          | `date: 2026-02-24`            |
| 数组格式错误   | `tags: 标签1, 标签2`        | `tags: [标签1, 标签2]`        |

### 6.3 特殊字符处理

当标题或内容包含特殊字符时，需要用引号括起来：

```yaml
# 包含冒号
title: "Hexo: 博客搭建指南"

# 包含 & 符号
title: "Hexo & GitHub Pages"

# 包含引号
title: "他说：\"Hello World\""
```

### 6.4 编码问题

- 使用 UTF-8 编码
- 避免使用中文标点
- 文件保存为 UTF-8 without BOM

---

## 七、在文章中使用

### 7.1 完整文章示例

```markdown
---
title: 我的第一篇文章
date: 2026-02-24 14:30:00
updated: 2026-02-24 16:20:00
tags: [测试, 入门]
categories: [技术, 教程]
keywords: [第一篇, 测试文章]
description: 这是我的第一篇博客文章
comments: true
toc: true
---

# 我的第一篇文章

## 介绍

这是文章正文内容...

## 正文

这里是详细内容...

## 总结

感谢阅读！
```

### 7.2 查看 Front-matter

```bash
# 查看文章头部
head -20 source/_posts/文章标题.md

# 提取 Front-matter
sed -n '/^---$/,/^---$/p' source/_posts/文章标题.md
```

---

## 八、常见问题

### 8.1 Q: Front-matter 可以留空吗？

A: 可以，但至少要有 `title` 和 `date` 字段。

### 8.2 Q: 可以自定义字段吗？

A: 可以，主题或插件可能支持自定义字段，也可以自己添加。

### 8.3 Q: 如何批量修改 Front-matter？

A: 可以使用脚本或编辑器批量替换：

```bash
# 为所有文章添加默认分类
for file in source/_posts/*.md; do
  sed -i '/^---$/a categories: [未分类]' "$file"
done
```

### 8.4 Q: Front-matter 中的日期时区问题？

A: 在 `_config.yml` 中设置时区：
```yaml
timezone: Asia/Shanghai
```

### 8.5 Q: 如何验证 Front-matter 格式？

A: 使用在线 YAML 验证器，或本地预览：
```bash
hexo server --debug
```

---

## 九、进阶用法

### 9.1 使用变量

```yaml
---
title: 文章标题
date: { { date }}
tags: { { tags }}
categories: { { categories }}
---
```

### 9.2 条件判断

某些主题支持条件判断：

```yaml
---
title: 文章标题
toc: { { page.toc | default(true) }}
---
```

### 9.3 继承模板

```yaml
---
layout: custom
title: 文章标题
---
```

### 9.4 多语言支持

```yaml
---
title: 
  zh-CN: 中文标题
  en: English Title
date: 2026-02-24 14:30:00
---
```

### 9.5 自定义脚本

```yaml
---
title: 文章标题
scripts:
  - /js/custom.js
styles:
  - /css/custom.css
---
```

---

## 📝 速查表

### 最常用字段
```yaml
title:      # 标题
date:       # 日期
tags:       # 标签
categories: # 分类
updated:    # 更新时间
comments:   # 评论
toc:        # 目录
top:        # 置顶
cover:      # 封面
```

### 一行搞定
```yaml
---
title: Hello World
date: 2026-02-24 14:30:00
tags: [Hexo, 博客]
categories: [技术]
---
```

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
>
> *本文档会持续更新，欢迎收藏！*