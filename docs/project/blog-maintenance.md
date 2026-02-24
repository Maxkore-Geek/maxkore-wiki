# 🔧 Maxkore 博客维护说明书

> 全面的博客维护指南，涵盖日常维护、故障排查、性能优化等
> **最后更新：2026年2月24日**

---

## 📖 目录

- [一、博客基本信息](#一博客基本信息)
- [二、日常维护清单](#二日常维护清单)
- [三、环境维护](#三环境维护)
- [四、内容维护](#四内容维护)
- [五、域名维护](#五域名维护)
- [六、性能优化](#六性能优化)
- [七、安全维护](#七安全维护)
- [八、备份策略](#八备份策略)
- [九、监控和日志](#九监控和日志)
- [十、故障排查](#十故障排查)
- [十一、维护脚本](#十一维护脚本)
- [十二、维护计划](#十二维护计划)
- [十三、紧急预案](#十三紧急预案)
- [十四、维护记录](#十四维护记录)

---

## 一、博客基本信息

### 1.1 博客概览

| 项目            | 信息                                                         |
| --------------- | ------------------------------------------------------------ |
| **博客名称**    | Maxkore的博客                                                |
| **主域名**      | https://maxkore.bbroot.com                                   |
| **备用域名**    | https://maxkore-geek.github.io                               |
| **博客类型**    | Hexo + NexT.Muse                                             |
| **本地路径**    | `E:/MyBlog`                                                  |
| **GitHub 仓库** | [Maxkore-Geek/Maxkore-Geek.github.io](https://github.com/Maxkore-Geek/Maxkore-Geek.github.io) |
| **主题**        | NexT.Muse v7.8.0                                             |
| **创建时间**    | 2026年2月                                                    |
| **维护人**      | Maxkore                                                      |

### 1.2 相关站点

| 站点       | 域名                            | 说明     |
| ---------- | ------------------------------- | -------- |
| **主博客** | https://maxkore.bbroot.com      | 技术博客 |
| **文档站** | https://docs.bbroot.com         | 项目文档 |
| **Wiki**   | https://maxkore-wiki.bbroot.com | 知识库   |
| **GitHub** | https://github.com/Maxkore-Geek | 代码仓库 |

### 1.3 目录结构

```
E:/MyBlog/
├── _config.yml              # 主配置文件
├── package.json             # 依赖管理
├── node_modules/            # 依赖模块
├── scaffolds/               # 文章模板
│   ├── post.md              # 文章模板
│   ├── draft.md             # 草稿模板
│   └── page.md              # 页面模板
├── source/                  # 源文件（核心）
│   ├── _posts/              # 文章目录
│   ├── _drafts/             # 草稿目录
│   ├── about/               # 关于页面
│   ├── tags/                # 标签页面
│   ├── categories/          # 分类页面
│   ├── CNAME                # 自定义域名
│   ├── images/              # 图片资源
│   └── docs/                 # 重定向配置
├── themes/                   # 主题
│   └── next/                 # NexT 主题
│       ├── _config.yml       # 主题配置
│       ├── layout/           # 布局文件
│       ├── source/           # 主题资源
│       └── languages/        # 语言文件
├── public/                   # 生成的静态文件
├── .deploy_git/              # 部署临时文件
└── .git/                     # Git 仓库
```

---

## 二、日常维护清单

### 2.1 每日检查

- [ ] 博客是否正常访问（https://maxkore.bbroot.com）
- [ ] HTTPS 证书是否有效
- [ ] 新文章是否正常显示
- [ ] 评论功能是否正常
- [ ] 页面加载速度是否正常

### 2.2 每周维护

- [ ] 写新文章并发布
- [ ] 检查并回复评论
- [ ] 更新文章标签和分类
- [ ] 备份 source 目录
- [ ] 检查 GitHub Actions 构建状态

### 2.3 每月维护

- [ ] 检查域名续期状态
- [ ] 更新 Hexo 和插件版本
- [ ] 清理无用文件和草稿
- [ ] 检查死链
- [ ] 优化图片大小
- [ ] 检查 SEO 状态
- [ ] 查看 Google Analytics 数据

### 2.4 每季度维护

- [ ] 全面检查配置文件
- [ ] 更新主题版本
- [ ] 重构文章分类
- [ ] 检查并更新友情链接
- [ ] 生成站点地图
- [ ] 提交搜索引擎更新

### 2.5 年度维护

- [ ] 更换头像（可选）
- [ ] 更新关于页面
- [ ] 整理归档文章
- [ ] 检查所有外部链接
- [ ] 生成年度总结
- [ ] 备份完整项目

---

## 三、环境维护

### 3.1 Node.js 环境

```bash
# 检查 Node.js 版本
node -v
# 要求：v12.0.0 以上，推荐 v18.x

# 检查 npm 版本
npm -v

# 更新 npm
npm install -g npm@latest
```

### 3.2 Hexo 版本管理

```bash
# 查看 Hexo 版本
hexo version

# 更新 Hexo
npm update hexo -g

# 查看过时的插件
npm outdated

# 更新所有插件
npm update

# 安装新插件
npm install --save 插件名
```

### 3.3 依赖包维护

```bash
# 检查 package.json
cat package.json

# 重新安装依赖
rm -rf node_modules
npm install

# 修复漏洞
npm audit fix
```

### 3.4 主题维护

```bash
# 进入主题目录
cd themes/next

# 更新主题
git pull origin master

# 查看主题版本
cat package.json | grep version
```

---

## 四、内容维护

### 4.1 文章质量检查

```bash
# 检查文章数量
ls source/_posts/ | wc -l

# 检查最近更新的文章
ls -lt source/_posts/ | head -10

# 检查没有标签的文章
grep -L "tags:" source/_posts/*.md

# 检查没有分类的文章
grep -L "categories:" source/_posts/*.md
```

### 4.2 图片管理

```bash
# 检查图片目录
ls -la source/images/

# 统计图片数量
find source/images -type f | wc -l

# 查找大图片（超过1MB）
find source/images -size +1M

# 优化图片（需要安装 imagemin）
npx imagemin source/images/* --out-dir source/images/optimized
```

### 4.3 标签和分类优化

```bash
# 统计标签使用频率
grep -h "^tags:" source/_posts/*.md | \
  sed 's/tags: \[//' | sed 's/\]//' | \
  tr ',' '\n' | sort | uniq -c | sort -nr

# 统计分类使用频率
grep -h "^categories:" source/_posts/*.md | \
  sed 's/categories: \[//' | sed 's/\]//' | \
  tr ',' '\n' | sort | uniq -c | sort -nr
```

### 4.4 死链检查

```bash
# 检查内部死链
grep -r "](/.*)" source/_posts/ | \
  sed 's/.*](\([^)]*\)).*/\1/' | \
  while read link; do
    if [[ ! -f "source/$link" ]] && [[ ! -f "public/$link" ]]; then
      echo "死链: $link"
    fi
  done
```

### 4.5 文章归档

```bash
# 按年份归档
mkdir -p source/_posts/archive/2025
mv source/_posts/2025-*.md source/_posts/archive/2025/

# 创建归档页面
hexo new page "archive-2025"
```

---

## 五、域名维护

### 5.1 域名信息

| 项目           | 信息                 |
| -------------- | -------------------- |
| **主域名**     | maxkore.bbroot.com   |
| **注册商**     | DNSHe                |
| **到期时间**   | 2036年（10年有效期） |
| **DNS 服务器** | 默认 DNSHe 服务器    |

### 5.2 DNS 记录检查

```bash
# 检查 A 记录
nslookup maxkore.bbroot.com 8.8.8.8

# 应该返回：
# 185.199.108.153
# 185.199.109.153
# 185.199.110.153
# 185.199.111.153

# 检查 CNAME 记录
nslookup -type=CNAME www.maxkore.bbroot.com 8.8.8.8
```

### 5.3 HTTPS 证书检查

```bash
# 检查证书有效期
curl -vI https://maxkore.bbroot.com 2>&1 | grep "expire date"

# 或使用 openssl
echo | openssl s_client -servername maxkore.bbroot.com -connect maxkore.bbroot.com:443 2>/dev/null | openssl x509 -noout -dates
```

### 5.4 域名续期

DNSHe 免费域名有效期为10年，但仍需注意：

```bash
# 登录 DNSHe 后台检查到期时间
# 访问：https://my.dnshe.com

# 设置提醒（每月1日检查）
# 在 Windows 计划任务中添加：
# 名称：DNSHe 域名检查
# 触发器：每月1日 09:00
# 操作：start https://my.dnshe.com
```

---

## 六、性能优化

### 6.1 加载速度优化

```bash
# 生成静态文件并查看大小
hexo clean && hexo generate
du -sh public/

# 压缩 HTML
npm install hexo-neat --save-dev
```

在 `_config.yml` 中添加：

```yaml
# 压缩优化
neat:
  html:
    enable: true
    exclude:
  css:
    enable: true
    exclude:
      - '*.min.css'
  js:
    enable: true
    mangle: true
    exclude:
      - '*.min.js'
```

### 6.2 图片优化

```yaml
# 在 _config.yml 中配置
# 使用 hexo-images 插件
npm install hexo-images --save

# 配置
images:
  enable: true
  quality: 80
  webp: true
```

### 6.3 缓存优化

```bash
# 启用 CDN
# 在主题配置中启用
cdn:
  enable: true
  provider: unpkg
```

### 6.4 性能测试

```bash
# 使用 Lighthouse 测试
# Chrome 开发者工具 → Lighthouse

# 使用命令行工具
npm install -g lighthouse
lighthouse https://maxkore.bbroot.com --view
```

---

## 七、安全维护

### 7.1 配置文件安全

```bash
# 检查敏感信息
grep -r "password\|token\|key" _config.yml themes/next/_config.yml

# 确保 .gitignore 包含敏感文件
cat .gitignore
# 应包含：
# .env
# config.local.yml
# *.log
```

### 7.2 依赖安全

```bash
# 检查漏洞
npm audit

# 修复漏洞
npm audit fix

# 查看安全建议
npm audit --json
```

### 7.3 访问安全

```bash
# 确保 HTTPS 强制开启
# 在 GitHub Pages 设置中勾选 "Enforce HTTPS"

# 检查 CAA 记录
dig CAA maxkore.bbroot.com
```

### 7.4 备份安全

```bash
# 加密敏感备份
gpg -c backup.tar.gz  # 加密
gpg backup.tar.gz.gpg  # 解密
```

---

## 八、备份策略

### 8.1 备份内容

| 备份项   | 路径                      | 频率     | 重要性 |
| -------- | ------------------------- | -------- | ------ |
| 文章     | `source/_posts/`          | 每次更新 | ⭐⭐⭐    |
| 配置     | `_config.yml`             | 每次修改 | ⭐⭐⭐    |
| 主题配置 | `themes/next/_config.yml` | 每月     | ⭐⭐     |
| 图片     | `source/images/`          | 每月     | ⭐⭐     |
| 完整项目 | 整个目录                  | 每季度   | ⭐      |

### 8.2 自动备份脚本

创建 `auto-backup.sh`：

```bash
#!/bin/bash
# 自动备份脚本

# 配置
BACKUP_DIR="/e/博客备份"
BLOG_DIR="/e/MyBlog"
DATE=$(date +%Y%m%d_%H%M%S)
RETENTION_DAYS=30

# 创建备份目录
mkdir -p "$BACKUP_DIR"/{daily,weekly,monthly}

# 备份文章
echo "📁 备份文章中..."
tar -czf "$BACKUP_DIR/daily/posts_$DATE.tar.gz" \
  -C "$BLOG_DIR" source/_posts

# 备份配置文件
echo "⚙️ 备份配置中..."
cp "$BLOG_DIR/_config.yml" "$BACKUP_DIR/daily/config_$DATE.yml"
cp "$BLOG_DIR/themes/next/_config.yml" "$BACKUP_DIR/daily/theme_config_$DATE.yml"

# 备份完整项目（每周日执行）
if [ $(date +%u) -eq 7 ]; then
  echo "📦 每周完整备份..."
  tar -czf "$BACKUP_DIR/weekly/full_$DATE.tar.gz" \
    --exclude="node_modules" \
    --exclude=".git" \
    --exclude="public" \
    --exclude=".deploy_git" \
    -C "$BLOG_DIR" .
fi

# 每月1日执行月备份
if [ $(date +%d) -eq 1 ]; then
  echo "📅 每月完整备份..."
  cp -r "$BLOG_DIR" "$BACKUP_DIR/monthly/blog_$DATE"
fi

# 清理旧备份
find "$BACKUP_DIR/daily" -type f -mtime +$RETENTION_DAYS -delete
find "$BACKUP_DIR/weekly" -type f -mtime +90 -delete

echo "✅ 备份完成！"
```

### 8.3 恢复步骤

```bash
# 恢复文章
tar -xzf posts_20260224.tar.gz -C /e/MyBlog/source/

# 恢复配置
cp config_20260224.yml /e/MyBlog/_config.yml

# 恢复完整项目
tar -xzf full_20260224.tar.gz -C /e/MyBlog/
npm install  # 重新安装依赖
```

---

## 九、监控和日志

### 9.1 本地日志

```bash
# 查看 Hexo 日志
hexo server --debug

# 查看部署日志
hexo deploy --debug

# 查看 Git 日志
git log --oneline -20
```

### 9.2 GitHub Actions 监控

```bash
# 访问 Actions 页面
# https://github.com/Maxkore-Geek/Maxkore-Geek.github.io/actions

# 使用 API 检查状态
curl -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/Maxkore-Geek/Maxkore-Geek.github.io/actions/workflows
```

### 9.3 访问监控

使用 Google Analytics 或 Cloudflare Analytics：

```bash
# 在主题配置中启用
google_analytics:
  tracking_id: UA-XXXXX-Y
```

### 9.4 监控脚本

创建 `monitor.sh`：

```bash
#!/bin/bash
# 博客监控脚本

BLOG_URL="https://maxkore.bbroot.com"
LOG_FILE="/e/blog_monitor.log"

echo "$(date): 开始监控..." >> "$LOG_FILE"

# 检查网站是否可访问
if curl -s -o /dev/null -w "%{http_code}" "$BLOG_URL" | grep -q "200"; then
  echo "✅ 网站正常" >> "$LOG_FILE"
else
  echo "❌ 网站异常！" >> "$LOG_FILE"
  
  # 发送通知（可以使用邮件、短信等）
  # start mailto:admin@example.com?subject=博客异常
fi

# 检查 HTTPS 证书
expiry_date=$(echo | openssl s_client -servername maxkore.bbroot.com -connect maxkore.bbroot.com:443 2>/dev/null | openssl x509 -noout -enddate | cut -d= -f2)
echo "证书到期: $expiry_date" >> "$LOG_FILE"

# 检查 GitHub Pages 状态
curl -s https://www.githubstatus.com/api/v2/status.json | grep -q "operational"
if [ $? -eq 0 ]; then
  echo "✅ GitHub Pages 正常" >> "$LOG_FILE"
else
  echo "⚠️ GitHub Pages 可能有问题" >> "$LOG_FILE"
fi
```

---

## 十、故障排查

### 10.1 常见问题速查表

| 问题             | 可能原因            | 解决方法                |
| ---------------- | ------------------- | ----------------------- |
| **网站 404**     | GitHub Pages 未更新 | 等待2-5分钟，重新部署   |
| **样式丢失**     | 缓存问题            | `hexo clean` 重新生成   |
| **文章不显示**   | Front-matter 错误   | 检查日期和格式          |
| **部署失败**     | 网络问题            | 重试或手动 Git 推送     |
| **域名失效**     | CNAME 文件丢失      | 重新创建 `source/CNAME` |
| **HTTPS 警告**   | 证书未颁发          | 等待15-30分钟           |
| **评论无法使用** | 配置错误            | 检查评论插件配置        |

### 10.2 诊断命令

```bash
# 1. 检查本地环境
node -v
npm -v
hexo version

# 2. 检查配置文件
cat _config.yml | grep -v "^#" | head -20

# 3. 检查生成的文件
ls -la public/

# 4. 检查 Git 状态
git status

# 5. 检查远程仓库
git remote -v

# 6. 测试部署
hexo clean && hexo g -d --debug
```

### 10.3 紧急恢复步骤

**场景1：网站完全无法访问**

```bash
# 1. 检查 GitHub Pages 设置
# 访问 https://github.com/Maxkore-Geek/Maxkore-Geek.github.io/settings/pages

# 2. 重新部署
cd /e/MyBlog
hexo clean && hexo g -d

# 3. 检查 CNAME 文件
cat source/CNAME
echo -n "maxkore.bbroot.com" > source/CNAME
git add source/CNAME
git commit -m "紧急修复 CNAME"
git push

# 4. 等待5分钟
```

**场景2：文章发布后不显示**

```bash
# 1. 检查文章日期
head -20 source/_posts/文章标题.md | grep "date"

# 2. 清理缓存
hexo clean

# 3. 重新生成
hexo generate

# 4. 本地预览
hexo server

# 5. 重新部署
hexo deploy
```

**场景3：域名被清空**

```bash
# 1. 重新创建 CNAME
echo -n "maxkore.bbroot.com" > source/CNAME

# 2. 提交到 Git
git add source/CNAME
git commit -m "紧急恢复 CNAME"
git push

# 3. 在 GitHub 重新设置
# Settings → Pages → Custom domain → maxkore.bbroot.com → Save

# 4. 等待 HTTPS 重新颁发
```

---

## 十一、维护脚本

### 11.1 一键维护脚本

创建 `maintain.sh`：

```bash
#!/bin/bash
# 博客一键维护脚本

echo "🔧 Maxkore 博客维护工具"
echo "========================"
echo "1. 完整检查"
echo "2. 清理并优化"
echo "3. 备份"
echo "4. 更新依赖"
echo "5. 退出"
echo "========================"
read -p "请选择 [1-5]: " choice

case $choice in
  1)
    echo "🔍 开始完整检查..."
    
    # 检查 Node.js
    echo "Node.js: $(node -v)"
    
    # 检查 Hexo
    echo "Hexo: $(hexo version | head -1)"
    
    # 检查文章数量
    count=$(ls source/_posts/*.md 2>/dev/null | wc -l)
    echo "文章数量: $count"
    
    # 检查 CNAME
    if [ -f source/CNAME ]; then
      echo "CNAME: $(cat source/CNAME)"
    else
      echo "⚠️ CNAME 文件不存在！"
    fi
    
    # 检查配置文件
    echo "检查 _config.yml..."
    grep -E "title:|url:|theme:" _config.yml
    
    # 检查磁盘空间
    du -sh .
    ;;
    
  2)
    echo "🧹 开始清理..."
    
    # 清理缓存
    hexo clean
    
    # 删除无用文件
    find . -name "*.log" -delete
    find . -name ".DS_Store" -delete
    
    # 优化图片
    echo "优化图片..."
    # 如果有 imagemin 则运行
    
    echo "✅ 清理完成"
    ;;
    
  3)
    echo "💾 开始备份..."
    backup_dir="/e/博客备份/$(date +%Y%m%d)"
    mkdir -p "$backup_dir"
    
    # 备份文章
    cp -r source/_posts "$backup_dir/"
    
    # 备份配置
    cp _config.yml "$backup_dir/"
    cp themes/next/_config.yml "$backup_dir/theme_config.yml"
    
    # 创建压缩包
    tar -czf "$backup_dir.tar.gz" "$backup_dir"
    rm -rf "$backup_dir"
    
    echo "✅ 备份完成: $backup_dir.tar.gz"
    ;;
    
  4)
    echo "📦 更新依赖..."
    
    # 检查过时包
    npm outdated
    
    # 更新
    npm update
    
    # 修复漏洞
    npm audit fix
    
    echo "✅ 更新完成"
    ;;
    
  5)
    exit 0
    ;;
esac
```

### 11.2 使用脚本

```bash
# 添加执行权限
chmod +x maintain.sh

# 运行
./maintain.sh
```

### 11.3 定时任务设置

在 Windows 计划任务中添加：

```bash
# 创建计划任务脚本
schtasks /create /tn "BlogMaintenance" /tr "C:\Program Files\Git\bin\bash.exe -c 'cd /e/MyBlog && ./maintain.sh'" /sc weekly /d SUN /st 09:00
```

---

## 十二、维护计划

### 12.1 2026年维护日历

| 月份 | 维护任务             |
| ---- | -------------------- |
| 1月  | 年度大检查、更新主题 |
| 2月  | 常规维护、备份       |
| 3月  | 检查域名、更新插件   |
| 4月  | 优化图片、清理草稿   |
| 5月  | 检查死链、更新文章   |
| 6月  | 常规维护、半年备份   |
| 7月  | 检查分类标签         |
| 8月  | 更新主题配置         |
| 9月  | 常规维护、优化性能   |
| 10月 | 检查外部链接         |
| 11月 | 备份完整项目         |
| 12月 | 年度总结、计划明年   |

### 12.2 版本升级计划

```bash
# 检查 Hexo 新版本
npm info hexo version

# 升级 Hexo
npm install hexo@latest --save

# 检查主题新版本
cd themes/next
git tag -l
git checkout v8.0.0  # 升级到指定版本
```

---

## 十三、紧急预案

### 13.1 故障分级

| 级别   | 定义             | 响应时间 |
| ------ | ---------------- | -------- |
| **P0** | 网站完全无法访问 | 立即处理 |
| **P1** | 核心功能故障     | 2小时内  |
| **P2** | 部分功能异常     | 24小时内 |
| **P3** | 体验问题         | 3天内    |

### 13.2 P0 紧急响应流程

```bash
# 1. 立即检查 GitHub Pages 状态
curl -I https://maxkore.bbroot.com

# 2. 检查 GitHub 仓库
git status
git pull

# 3. 强制重新部署
cd /e/MyBlog
hexo clean
hexo generate
hexo deploy --force

# 4. 检查域名
nslookup maxkore.bbroot.com

# 5. 如果5分钟内未恢复，切换备用域名
# 临时使用：https://maxkore-geek.github.io
```

### 13.3 联系人

| 角色            | 联系人         | 联系方式                    |
| --------------- | -------------- | --------------------------- |
| **维护人**      | Maxkore        | GitHub @Maxkore-Geek        |
| **GitHub 支持** | GitHub Support | https://support.github.com/ |
| **域名支持**    | DNSHe          | https://my.dnshe.com        |

---

## 十四、维护记录

### 14.1 维护日志

| 日期       | 维护内容       | 维护人  | 备注                    |
| ---------- | -------------- | ------- | ----------------------- |
| 2026-02-23 | 博客初始化     | Maxkore | 创建博客                |
| 2026-02-23 | 配置自定义域名 | Maxkore | maxkore.bbroot.com      |
| 2026-02-23 | 添加重定向     | Maxkore | /docs → docs.bbroot.com |
| 2026-02-24 | 创建 Wiki      | Maxkore | maxkore-wiki.bbroot.com |
| 2026-02-24 | 更新主题配置   | Maxkore | 优化显示                |

### 14.2 问题记录

| 日期       | 问题           | 原因           | 解决              |
| ---------- | -------------- | -------------- | ----------------- |
| 2026-02-23 | 部署后域名消失 | CNAME 文件缺失 | 创建 source/CNAME |
| 2026-02-24 | HTTPS 不可用   | DNS 未生效     | 等待30分钟后启用  |
| 2026-02-24 | Git 推送被拒绝 | 远程有更新     | git pull 后重试   |

### 14.3 定期检查表

```bash
# 每月1日运行
echo "📋 月度检查表" > monthly_check.txt
echo "=================" >> monthly_check.txt
echo "✅ 域名状态: $(date)" >> monthly_check.txt
echo "✅ 文章数量: $(ls source/_posts/ | wc -l)" >> monthly_check.txt
echo "✅ 磁盘空间: $(du -sh .)" >> monthly_check.txt
echo "✅ GitHub Actions: https://github.com/Maxkore-Geek/Maxkore-Geek.github.io/actions" >> monthly_check.txt
```

---

## 📌 维护命令速查

| 命令                           | 说明      |
| ------------------------------ | --------- |
| `hexo clean && hexo g -d`      | 一键部署  |
| `git pull && git push`         | 同步代码  |
| `npm update`                   | 更新依赖  |
| `npm audit fix`                | 修复漏洞  |
| `find . -name "*.log" -delete` | 清理日志  |
| `du -sh .`                     | 查看空间  |
| `nslookup 域名`                | 检查 DNS  |
| `curl -I 域名`                 | 检查 HTTP |

---

> **最后更新**：2026年2月24日
> **维护人**：Maxkore
>
> *本说明书会持续更新，建议每月 review 一次！*
