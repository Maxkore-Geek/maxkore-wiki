# 📝 Hexo 博客完全操作手册

> 基于 Maxkore 亲身经历的完整总结
> 涵盖日常操作、Git 工作流、各类报错解决方案

## 📋 一、博客日常操作（标准流程）

### 1.1 写新文章
```bash
# 进入博客目录
cd /e/MyBlog

# 创建新文章（标题可以用中文）
hexo new "文章标题"

# 编辑文章（用 Typora/VS Code/记事本）
notepad source/_posts/文章标题.md
    **文章头部格式示例**：
	```yaml
	---
	title: 文章标题
	date: 2026-02-23 13:26:02
	tags: [标签1, 标签2]
	categories: [分类名]
	---

### 文章头部格式详解

每篇文章开头都需要有 YAML 格式的 Front-matter，用 `---` 包裹：

```yaml
---
title: 文章标题          # 必填，文章标题
date: 2026-02-23 13:26:02  # 必填，创建时间
updated: 2026-02-24 10:30:00 # 可选，更新时间
tags: [标签1, 标签2]     # 可选，标签
categories: [分类名]      # 可选，分类
permalink: custom-url    # 可选，自定义链接
comments: true          # 可选，是否开启评论
---
