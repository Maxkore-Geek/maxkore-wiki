# 🌐 Maxkore Wiki 配置说明书

> 详细介绍 Maxkore Wiki 的搭建过程、配置方法和日常维护
> **最后更新：2026年2月24日**

---

## 📖 目录

- [一、项目概述](#一项目概述)
- [二、技术选型](#二技术选型)
- [三、环境搭建](#三环境搭建)
- [四、基础配置](#四基础配置)
- [五、内容管理](#五内容管理)
- [六、主题美化](#六主题美化)
- [七、插件配置](#七插件配置)
- [八、域名配置](#八域名配置)
- [九、部署配置](#九部署配置)
- [十、日常维护](#十日常维护)
- [十一、故障排查](#十一故障排查)
- [十二、备份策略](#十二备份策略)
- [十三、性能优化](#十三性能优化)
- [十四、SEO 配置](#十四seo-配置)
- [十五、常见问题](#十五常见问题)
- [十六、相关链接](#十六相关链接)

---

## 一、项目概述

### 1.1 基本信息

| 项目            | 信息                                                         |
| --------------- | ------------------------------------------------------------ |
| **Wiki 名称**   | Maxkore Wiki 知识库                                          |
| **Wiki 域名**   | https://maxkore-wiki.bbroot.com                              |
| **备用地址**    | https://maxkore-geek.github.io/maxkore-wiki/                 |
| **技术栈**      | Docsify                                                      |
| **本地路径**    | `E:/maxkore-wiki`                                            |
| **GitHub 仓库** | [Maxkore-Geek/maxkore-wiki](https://github.com/Maxkore-Geek/maxkore-wiki) |
| **创建时间**    | 2026年2月24日                                                |
| **维护人**      | Maxkore                                                      |

### 1.2 Wiki 结构

```
E:/maxkore-wiki/
├── docs/                      # 文档根目录
│   ├── index.html             # 入口文件
│   ├── README.md              # 首页内容
│   ├── _sidebar.md            # 侧边栏配置
│   ├── _navbar.md             # 导航栏配置（可选）
│   ├── _coverpage.md          # 封面页配置（可选）
│   ├── .nojekyll              # 禁用 Jekyll
│   ├── CNAME                  # 自定义域名
│   ├── python/                 # Python 笔记
│   │   └── 基础语法.md
│   ├── javascript/             # JavaScript 笔记
│   │   └── 基础语法.md
│   ├── linux/                  # Linux 笔记
│   │   ├── commands.md
│   │   └── docker.md
│   ├── tools/                  # 开发工具
│   │   ├── git.md
│   │   ├── vscode.md
│   │   └── markdown.md
│   ├── hexo-guide/             # 博客维护
│   │   ├── README.md
│   │   ├── front-matter.md
│   │   └── post-management.md
│   └── project/                # 项目文档
│       ├── blog-maintenance.md
│       ├── docs-redirect.md
│       └── wiki-setup.md
├── .github/
│   └── workflows/
│       └── deploy.yml          # GitHub Actions 部署配置
└── .gitignore                  # Git 忽略文件
```

### 1.3 功能特点

- ✅ **零配置** - 无需生成静态文件，直接渲染 Markdown
- ✅ **实时预览** - 修改 Markdown 即时生效
- ✅ **全文搜索** - 内置搜索功能
- ✅ **多主题** - 支持多种主题切换
- ✅ **插件丰富** - 支持代码高亮、流程图等
- ✅ **响应式** - 完美支持移动端
- ✅ **SEO友好** - 支持自定义 meta 信息

---

## 二、技术选型

### 2.1 为什么选择 Docsify？

| 特性         | Docsify     | Hexo   | MkDocs   | VuePress |
| ------------ | ----------- | ------ | -------- | -------- |
| **学习曲线** | 低          | 中     | 低       | 高       |
| **构建速度** | 无需构建    | 慢     | 中       | 慢       |
| **实时预览** | 原生支持    | 需重启 | 需重启   | 需重启   |
| **插件生态** | 丰富        | 丰富   | 一般     | 丰富     |
| **适合场景** | 知识库/文档 | 博客   | 项目文档 | 大型文档 |

### 2.2 核心优势

1. **无需构建** - 修改 Markdown 后刷新即生效
2. **轻量级** - 纯前端，加载速度快
3. **易部署** - 直接部署到 GitHub Pages
4. **易扩展** - 插件机制完善

---

## 三、环境搭建

### 3.1 安装 Docsify CLI

```bash
# 全局安装 docsify-cli
npm i -g docsify-cli

# 验证安装
docsify -v
```

### 3.2 初始化项目

```bash
# 创建项目目录
cd /e/
mkdir maxkore-wiki
cd maxkore-wiki

# 初始化 Docsify
docsify init ./docs
```

初始化后生成的文件：
```
docs/
  ├── index.html     # 入口文件
  ├── README.md      # 首页内容
  └── .nojekyll      # 禁用 Jekyll
```

### 3.3 本地预览

```bash
# 启动本地服务器
docsify serve docs

# 访问 http://localhost:3000
```

### 3.4 项目初始化脚本

创建 `init-wiki.sh`：

```bash
#!/bin/bash
# Wiki 初始化脚本

echo "🚀 开始初始化 Wiki..."

# 创建目录
mkdir -p docs/{python,javascript,linux,tools,hexo-guide,project,guides}

# 初始化 Docsify
docsify init ./docs

# 创建 .gitignore
cat > .gitignore << 'EOF'
# Node modules
node_modules/
npm-debug.log
package-lock.json

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
EOF

# 创建 README.md
cat > docs/README.md << 'EOF'
# 📚 Maxkore Wiki 知识库

> 记录技术、学习、生活的知识库

## 📖 快速开始

欢迎来到我的个人 Wiki！
EOF

echo "✅ Wiki 初始化完成！"
```

---

## 四、基础配置

### 4.1 index.html 完整配置

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <title>Maxkore Wiki</title>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="description" content="Maxkore 知识库 - 记录技术、学习、生活的知识库">
  <meta name="keywords" content="Maxkore, Wiki, 知识库, 技术笔记, 编程教程">
  <meta name="author" content="Maxkore">
  <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0" />
  
  <!-- 主题样式 -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css" />
  
  <!-- 代码高亮主题 -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/prismjs@1/themes/prism-tomorrow.css" />
  
  <!-- 字体图标 -->
  <link rel="stylesheet" href="//cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@5/css/all.min.css" />
</head>
<body>
  <div id="app"></div>
  
  <script>
    window.$docsify = {
      // 基础配置
      name: '📚 Maxkore Wiki',
      repo: 'https://github.com/Maxkore-Geek/maxkore-wiki',
      basePath: '/',
      
      // 路由配置
      route: {
        '/': 'README.md',
        '/python/': 'python/README.md',
        '/javascript/': 'javascript/README.md',
      },
      
      // 侧边栏配置
      loadSidebar: true,
      subMaxLevel: 3,
      sidebarDisplayLevel: 1,
      
      // 导航栏配置
      loadNavbar: true,
      
      // 封面配置
      coverpage: true,
      
      // 搜索配置
      search: {
        maxAge: 86400000, // 1天
        paths: 'auto',
        placeholder: '搜索文档...',
        noData: '没有结果',
        depth: 3
      },
      
      // 代码高亮
      prism: ['bash', 'javascript', 'python', 'yaml', 'json', 'markdown'],
      
      // 自动编号
      autoHeader: true,
      
      // 复制代码
      copyCode: {
        buttonText: '复制',
        errorText: '错误',
        successText: '已复制'
      },
      
      // 分页配置
      pagination: {
        previousText: '上一页',
        nextText: '下一页',
        crossChapter: true
      },
      
      // 字数统计
      count: {
        countable: true,
        fontsize: '0.9em',
        color: 'rgb(90,90,90)',
        language: 'chinese'
      },
      
      // 更新时间
      formatUpdated: '{YYYY}/{MM}/{DD} {HH}:{mm}',
      
      // 图片缩放
      zoom: true,
      
      // 表情符号
      emoji: true,
      
      // 外部链接
      externalLinkTarget: '_blank',
      
      // 主题切换
      themeable: {
        readyTransition: true,
        themes: [
          { name: '默认', value: '//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css' },
          { name: '暗色', value: '//cdn.jsdelivr.net/npm/docsify@4/lib/themes/dark.css' },
          { name: '极简', value: '//cdn.jsdelivr.net/npm/docsify@4/lib/themes/buble.css' }
        ]
      }
    }
  </script>
  
  <!-- 加载 Docsify -->
  <script src="//cdn.jsdelivr.net/npm/docsify@4"></script>
  
  <!-- 加载插件 -->
  <script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify-copy-code"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify-pagination/dist/docsify-pagination.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify-count/dist/countable.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify-zoom-image"></script>
  <script src="//cdn.jsdelivr.net/npm/docsify-emoj"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-bash.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-python.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-javascript.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-yaml.min.js"></script>
  <script src="//cdn.jsdelivr.net/npm/prismjs@1/components/prism-json.min.js"></script>
</body>
</html>
```

### 4.2 首页配置 (README.md)

```markdown
# 📚 Maxkore Wiki 知识库

> 记录技术、学习、生活的知识库
> 最后更新：2026年2月24日

---

## 📖 快速开始

欢迎来到我的个人 Wiki！这里记录了我学习过程中的笔记、心得和总结。

### 📋 主要分类

#### 💻 **编程技术**
- [Python 笔记](/python/基础语法) - Python 基础语法、进阶技巧
- [JavaScript 笔记](/javascript/基础语法) - JS 核心概念、ES6+ 特性

#### 🐧 **Linux/运维**
- [Linux 命令速查](/linux/commands) - 常用命令汇总
- [Docker 使用](/linux/docker) - 容器化部署指南

#### 🔧 **开发工具**
- [Git 教程](/tools/git) - 版本控制必知必会
- [VSCode 配置](/tools/vscode) - 编辑器优化技巧
- [Markdown 语法](/tools/markdown) - 写作必备

#### 📝 **博客维护**
- [Hexo 博客完全操作手册](/hexo-guide/) - 日常写作指南
- [文章头部格式详解](/hexo-guide/front-matter) - Front-matter 说明
- [文章管理指南](/hexo-guide/post-management) - 新建/修改/删除

#### 📚 **项目文档**
- [博客维护说明书](/project/blog-maintenance) - Maxkore 博客维护
- [Docs 重定向说明书](/project/docs-redirect) - 文档站配置
- [Wiki 配置说明书](/project/wiki-setup) - 本 Wiki 搭建指南

#### 📖 **使用指南**
- [如何新建文章](/guides/new-post) - 一步步教你写博客
- [如何修改文章](/guides/edit-post) - 更新已有内容
- [如何删除文章](/guides/delete-post) - 移除不需要的文章
- [如何部署博客](/guides/deploy-blog) - 一键发布

---

## 🌐 **其他站点**

| 站点 | 地址 | 说明 |
|------|------|------|
| 🏠 **主博客** | [https://maxkore.bbroot.com](https://maxkore.bbroot.com) | 技术文章、学习笔记 |
| 📄 **文档站** | [https://docs.bbroot.com](https://docs.bbroot.com) | 项目文档、API 参考 |
| 📚 **本 Wiki** | [https://maxkore-wiki.bbroot.com](https://maxkore-wiki.bbroot.com) | 知识库、操作手册 |

---

## 🔍 **快速链接**

- [📝 写新文章](/guides/new-post)
- [🚀 部署博客](/guides/deploy-blog)
- [❓ 常见问题](/hexo-guide/error-solutions)
- [📊 站点状态](https://github.com/Maxkore-Geek)

---

## 📌 **最近更新**

- [2026-02-24] 添加 Hexo 博客完全操作手册
- [2026-02-24] 完善 Wiki 首页布局
- [2026-02-23] 初始化 Wiki 知识库

---

> **最后更新**：2026年2月24日  
> **维护人**：Maxkore  
> [GitHub](https://github.com/Maxkore-Geek) | [博客](https://maxkore.bbroot.com)
```

### 4.3 侧边栏配置 (_sidebar.md)

```markdown
* [📚 首页](/)

**💻 编程技术**
* [Python 笔记](/python/基础语法)
* [JavaScript 笔记](/javascript/基础语法)

**🐧 Linux/运维**
* [Linux 命令速查](/linux/commands)
* [Docker 使用](/linux/docker)

**🔧 开发工具**
* [Git 教程](/tools/git)
* [VSCode 配置](/tools/vscode)
* [Markdown 语法](/tools/markdown)

**📝 博客维护**
* [Hexo 博客完全操作手册](/hexo-guide/)
* [文章头部格式详解](/hexo-guide/front-matter)
* [文章管理指南](/hexo-guide/post-management)

**📚 项目文档**
* [博客维护说明书](/project/blog-maintenance)
* [Docs 重定向说明书](/project/docs-redirect)
* [Wiki 配置说明书](/project/wiki-setup)

**📖 使用指南**
* [如何新建文章](/guides/new-post)
* [如何修改文章](/guides/edit-post)
* [如何删除文章](/guides/delete-post)
* [如何部署博客](/guides/deploy-blog)

**🔗 快速链接**
* [📝 写新文章](/guides/new-post)
* [🚀 部署博客](/guides/deploy-blog)
* [❓ 常见问题](/hexo-guide/error-solutions)
* [📊 站点状态](https://github.com/Maxkore-Geek)
```

### 4.4 导航栏配置 (_navbar.md)

```markdown
* [🏠 首页](/)
* [📝 博客](https://maxkore.bbroot.com)
* [📄 文档](https://docs.bbroot.com)
* [📚 Wiki](/)
* [🐱 GitHub](https://github.com/Maxkore-Geek)
```

### 4.5 封面配置 (_coverpage.md)

```markdown
# 📚 Maxkore Wiki
> 记录技术、学习、生活的知识库

- 编程技术
- Linux/运维
- 开发工具
- 博客维护

[GitHub](https://github.com/Maxkore-Geek)
[开始阅读](/README.md)
```

---

## 五、内容管理

### 5.1 创建新文档

```bash
# 创建新文档
touch docs/分类/文档名.md

# 用 Typora 编辑
"D:/Typora/Typora.exe" docs/分类/文档名.md
```

### 5.2 文档模板

创建 `template.md`：

```markdown
---
title: 文档标题
date: 2026-02-24
tags: [标签1, 标签2]
---

# 文档标题

> 文档描述

## 简介

在这里写简介...

## 正文

### 小节1

内容...

### 小节2

内容...

## 总结

总结要点...

---

> 最后更新：2026年2月24日
```

### 5.3 批量创建文档

```bash
# 批量创建文档
for name in "入门" "进阶" "高级"; do
  touch "docs/python/$name.md"
done
```

### 5.4 文档组织规范

```
docs/
├── 分类1/
│   ├── README.md        # 分类首页
│   ├── 主题1.md
│   └── 主题2.md
├── 分类2/
│   ├── README.md
│   └── 主题.md
└── ...
```

---

## 六、主题美化

### 6.1 主题切换

在 `index.html` 中配置主题：

```javascript
window.$docsify = {
  // 主题配置
  themeable: {
    themes: [
      { name: 'vue', value: '//cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css' },
      { name: 'dark', value: '//cdn.jsdelivr.net/npm/docsify@4/lib/themes/dark.css' },
      { name: 'buble', value: '//cdn.jsdelivr.net/npm/docsify@4/lib/themes/buble.css' }
    ]
  }
}
```

### 6.2 自定义 CSS

创建 `docs/custom.css`：

```css
:root {
  --theme-color: #42b983;
  --text-color: #34495e;
  --bg-color: #fff;
  --code-bg-color: #f8f8f8;
}

/* 自定义样式 */
.sidebar {
  background: linear-gradient(180deg, #f8f9fa 0%, #e9ecef 100%);
}

.markdown-section h1 {
  color: var(--theme-color);
  border-bottom: 2px solid var(--theme-color);
}

.markdown-section code {
  background: var(--code-bg-color);
  border-radius: 3px;
}
```

在 `index.html` 中引入：

```html
<link rel="stylesheet" href="custom.css" />
```

### 6.3 暗色主题适配

```css
/* 暗色主题 */
@media (prefers-color-scheme: dark) {
  :root {
    --text-color: #eee;
    --bg-color: #1e1e1e;
    --code-bg-color: #2d2d2d;
  }
}
```

---

## 七、插件配置

### 7.1 常用插件

| 插件           | 说明     | 引入方式                                                     |
| -------------- | -------- | ------------------------------------------------------------ |
| **search**     | 全文搜索 | `<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>` |
| **copy-code**  | 复制代码 | `<script src="//cdn.jsdelivr.net/npm/docsify-copy-code"></script>` |
| **pagination** | 分页导航 | `<script src="//cdn.jsdelivr.net/npm/docsify-pagination/dist/docsify-pagination.min.js"></script>` |
| **count**      | 字数统计 | `<script src="//cdn.jsdelivr.net/npm/docsify-count/dist/countable.min.js"></script>` |
| **zoom-image** | 图片缩放 | `<script src="//cdn.jsdelivr.net/npm/docsify-zoom-image"></script>` |
| **emoji**      | 表情支持 | `<script src="//cdn.jsdelivr.net/npm/docsify-emoj"></script>` |
| **tabs**       | 标签页   | `<script src="//cdn.jsdelivr.net/npm/docsify-tabs@1"></script>` |
| **chart**      | 图表     | `<script src="//cdn.jsdelivr.net/npm/docsify-chart"></script>` |
| **mermaid**    | 流程图   | `<script src="//cdn.jsdelivr.net/npm/docsify-mermaid@1"></script>` |

### 7.2 插件配置示例

```javascript
window.$docsify = {
  // 搜索配置
  search: {
    maxAge: 86400000,
    paths: 'auto',
    placeholder: '搜索文档...',
    noData: '没有结果',
    depth: 3
  },
  
  // 代码复制
  copyCode: {
    buttonText: '复制',
    errorText: '错误',
    successText: '已复制'
  },
  
  // 分页
  pagination: {
    previousText: '上一页',
    nextText: '下一页',
    crossChapter: true
  },
  
  // 字数统计
  count: {
    countable: true,
    fontsize: '0.9em',
    color: 'rgb(90,90,90)',
    language: 'chinese'
  },
  
  // 标签页
  tabs: {
    persist: true,
    sync: true,
    theme: 'classic'
  },
  
  // Mermaid 流程图
  mermaid: {
    theme: 'default'
  }
}
```

---

## 八、域名配置

### 8.1 创建 CNAME 文件

```bash
# 创建 CNAME 文件
echo "maxkore-wiki.bbroot.com" > docs/CNAME

# 验证
cat docs/CNAME
```

### 8.2 DNS 配置

在 DNSHe 后台添加 A 记录：

| 记录类型 | 主机记录     | 记录值          | TTL  |
| -------- | ------------ | --------------- | ---- |
| A        | maxkore-wiki | 185.199.108.153 | 600  |
| A        | maxkore-wiki | 185.199.109.153 | 600  |
| A        | maxkore-wiki | 185.199.110.153 | 600  |
| A        | maxkore-wiki | 185.199.111.153 | 600  |

### 8.3 验证 DNS

```bash
# 测试 DNS 解析
nslookup maxkore-wiki.bbroot.com 8.8.8.8

# 应该返回四个 IP
```

### 8.4 GitHub Pages 设置

1. 访问 https://github.com/Maxkore-Geek/maxkore-wiki/settings/pages
2. **Custom domain** 输入：`maxkore-wiki.bbroot.com`
3. 点击 **Save**
4. 等待 DNS 检查通过
5. 勾选 **Enforce HTTPS**

---

## 九、部署配置

### 9.1 GitHub Actions 自动部署

创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy Wiki to GitHub Pages

on:
  push:
    branches:
      - main
      - master
    paths:
      - 'docs/**'
      - '.github/workflows/**'

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./docs
          publish_branch: gh-pages
          cname: maxkore-wiki.bbroot.com
```

### 9.2 手动部署

```bash
# 本地预览
docsify serve docs

# 提交到 GitHub
git add .
git commit -m "更新 Wiki"
git push origin main
```

### 9.3 部署脚本

创建 `deploy.sh`：

```bash
#!/bin/bash
# 一键部署脚本

echo "🚀 开始部署 Wiki..."

# 检查是否有未提交的更改
if [[ -n $(git status -s) ]]; then
  echo "📦 提交更改..."
  git add .
  git commit -m "自动部署: $(date +'%Y-%m-%d %H:%M:%S')"
fi

# 推送到 GitHub
echo "☁️ 推送到 GitHub..."
git push origin main

# 等待部署
echo "⏳ 等待 GitHub Actions 部署..."
sleep 5

# 打开网站
start https://maxkore-wiki.bbroot.com

echo "✅ 部署完成！"
```

---

## 十、日常维护

### 10.1 每日维护

```bash
# 本地预览
docsify serve docs

# 检查新内容
git status
```

### 10.2 每周维护

```bash
# 更新内容
git add .
git commit -m "每周更新: $(date +'%Y-%m-%d')"
git push

# 检查 GitHub Actions 状态
# https://github.com/Maxkore-Geek/maxkore-wiki/actions
```

### 10.3 维护脚本

创建 `maintain.sh`：

```bash
#!/bin/bash
# Wiki 维护脚本

echo "🔧 Wiki 维护工具"
echo "================"
echo "1. 检查更新"
echo "2. 本地预览"
echo "3. 提交更改"
echo "4. 检查链接"
echo "5. 备份"
echo "================"
read -p "请选择 [1-5]: " choice

case $choice in
  1)
    git status
    git log --oneline -5
    ;;
  2)
    docsify serve docs
    ;;
  3)
    git add .
    read -p "提交信息: " msg
    git commit -m "$msg"
    git push
    ;;
  4)
    # 检查死链
    grep -r "](" docs/ | grep -v "http" | while read line; do
      file=$(echo $line | cut -d: -f1)
      link=$(echo $line | grep -o ']([^)]*)' | cut -d'(' -f2 | cut -d')' -f1)
      if [[ ! -f "docs/$link" ]] && [[ ! -f "docs/$link.md" ]]; then
        echo "死链: $file -> $link"
      fi
    done
    ;;
  5)
    tar -czf "wiki_backup_$(date +%Y%m%d).tar.gz" docs/
    echo "✅ 备份完成"
    ;;
esac
```

---

## 十一、故障排查

### 11.1 常见问题

| 问题             | 可能原因            | 解决方法             |
| ---------------- | ------------------- | -------------------- |
| **404 错误**     | 文件不存在          | 检查路径和文件名     |
| **样式丢失**     | CDN 问题            | 更换 CDN 源          |
| **搜索不工作**   | 插件未加载          | 检查 search 插件配置 |
| **侧边栏不显示** | _sidebar.md 错误    | 检查文件格式         |
| **部署失败**     | GitHub Actions 错误 | 查看 Actions 日志    |

### 11.2 诊断命令

```bash
# 检查文件
ls -la docs/

# 检查配置
cat docs/index.html | grep "window.$docsify"

# 检查侧边栏
cat docs/_sidebar.md

# 检查 Git 状态
git status

# 本地预览测试
docsify serve docs
```

### 11.3 修复步骤

**问题：404 错误**

```bash
# 检查文件是否存在
find docs -name "文件名.md"

# 检查链接格式
grep -r "](链接)" docs/
```

**问题：侧边栏不显示**

```bash
# 检查文件编码
file docs/_sidebar.md

# 重新创建
echo "* [首页](README.md)" > docs/_sidebar.md
```

**问题：部署失败**

```bash
# 强制推送
git push -f origin main

# 手动触发 Actions
# GitHub 仓库 → Actions → Deploy Wiki → Run workflow
```

---

## 十二、备份策略

### 12.1 本地备份

```bash
# 完整备份
tar -czf wiki_backup_$(date +%Y%m%d).tar.gz docs/

# 增量备份
cp -r docs docs_backup_$(date +%Y%m%d)
```

### 12.2 Git 备份

```bash
# 提交到 Git
git add .
git commit -m "备份: $(date +'%Y-%m-%d')"
git push
```

### 12.3 自动备份脚本

创建 `auto-backup.sh`：

```bash
#!/bin/bash
# 自动备份脚本

BACKUP_DIR="/e/博客备份/wiki"
DATE=$(date +%Y%m%d_%H%M%S)

# 创建备份目录
mkdir -p "$BACKUP_DIR"

# 备份
tar -czf "$BACKUP_DIR/wiki_$DATE.tar.gz" \
  --exclude="node_modules" \
  --exclude=".git" \
  docs/

# 删除30天前的备份
find "$BACKUP_DIR" -name "*.tar.gz" -mtime +30 -delete

echo "✅ 备份完成: wiki_$DATE.tar.gz"
```

---

## 十三、性能优化

### 13.1 加载速度优化

```html
<!-- 使用本地资源 -->
<link rel="stylesheet" href="/lib/docsify/vue.css" />

<!-- 预加载 -->
<link rel="preload" href="//cdn.jsdelivr.net/npm/docsify@4" as="script" />
```

### 13.2 图片优化

```markdown
<!-- 使用 WebP 格式 -->
![图片](image.webp)

<!-- 懒加载 -->
<img data-src="image.jpg" class="lazyload" />
```

### 13.3 缓存优化

```javascript
window.$docsify = {
  // 启用缓存
  cache: true,
  
  // 设置缓存时间
  maxAge: 86400000
}
```

---

## 十四、SEO 配置

### 14.1 Meta 信息

```html
<head>
  <title>Maxkore Wiki - 技术知识库</title>
  <meta name="description" content="Maxkore 的技术笔记和知识库">
  <meta name="keywords" content="编程, Linux, Docker, Git, VSCode">
  <meta name="author" content="Maxkore">
  
  <!-- Open Graph -->
  <meta property="og:title" content="Maxkore Wiki">
  <meta property="og:description" content="技术知识库">
  <meta property="og:url" content="https://maxkore-wiki.bbroot.com">
  
  <!-- Twitter Card -->
  <meta name="twitter:card" content="summary">
  <meta name="twitter:title" content="Maxkore Wiki">
</head>
```

### 14.2 站点地图

创建 `sitemap.xml`：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
  <url>
    <loc>https://maxkore-wiki.bbroot.com/</loc>
    <lastmod>2026-02-24</lastmod>
    <changefreq>weekly</changefreq>
    <priority>1.0</priority>
  </url>
</urlset>
```

### 14.3 robots.txt

```txt
User-agent: *
Allow: /
Sitemap: https://maxkore-wiki.bbroot.com/sitemap.xml
```

---

## 十五、常见问题

### 15.1 Q: 如何添加新分类？

A: 
```bash
# 创建分类目录
mkdir -p docs/新分类

# 创建侧边栏链接
echo "* [新分类](/新分类/)" >> docs/_sidebar.md
```

### 15.2 Q: 如何修改主题颜色？

A: 在 `custom.css` 中修改：
```css
:root {
  --theme-color: #你的颜色;
}
```

### 15.3 Q: 如何添加搜索功能？

A: 在 `index.html` 中添加：
```html
<script src="//cdn.jsdelivr.net/npm/docsify/lib/plugins/search.min.js"></script>
```

### 15.4 Q: 如何支持数学公式？

A: 
```html
<!-- 添加插件 -->
<script src="//cdn.jsdelivr.net/npm/docsify-katex@1"></script>
```

### 15.5 Q: 如何添加评论系统？

A: 使用 Gitalk 或 Disqus：
```html
<script src="//cdn.jsdelivr.net/npm/docsify-gitalk@1"></script>
<script>
window.$docsify = {
  gitalk: {
    clientID: '你的ID',
    clientSecret: '你的密钥',
    repo: 'maxkore-wiki',
    owner: 'Maxkore-Geek',
    admin: ['Maxkore-Geek']
  }
}
</script>
```

---

## 十六、相关链接

### 16.1 官方文档

- [Docsify 官方文档](https://docsify.js.org/)
- [Docsify GitHub](https://github.com/docsifyjs/docsify/)
- [Docsify 插件列表](https://docsify.js.org/#/plugins)

### 16.2 相关项目

- [Maxkore 博客](https://maxkore.bbroot.com)
- [Maxkore Docs](https://docs.bbroot.com)
- [GitHub 仓库](https://github.com/Maxkore-Geek/maxkore-wiki)

### 16.3 工具推荐

| 工具           | 用途            |
| -------------- | --------------- |
| Typora         | Markdown 编辑器 |
| VS Code        | 代码编辑器      |
| Git Bash       | 命令行工具      |
| GitHub Desktop | Git 客户端      |

---

## 📝 快速命令速查

```bash
# 本地预览
docsify serve docs

# 创建新文档
touch docs/分类/文档.md

# 提交更改
git add .
git commit -m "更新"
git push

# 检查状态
git status

# 查看日志
git log --oneline -10
```

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
>
> *如有问题，请在 GitHub 提交 Issue*