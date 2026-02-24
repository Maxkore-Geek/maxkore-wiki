好的！我来帮你创建完整的"如何部署博客"指南。

## 创建如何部署博客指南

```bash
# 进入 Wiki 目录
cd /e/maxkore-wiki

# 用 Typora 创建部署博客指南
"D:/Typora/Typora.exe" docs/guides/deploy-blog.md
```

在 Typora 中**复制粘贴**以下完整内容：

````markdown
# 🚀 如何部署博客

> 一步步教你将 Hexo 博客部署到 GitHub Pages
> **适用博客**：https://maxkore.bbroot.com

---

## 📖 快速导航

- [一、部署前准备](#一部署前准备)
- [二、一键部署（最简单）](#二一键部署最简单)
- [三、分步部署（推荐）](#三分步部署推荐)
- [四、手动 Git 部署](#四手动-git-部署)
- [五、部署后验证](#五部署后验证)
- [六、常见部署问题](#六常见部署问题)
- [七、自动化部署](#七自动化部署)
- [八、部署脚本](#八部署脚本)
- [九、多环境部署](#九多环境部署)
- [十、部署检查清单](#十部署检查清单)
- [十一、快速命令速查](#十一快速命令速查)

---

## 一、部署前准备

### 1.1 进入博客目录

```bash
# 打开 Git Bash，进入博客目录
cd /e/MyBlog

# 确认当前目录
pwd
# 应该显示：/e/MyBlog
```

### 1.2 检查文章状态

```bash
# 查看最近修改的文章
git status
ls -lt source/_posts/ | head -5
```

### 1.3 本地预览确认

```bash
# 启动本地预览
hexo server

# 访问 http://localhost:4000
# 检查所有修改是否正确
# 按 Ctrl+C 停止预览
```

### 1.4 部署前检查清单

- [ ] 所有文章格式正确
- [ ] 图片能正常显示
- [ ] 链接有效
- [ ] 标签和分类正确
- [ ] 本地预览效果满意
- [ ] CNAME 文件存在（自定义域名）

---

## 二、一键部署（最简单）

### 2.1 基本命令

```bash
# 清理缓存、生成静态文件、部署，一步完成
hexo clean && hexo g -d
```

### 2.2 命令说明

这条命令做了三件事：
1. **`hexo clean`** - 清理缓存文件
2. **`hexo generate`** - 生成静态文件（简写 `hexo g`）
3. **`hexo deploy`** - 部署到 GitHub（简写 `hexo d`）

### 2.3 执行示例

```bash
$ hexo clean && hexo g -d
INFO  Deleted database.
INFO  Deleted public folder.
INFO  Start processing
INFO  Files loaded in 238 ms
INFO  Generated: index.html
INFO  Generated: archives/index.html
INFO  Generated: tags/index.html
...
INFO  Deploy done: git
```

---

## 三、分步部署（推荐）

### 3.1 步骤1：清理缓存

```bash
# 清理之前生成的静态文件
hexo clean
```

**作用**：
- 删除 `public` 目录
- 删除数据库缓存
- 解决一些奇怪的问题

### 3.2 步骤2：生成静态文件

```bash
# 生成静态文件
hexo generate
# 或简写
hexo g
```

**作用**：
- 将 Markdown 文件转换为 HTML
- 生成到 `public` 目录
- 可以查看生成的静态文件

### 3.3 步骤3：本地预览（可选）

```bash
# 启动本地服务器查看效果
hexo server
# 或指定端口
hexo s -p 4001
```

访问 http://localhost:4000 检查效果，确认无误后按 `Ctrl+C` 停止。

### 3.4 步骤4：部署到 GitHub

```bash
# 部署到 GitHub Pages
hexo deploy
# 或简写
hexo d
```

### 3.5 完整分步流程

```bash
# 1. 清理
hexo clean

# 2. 生成
hexo generate

# 3. 预览（可选）
hexo server

# 4. 部署
hexo deploy
```

---

## 四、手动 Git 部署

### 4.1 什么时候需要手动部署？

- Hexo 部署失败时
- 需要直接操作 Git 时
- 想更清楚地看到部署过程

### 4.2 查看生成的文件

```bash
# 先正常生成静态文件
hexo clean
hexo generate

# 查看生成的 public 目录
ls -la public/
```

### 4.3 手动 Git 操作

```bash
# 进入 public 目录
cd public

# 初始化 Git 仓库（如果需要）
git init

# 添加所有文件
git add .

# 提交
git commit -m "部署博客 $(date +'%Y-%m-%d %H:%M')"

# 添加远程仓库
git remote add origin https://github.com/Maxkore-Geek/Maxkore-Geek.github.io.git

# 推送到 GitHub
git push -f origin master
```

### 4.4 返回博客目录

```bash
# 部署完成后返回博客目录
cd /e/MyBlog
```

---

## 五、部署后验证

### 5.1 等待部署

GitHub Pages 部署需要 2-5 分钟才能生效。

### 5.2 浏览器验证

访问以下地址：
- 主域名：https://maxkore.bbroot.com
- 备用：https://maxkore-geek.github.io

### 5.3 命令行验证

```bash
# 检查 HTTP 状态
curl -I https://maxkore.bbroot.com
# 应该返回 200 OK

# 检查特定页面
curl -I https://maxkore.bbroot.com/archives/
```

### 5.4 验证脚本

创建 `verify-deploy.sh`：

```bash
#!/bin/bash
# 部署验证脚本

URL="https://maxkore.bbroot.com"
echo "🔍 验证部署: $URL"

# 检查首页
status=$(curl -s -o /dev/null -w "%{http_code}" "$URL")
if [ "$status" = "200" ]; then
  echo "✅ 首页: $status OK"
else
  echo "❌ 首页: $status"
fi

# 检查最近文章
latest=$(curl -s "$URL" | grep -o '<a href="[^"]*">' | head -3)
echo "📄 最近文章:"
echo "$latest"

# 检查自定义域名
cname=$(curl -s -I "$URL" | grep -i "server" | head -1)
echo "🌐 服务器: $cname"
```

---

## 六、常见部署问题

### 6.1 问题1：部署后页面没更新

**现象**：访问网站还是旧内容

**原因**：
- GitHub Pages 缓存
- CDN 缓存
- 浏览器缓存

**解决方法**：

```bash
# 1. 等待 2-5 分钟
# 2. 强制刷新浏览器 (Ctrl+F5)
# 3. 用无痕模式访问
# 4. 重新部署一次
hexo clean && hexo g -d
```

### 6.2 问题2：部署失败 - 网络问题

**错误信息**：
```
fatal: unable to access '...': Recv failure: Connection was reset
```

**解决方法**：

```bash
# 方法1：重试
hexo clean && hexo g -d

# 方法2：手动 Git 推送
cd public
git push -f origin master

# 方法3：切换网络（换热点）
```

### 6.3 问题3：部署失败 - 权限问题

**错误信息**：
```
remote: Permission to ... denied
```

**解决方法**：

```bash
# 检查远程仓库地址
git remote -v

# 重新设置远程地址（使用 token）
git remote set-url origin https://用户名:token@github.com/用户名/仓库名.git
```

### 6.4 问题4：自定义域名失效

**现象**：部署后自定义域名被清空

**解决方法**：

```bash
# 检查 CNAME 文件
cat source/CNAME
# 应该显示：maxkore.bbroot.com

# 如果不存在，重新创建
echo -n "maxkore.bbroot.com" > source/CNAME

# 重新部署
hexo clean && hexo g -d
```

### 6.5 问题5：样式丢失

**现象**：页面显示正常，但没有样式

**解决方法**：

```bash
# 清理缓存重新生成
hexo clean
hexo generate

# 检查 public 目录
ls -la public/css/

# 重新部署
hexo deploy
```

### 6.6 问题6：404 错误

**现象**：访问页面显示 404

**解决方法**：

```bash
# 检查文件是否生成
ls -la public/文章路径/

# 重新生成
hexo clean && hexo generate

# 检查 GitHub Pages 设置
# https://github.com/Maxkore-Geek/Maxkore-Geek.github.io/settings/pages
```

---

## 七、自动化部署

### 7.1 使用 GitHub Actions

创建 `.github/workflows/deploy.yml`：

```yaml
name: Deploy Blog

on:
  push:
    branches:
      - master
    paths:
      - 'source/**'
      - '_config.yml'
      - 'themes/**'

jobs:
  deploy:
    runs-on: ubuntu-latest
    
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: |
          npm install
          npm install hexo-cli -g
      
      - name: Generate files
        run: |
          hexo clean
          hexo generate
      
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./public
          cname: maxkore.bbroot.com
```

### 7.2 使用 Git Hooks

创建 `.git/hooks/pre-push`：

```bash
#!/bin/bash
echo "🚀 推送前自动部署博客..."

cd /e/MyBlog
hexo clean && hexo g -d

if [ $? -eq 0 ]; then
  echo "✅ 部署成功"
else
  echo "❌ 部署失败"
  exit 1
fi
```

### 7.3 定时自动部署

创建 Windows 计划任务：

```bash
# 创建定时部署脚本 auto-deploy.bat
@echo off
cd /d E:\MyBlog
call hexo clean && hexo g -d
echo 部署完成：%date% %time% >> deploy.log
```

在计划任务中设置每天凌晨 3 点执行。

---

## 八、部署脚本

### 8.1 一键部署脚本

创建 `deploy.sh`：

```bash
#!/bin/bash
# 一键部署脚本

echo "🚀 ====================="
echo "🚀 开始部署博客"
echo "🚀 ====================="

# 进入博客目录
cd /e/MyBlog || exit 1

# 记录开始时间
start_time=$(date +%s)

# 步骤1：清理缓存
echo "📦 步骤1：清理缓存..."
hexo clean
if [ $? -ne 0 ]; then
  echo "❌ 清理失败"
  exit 1
fi

# 步骤2：生成静态文件
echo "📦 步骤2：生成静态文件..."
hexo generate
if [ $? -ne 0 ]; then
  echo "❌ 生成失败"
  exit 1
fi

# 步骤3：本地预览（可选）
echo "📦 步骤3：本地预览 (5秒)..."
hexo server &
SERVER_PID=$!
sleep 5
kill $SERVER_PID
echo "✅ 预览完成"

# 步骤4：部署
echo "📦 步骤4：部署到 GitHub..."
hexo deploy
if [ $? -ne 0 ]; then
  echo "❌ 部署失败"
  exit 1
fi

# 计算用时
end_time=$(date +%s)
duration=$((end_time - start_time))

echo "✅ ====================="
echo "✅ 部署完成！"
echo "✅ 用时: ${duration}秒"
echo "✅ 访问: https://maxkore.bbroot.com"
echo "✅ ====================="

# 打开浏览器
start https://maxkore.bbroot.com
```

### 8.2 带参数的高级脚本

创建 `deploy-advanced.sh`：

```bash
#!/bin/bash
# 高级部署脚本

# 颜色定义
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
NC='\033[0m' # No Color

# 显示帮助
show_help() {
  echo "使用方法: ./deploy-advanced.sh [选项]"
  echo "选项:"
  echo "  -h, --help     显示帮助"
  echo "  -c, --clean    强制清理"
  echo "  -p, --preview  预览模式（不部署）"
  echo "  -g, --git      同时提交到 Git"
  echo "  -f, --force    强制推送"
}

# 默认值
CLEAN=false
PREVIEW=false
GIT=false
FORCE=false

# 解析参数
while [[ $# -gt 0 ]]; do
  case $1 in
    -h|--help)
      show_help
      exit 0
      ;;
    -c|--clean)
      CLEAN=true
      shift
      ;;
    -p|--preview)
      PREVIEW=true
      shift
      ;;
    -g|--git)
      GIT=true
      shift
      ;;
    -f|--force)
      FORCE=true
      shift
      ;;
    *)
      echo "未知选项: $1"
      show_help
      exit 1
      ;;
  esac
done

echo -e "${GREEN}🚀 开始部署博客${NC}"

cd /e/MyBlog || exit 1

# 清理
if [ "$CLEAN" = true ]; then
  echo -e "${YELLOW}📦 强制清理缓存...${NC}"
  hexo clean
else
  echo -e "${YELLOW}📦 清理缓存...${NC}"
  hexo clean
fi

# 生成
echo -e "${YELLOW}📦 生成静态文件...${NC}"
hexo generate

# 预览模式
if [ "$PREVIEW" = true ]; then
  echo -e "${YELLOW}📦 预览模式，启动本地服务器...${NC}"
  hexo server
  exit 0
fi

# 部署
DEPLOY_CMD="hexo deploy"
if [ "$FORCE" = true ]; then
  DEPLOY_CMD="hexo deploy --force"
fi

echo -e "${YELLOW}📦 部署到 GitHub...${NC}"
$DEPLOY_CMD

if [ $? -eq 0 ]; then
  echo -e "${GREEN}✅ 部署成功！${NC}"
else
  echo -e "${RED}❌ 部署失败！${NC}"
  exit 1
fi

# Git 提交
if [ "$GIT" = true ]; then
  echo -e "${YELLOW}📦 提交到 Git...${NC}"
  git add .
  read -p "输入提交信息: " msg
  git commit -m "$msg"
  git push origin master
fi

echo -e "${GREEN}✅ 访问: https://maxkore.bbroot.com${NC}"
```

使用方式：
```bash
# 普通部署
./deploy-advanced.sh

# 强制清理并部署
./deploy-advanced.sh -c

# 预览模式
./deploy-advanced.sh -p

# 部署并提交 Git
./deploy-advanced.sh -g

# 强制推送
./deploy-advanced.sh -f
```

---

## 九、多环境部署

### 9.1 本地预览环境

```bash
# 本地开发环境
hexo server
# http://localhost:4000
```

### 9.2 测试环境

部署到 GitHub Pages 的分支：

```bash
# 修改 _config.yml
deploy:
  type: git
  repo: git@github.com:Maxkore-Geek/Maxkore-Geek.github.io.git
  branch: testing  # 使用 testing 分支
```

### 9.3 生产环境

```bash
# 正式部署
deploy:
  type: git
  repo: git@github.com:Maxkore-Geek/Maxkore-Geek.github.io.git
  branch: master
```

---

## 十、部署检查清单

### 10.1 部署前检查

- [ ] 所有文章已保存
- [ ] 本地预览正常
- [ ] 图片能显示
- [ ] 链接有效
- [ ] CNAME 文件存在
- [ ] _config.yml 配置正确
- [ ] 网络连接正常

### 10.2 部署中监控

- [ ] 清理缓存成功
- [ ] 生成文件成功
- [ ] 部署命令执行成功
- [ ] 没有错误提示

### 10.3 部署后验证

- [ ] 等待 2-5 分钟
- [ ] 首页能访问
- [ ] 新文章显示
- [ ] 样式正常
- [ ] 自定义域名生效
- [ ] HTTPS 正常

---

## 十一、快速命令速查

### 11.1 常用部署命令

| 命令 | 说明 | 使用场景 |
|------|------|----------|
| `hexo clean && hexo g -d` | 一键部署 | 日常使用 |
| `hexo clean` | 清理缓存 | 出问题时 |
| `hexo generate` | 生成文件 | 查看生成结果 |
| `hexo server` | 本地预览 | 写文章时 |
| `hexo deploy` | 仅部署 | 生成后单独部署 |

### 11.2 组合命令

```bash
# 最常用
hexo clean && hexo g -d

# 生成并预览
hexo g && hexo s

# 清理后预览
hexo clean && hexo g && hexo s

# 完整流程
hexo clean && hexo g && hexo s && hexo d
```

### 11.3 Git 相关命令

```bash
# 查看修改
git status

# 提交源文件
git add source/
git commit -m "更新博客"
git push

# 强制推送
git push -f origin master
```

---

## 📝 一句话总结

```bash
# 日常部署就用这一条命令
cd /e/MyBlog && hexo clean && hexo g -d
```

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
> 
> *部署博客就这么简单！* 🚀
````

保存文件（`Ctrl+S`），关闭 Typora。

## 更新侧边栏

```bash
# 编辑侧边栏确保有链接
"D:/Typora/Typora.exe" docs/_sidebar.md
```

确保在"使用指南"分类下有：

```markdown
**📖 使用指南**
* [如何新建文章](/guides/new-post)
* [如何修改文章](/guides/edit-post)
* [如何删除文章](/guides/delete-post)
* [如何部署博客](/guides/deploy-blog)
```

## 提交到 GitHub

```bash
# 添加文件
git add docs/guides/deploy-blog.md
git commit -m "Add deploy blog guide"
git push origin main
```

## 本地预览

```bash
docsify serve docs
```

访问 http://localhost:3000/#/guides/deploy-blog 查看效果。
