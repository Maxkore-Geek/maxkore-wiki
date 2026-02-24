# 🔄 Docs 重定向配置说明书

> 详细说明如何将 `https://maxkore.bbroot.com/docs/` 重定向到 `https://docs.bbroot.com/`
> **最后更新：2026年2月24日**

---

## 📖 目录

- [一、项目概述](#一项目概述)
- [二、重定向原理](#二重定向原理)
- [三、文件配置](#三文件配置)
- [四、部署步骤](#四部署步骤)
- [五、验证方法](#五验证方法)
- [六、故障排查](#六故障排查)
- [七、高级配置](#七高级配置)
- [八、维护指南](#八维护指南)
- [九、常见问题](#九常见问题)
- [十、相关链接](#十相关链接)

---

## 一、项目概述

### 1.1 基本信息

| 项目           | 信息                               |
| -------------- | ---------------------------------- |
| **源地址**     | `https://maxkore.bbroot.com/docs/` |
| **目标地址**   | `https://docs.bbroot.com/`         |
| **重定向类型** | 301/302 永久/临时重定向            |
| **实现方式**   | HTML meta refresh + JavaScript     |
| **所属项目**   | Maxkore 主博客                     |
| **本地路径**   | `E:/MyBlog/source/docs/`           |
| **创建时间**   | 2026年2月23日                      |
| **维护人**     | Maxkore                            |

### 1.2 项目背景

当访问主博客的 `/docs/` 路径时，需要自动跳转到独立的文档站。这样可以：
- 分离博客内容和文档内容
- 便于文档站的独立维护和升级
- 保持 URL 结构清晰

### 1.3 相关站点

| 站点       | 域名                            | 说明     |
| ---------- | ------------------------------- | -------- |
| **主博客** | https://maxkore.bbroot.com      | 源站点   |
| **文档站** | https://docs.bbroot.com         | 目标站点 |
| **GitHub** | https://github.com/Maxkore-Geek | 代码仓库 |

---

## 二、重定向原理

### 2.1 重定向方式

本项目使用两种重定向方式确保兼容性：

1. **Meta Refresh**（HTML 方式）
   ```html
   <meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">
   ```

2. **JavaScript 重定向**（备用）
   ```javascript
   window.location.replace("https://docs.bbroot.com/");
   ```

3. **规范链接**（SEO）
   ```html
   <link rel="canonical" href="https://docs.bbroot.com/">
   ```

### 2.2 重定向流程

```
用户访问
    ↓
https://maxkore.bbroot.com/docs/
    ↓
读取 /docs/index.html
    ↓
执行重定向
    ↓
https://docs.bbroot.com/
```

### 2.3 重定向类型说明

| 类型               | 说明             | 适用场景   |
| ------------------ | ---------------- | ---------- |
| **301 永久重定向** | 搜索引擎更新索引 | 永久迁移   |
| **302 临时重定向** | 保留原索引       | 临时调整   |
| **Meta Refresh**   | HTML 级重定向    | 兼容性最好 |
| **JavaScript**     | 客户端重定向     | 备用方案   |

---

## 三、文件配置

### 3.1 文件结构

```
E:/MyBlog/
├── source/
│   ├── docs/
│   │   ├── index.html    # 主重定向文件
│   │   └── 404.html      # 备用重定向文件
│   ├── _posts/           # 文章目录
│   └── CNAME             # 自定义域名
└── _config.yml           # 博客配置
```

### 3.2 index.html 完整代码

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>正在跳转到文档站...</title>
  
  <!-- Meta refresh 重定向 (0秒后跳转) -->
  <meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">
  
  <!-- 规范链接 (SEO) -->
  <link rel="canonical" href="https://docs.bbroot.com/">
  
  <!-- JavaScript 重定向 (备用) -->
  <script>
    // 立即执行重定向
    window.location.replace("https://docs.bbroot.com/");
    
    // 或者延迟2秒显示提示信息
    /*
    setTimeout(function() {
      window.location.replace("https://docs.bbroot.com/");
    }, 2000);
    */
  </script>
  
  <!-- 样式 (可选) -->
  <style>
    body {
      font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
      text-align: center;
      padding: 50px;
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      color: white;
      min-height: 100vh;
      margin: 0;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    .message {
      max-width: 600px;
      padding: 30px;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 10px;
      backdrop-filter: blur(10px);
      box-shadow: 0 20px 40px rgba(0,0,0,0.1);
    }
    h1 {
      font-size: 2.5em;
      margin-bottom: 20px;
    }
    p {
      font-size: 1.2em;
      margin-bottom: 30px;
      opacity: 0.9;
    }
    a {
      color: white;
      text-decoration: underline;
      opacity: 0.9;
    }
    a:hover {
      opacity: 1;
    }
    .loader {
      border: 3px solid rgba(255,255,255,0.3);
      border-radius: 50%;
      border-top: 3px solid white;
      width: 40px;
      height: 40px;
      animation: spin 1s linear infinite;
      margin: 20px auto;
    }
    @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
    }
  </style>
</head>
<body>
  <div class="message">
    <h1>🚀 正在跳转到文档站</h1>
    <p>您即将被重定向到 <strong>docs.bbroot.com</strong></p>
    <div class="loader"></div>
    <p>如果页面没有自动跳转，<a href="https://docs.bbroot.com/">请点击这里</a></p>
  </div>
  
  <!-- 备用的 noscript 方案 (当用户禁用JS时) -->
  <noscript>
    <meta http-equiv="refresh" content="2; url=https://docs.bbroot.com/">
    <div style="text-align:center; padding:50px;">
      <p>您的浏览器不支持 JavaScript，<a href="https://docs.bbroot.com/">点击此处访问文档站</a></p>
    </div>
  </noscript>
</body>
</html>
```

### 3.3 404.html 完整代码

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>页面不存在 - 正在跳转</title>
  <meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">
  <link rel="canonical" href="https://docs.bbroot.com/">
  <script>
    window.location.replace("https://docs.bbroot.com/");
  </script>
  <style>
    body {
      font-family: system-ui, -apple-system, sans-serif;
      text-align: center;
      padding: 50px;
      background: #f5f5f5;
    }
    .container {
      max-width: 600px;
      margin: 0 auto;
      padding: 40px;
      background: white;
      border-radius: 10px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    }
    h1 {
      color: #e74c3c;
      margin-bottom: 20px;
    }
    a {
      color: #3498db;
      text-decoration: none;
    }
    a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>🔍 页面不存在</h1>
    <p>您访问的页面不存在，正在跳转到文档站首页...</p>
    <p><a href="https://docs.bbroot.com/">立即前往 docs.bbroot.com</a></p>
  </div>
  <noscript>
    <meta http-equiv="refresh" content="2; url=https://docs.bbroot.com/">
  </noscript>
</body>
</html>
```

### 3.4 简化版本（无样式）

如果不需要样式，可以使用最简版本：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">
  <link rel="canonical" href="https://docs.bbroot.com/">
  <script>
    window.location.replace("https://docs.bbroot.com/");
  </script>
</head>
<body>
  <p>Redirecting to <a href="https://docs.bbroot.com/">docs.bbroot.com</a>...</p>
</body>
</html>
```

---

## 四、部署步骤

### 4.1 创建文件

```bash
# 进入博客目录
cd /e/MyBlog

# 创建 docs 目录
mkdir -p source/docs

# 创建 index.html
cat > source/docs/index.html << 'EOF'
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">
  <link rel="canonical" href="https://docs.bbroot.com/">
  <script>
    window.location.replace("https://docs.bbroot.com/");
  </script>
</head>
<body>
  <p>Redirecting to <a href="https://docs.bbroot.com/">docs.bbroot.com</a>...</p>
</body>
</html>
EOF

# 复制为 404.html
cp source/docs/index.html source/docs/404.html
```

### 4.2 使用 Typora 创建（推荐）

```bash
# 用 Typora 创建带样式的版本
"D:/Typora/Typora.exe" source/docs/index.html
# 粘贴上面的完整代码，保存

# 创建 404.html
"D:/Typora/Typora.exe" source/docs/404.html
# 粘贴上面的 404 代码，保存
```

### 4.3 验证文件

```bash
# 查看文件是否创建成功
ls -la source/docs/

# 查看文件内容
cat source/docs/index.html
```

### 4.4 Git 提交

```bash
# 添加文件到 Git
git add source/docs/

# 提交
git commit -m "Add redirect from /docs to docs.bbroot.com"

# 推送到 GitHub
git push origin master
```

### 4.5 Hexo 部署

```bash
# 清理缓存
hexo clean

# 生成静态文件
hexo generate

# 部署到 GitHub Pages
hexo deploy
```

### 4.6 一键完成所有步骤

```bash
# 创建文件并部署
cd /e/MyBlog && \
mkdir -p source/docs && \
cp /path/to/index.html source/docs/index.html && \
cp source/docs/index.html source/docs/404.html && \
git add source/docs/ && \
git commit -m "Add docs redirect" && \
git push origin master && \
hexo clean && hexo g -d
```

---

## 五、验证方法

### 5.1 本地验证

```bash
# 启动本地预览
hexo server

# 测试重定向
curl -I http://localhost:4000/docs/

# 应该返回 200 并包含重定向内容
```

### 5.2 线上验证

```bash
# 测试 HTTP 状态
curl -I https://maxkore.bbroot.com/docs/

# 应该返回 200 OK
# 并包含 Location 头
```

### 5.3 浏览器测试

访问以下 URL 测试：
- https://maxkore.bbroot.com/docs/
- https://maxkore.bbroot.com/docs/index.html
- https://maxkore.bbroot.com/docs/404.html
- https://maxkore.bbroot.com/docs/任意路径

都应该跳转到 https://docs.bbroot.com/

### 5.4 详细验证脚本

创建 `test-redirect.sh`：

```bash
#!/bin/bash
# 测试重定向脚本

URL="https://maxkore.bbroot.com/docs/"
TARGET="https://docs.bbroot.com/"

echo "🔍 测试重定向配置"
echo "=================="

# 测试 HTTP 状态
echo -n "HTTP 状态: "
status=$(curl -s -o /dev/null -w "%{http_code}" "$URL")
echo "$status"

# 测试重定向目标
echo -n "重定向目标: "
location=$(curl -s -I "$URL" | grep -i "location" | cut -d' ' -f2 | tr -d '\r')
echo "$location"

# 验证是否正确
if [[ "$location" == "$TARGET"* ]]; then
  echo "✅ 重定向配置正确"
else
  echo "❌ 重定向配置错误"
fi

# 测试直接访问文件
echo -e "\n测试直接访问文件:"
for file in index.html 404.html; do
  echo -n "$file: "
  curl -s -o /dev/null -w "%{http_code}" "https://maxkore.bbroot.com/docs/$file"
  echo ""
done
```

运行脚本：
```bash
chmod +x test-redirect.sh
./test-redirect.sh
```

### 5.5 在线工具验证

使用在线工具检查：
- https://httpstatus.io/
- https://www.redirect-checker.org/
- https://www.seoreviewtools.com/redirect-checker/

---

## 六、故障排查

### 6.1 常见问题速查表

| 问题                         | 可能原因        | 解决方法                 |
| ---------------------------- | --------------- | ------------------------ |
| **访问 /docs/ 显示 404**     | 文件不存在      | 检查 `source/docs/` 目录 |
| **访问 /docs/ 显示目录列表** | 缺少 index.html | 创建 index.html 文件     |
| **没有自动跳转**             | 重定向代码错误  | 检查 HTML 代码           |
| **跳转到错误地址**           | URL 写错        | 检查目标 URL             |
| **样式不显示**               | CSS 路径错误    | 检查内联样式             |

### 6.2 诊断命令

```bash
# 1. 检查文件是否存在
ls -la source/docs/

# 2. 检查文件内容
cat source/docs/index.html | grep "url="

# 3. 检查 Hexo 生成的文件
ls -la public/docs/

# 4. 检查 Git 状态
git status source/docs/

# 5. 测试线上文件
curl -I https://maxkore.bbroot.com/docs/index.html
```

### 6.3 修复步骤

**问题1：文件不存在**

```bash
# 重新创建文件
cd /e/MyBlog
mkdir -p source/docs
echo '<meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">' > source/docs/index.html
cp source/docs/index.html source/docs/404.html
```

**问题2：文件存在但不跳转**

```bash
# 检查并修复内容
"D:/Typora/Typora.exe" source/docs/index.html
# 确保包含正确的重定向代码

# 重新部署
hexo clean && hexo g -d
```

**问题3：部署后不生效**

```bash
# 清理缓存重新生成
hexo clean
hexo generate
hexo deploy

# 检查 public 目录
ls -la public/docs/
```

---

## 七、高级配置

### 7.1 保留路径重定向

如果需要将 `/docs/路径` 重定向到对应的文档路径：

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Redirecting...</title>
  <script>
    // 获取当前路径
    var path = window.location.pathname;
    
    // 去掉 /docs 前缀
    var newPath = path.replace(/^\/docs/, '');
    
    // 构建新 URL
    var newUrl = 'https://docs.bbroot.com' + newPath;
    
    // 跳转
    window.location.replace(newUrl);
  </script>
  <noscript>
    <meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">
  </noscript>
</head>
<body>
  <p>Redirecting to <a href="https://docs.bbroot.com/">docs.bbroot.com</a>...</p>
</body>
</html>
```

### 7.2 多语言支持

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Redirecting...</title>
  <script>
    // 根据浏览器语言跳转
    var lang = navigator.language || navigator.userLanguage;
    var targetUrl = 'https://docs.bbroot.com/';
    
    if (lang.startsWith('zh')) {
      targetUrl = 'https://docs.bbroot.com/zh/';
    } else if (lang.startsWith('en')) {
      targetUrl = 'https://docs.bbroot.com/en/';
    }
    
    window.location.replace(targetUrl);
  </script>
</head>
<body>
  <p>Redirecting...</p>
</body>
</html>
```

### 7.3 计数和统计

```html
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <title>Redirecting...</title>
  <script>
    // 发送统计请求
    fetch('https://analytics.example.com/redirect', {
      method: 'POST',
      body: JSON.stringify({
        url: window.location.href,
        referrer: document.referrer,
        timestamp: Date.now()
      })
    }).finally(() => {
      // 统计完成后跳转
      window.location.replace('https://docs.bbroot.com/');
    });
  </script>
  <noscript>
    <meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">
  </noscript>
</head>
<body>
  <p>Redirecting...</p>
</body>
</html>
```

### 7.5 备用方案

如果 HTML 方式不可用，可以在 Nginx 或 GitHub Pages 配置级别重定向：

**创建 `.htaccess` 文件**（仅 Apache 服务器）：
```apache
Redirect 301 /docs https://docs.bbroot.com/
```

**使用 GitHub Pages 的 404.html 技巧**：
```html
<!-- 在根目录的 404.html 中添加 -->
<script>
  if (window.location.pathname.startsWith('/docs')) {
    window.location.replace('https://docs.bbroot.com/' + window.location.pathname.replace('/docs', ''));
  }
</script>
```

---

## 八、维护指南

### 8.1 日常检查清单

- [ ] 每周测试一次重定向是否正常
- [ ] 检查目标网站 docs.bbroot.com 是否可访问
- [ ] 确认 HTTPS 证书有效
- [ ] 查看访问日志（如果有）

### 8.2 修改重定向目标

如果需要修改目标地址：

```bash
# 编辑文件
"D:/Typora/Typora.exe" source/docs/index.html

# 修改 url= 后面的地址
# 从 https://docs.bbroot.com/ 改为新地址

# 同步修改 404.html
cp source/docs/index.html source/docs/404.html

# 重新部署
hexo clean && hexo g -d
git add source/docs/
git commit -m "Update redirect target"
git push
```

### 8.3 备份配置

```bash
# 备份重定向文件
cp -r source/docs /e/博客备份/docs_$(date +%Y%m%d)

# 添加到 Git 备份
git add source/docs/
git commit -m "Backup redirect files"
git push
```

### 8.4 监控脚本

创建 `monitor-redirect.sh`：

```bash
#!/bin/bash
# 监控重定向状态

URL="https://maxkore.bbroot.com/docs/"
EXPECTED="https://docs.bbroot.com/"
LOG_FILE="/e/redirect_monitor.log"

echo "$(date): 开始监控..." >> "$LOG_FILE"

# 检查重定向
location=$(curl -s -I "$URL" | grep -i "location" | cut -d' ' -f2 | tr -d '\r')

if [[ "$location" == "$EXPECTED"* ]]; then
  echo "✅ 重定向正常: $location" >> "$LOG_FILE"
else
  echo "❌ 重定向异常: $location" >> "$LOG_FILE"
  
  # 发送通知
  # start mailto:admin@example.com?subject=重定向异常
fi

# 检查文件是否存在
status=$(curl -s -o /dev/null -w "%{http_code}" "$URL")
echo "HTTP状态: $status" >> "$LOG_FILE"
```

---

## 九、常见问题

### 9.1 Q: 为什么需要两个文件 (index.html 和 404.html)？

A: 
- `index.html` 处理正常访问 `/docs/`
- `404.html` 处理访问不存在的子路径，如 `/docs/abc`

### 9.2 Q: 重定向后 URL 会变化吗？

A: 会，从 `maxkore.bbroot.com/docs/` 变为 `docs.bbroot.com/`

### 9.3 Q: 对 SEO 有影响吗？

A: 
- 使用 `<link rel="canonical">` 告诉搜索引擎这是同一内容
- 建议使用 301 永久重定向，让搜索引擎更新索引

### 9.4 Q: 如何测试重定向是否生效？

A: 
```bash
curl -I https://maxkore.bbroot.com/docs/
```

### 9.5 Q: 重定向会影响原博客吗？

A: 不会，只影响 `/docs/` 路径，原博客其他页面正常访问

### 9.6 Q: 如何临时关闭重定向？

A: 
```bash
# 重命名或删除文件
mv source/docs/index.html source/docs/index.html.bak

# 重新部署
hexo clean && hexo g -d

# 恢复时改回来
mv source/docs/index.html.bak source/docs/index.html
```

### 9.7 Q: 重定向支持 HTTPS 吗？

A: 支持，重定向是客户端执行，与协议无关

### 9.8 Q: 用户禁用 JavaScript 怎么办？

A: 使用 `<noscript>` 和 `<meta refresh>` 作为备用

---

## 十、相关链接

### 10.1 文档站信息

| 项目           | 信息                                                         |
| -------------- | ------------------------------------------------------------ |
| **文档站域名** | https://docs.bbroot.com                                      |
| **文档站仓库** | [Maxkore-Geek/docs.bbroot.com](https://github.com/Maxkore-Geek/docs.bbroot.com) |
| **文档站类型** | Docsify / MkDocs                                             |
| **本地路径**   | `E:/docs.bbroot.com`                                         |

### 10.2 相关文档

- [博客维护说明书](/project/blog-maintenance)
- [Wiki 配置说明书](/project/wiki-setup)
- [Hexo 博客完全操作手册](/hexo-guide/)

### 10.3 参考资料

- [MDN: HTTP 重定向](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Redirections)
- [GitHub Pages 自定义域名](https://docs.github.com/cn/pages/configuring-a-custom-domain-for-your-github-pages-site)
- [HTML meta refresh](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/meta)

---

## 📝 快速命令速查

```bash
# 创建重定向文件
cd /e/MyBlog
mkdir -p source/docs
echo '<meta http-equiv="refresh" content="0; url=https://docs.bbroot.com/">' > source/docs/index.html
cp source/docs/index.html source/docs/404.html

# 部署
hexo clean && hexo g -d

# Git 提交
git add source/docs/
git commit -m "Add docs redirect"
git push

# 测试
curl -I https://maxkore.bbroot.com/docs/
```

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
>
> *如有问题，请在 GitHub 提交 Issue*