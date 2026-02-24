# VSCode 配置文件指南

## 一、VSCode 简介

Visual Studio Code 是由微软开发的免费、开源的跨平台代码编辑器，拥有丰富的插件生态系统和强大的功能。

### 主要特点
- **轻量级但功能强大**：启动快速，占用资源少
- **跨平台**：支持 Windows、macOS、Linux
- **丰富的插件市场**：数万个扩展
- **内置 Git**：版本控制集成
- **智能提示**：IntelliSense 代码补全
- **调试支持**：内置调试器
- **终端集成**：内置命令行终端

## 二、安装与初始配置

### 下载安装
1. 访问 [VSCode 官网](https://code.visualstudio.com/)
2. 下载对应系统的安装包
3. 按照安装向导完成安装

### 基础设置
```json
// 打开设置：File > Preferences > Settings 或 Ctrl+,
```

## 三、核心配置文件

VSCode 的配置主要通过三个文件管理：

### 1. 用户设置 (settings.json)
**位置**：
- Windows：`%APPDATA%\Code\User\settings.json`
- macOS：`~/Library/Application Support/Code/User/settings.json`
- Linux：`~/.config/Code/User/settings.json`

**完整配置示例**：
```json
{
    // 编辑器外观
    "workbench.colorTheme": "One Dark Pro",
    "workbench.iconTheme": "material-icon-theme",
    "workbench.fontAliasing": "auto",
    "workbench.startupEditor": "none",
    "workbench.tree.indent": 20,
    "workbench.sideBar.location": "left",
    
    // 编辑器设置
    "editor.fontSize": 14,
    "editor.fontFamily": "Fira Code, 'Courier New', monospace",
    "editor.fontLigatures": true,
    "editor.lineHeight": 24,
    "editor.lineNumbers": "on",
    "editor.minimap.enabled": false,
    "editor.renderWhitespace": "boundary",
    "editor.renderControlCharacters": true,
    "editor.rulers": [80, 100, 120],
    "editor.wordWrap": "on",
    "editor.tabSize": 2,
    "editor.insertSpaces": true,
    "editor.detectIndentation": true,
    "editor.formatOnSave": true,
    "editor.formatOnPaste": true,
    "editor.formatOnType": true,
    "editor.codeActionsOnSave": {
        "source.fixAll.eslint": true,
        "source.organizeImports": true
    },
    "editor.suggestSelection": "first",
    "editor.acceptSuggestionOnEnter": "smart",
    "editor.quickSuggestions": {
        "strings": true
    },
    "editor.bracketPairColorization.enabled": true,
    "editor.guides.bracketPairs": "active",
    
    // 文件设置
    "files.autoSave": "afterDelay",
    "files.autoSaveDelay": 1000,
    "files.eol": "\n",
    "files.trimTrailingWhitespace": true,
    "files.insertFinalNewline": true,
    "files.trimFinalNewlines": true,
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/.DS_Store": true,
        "**/node_modules": true
    },
    "files.watcherExclude": {
        "**/.git/objects/**": true,
        "**/.git/subtree-cache/**": true,
        "**/node_modules/**": true,
        "**/dist/**": true,
        "**/build/**": true
    },
    
    // 终端设置
    "terminal.integrated.fontSize": 13,
    "terminal.integrated.fontFamily": "Fira Code",
    "terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe",
    "terminal.integrated.shell.linux": "/bin/bash",
    "terminal.integrated.shell.osx": "/bin/zsh",
    "terminal.integrated.defaultProfile.windows": "Git Bash",
    "terminal.integrated.cursorStyle": "line",
    "terminal.integrated.cursorBlinking": true,
    
    // Git 配置
    "git.enableSmartCommit": true,
    "git.confirmSync": false,
    "git.autofetch": true,
    "gitlens.advanced.messages": {
        "suppressShowKey": true
    },
    
    // 语言特定设置
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[typescript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[json]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[html]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[css]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    },
    "[python]": {
        "editor.defaultFormatter": "ms-python.python"
    },
    
    // 扩展设置
    "eslint.validate": [
        "javascript",
        "javascriptreact",
        "typescript",
        "typescriptreact"
    ],
    "eslint.run": "onSave",
    "prettier.singleQuote": true,
    "prettier.trailingComma": "es5",
    "prettier.printWidth": 100,
    "prettier.tabWidth": 2,
    "prettier.semi": true,
    
    // 安全设置
    "security.workspace.trust.untrustedFiles": "open",
    "security.workspace.trust.enabled": true,
    
    // 窗口设置
    "window.zoomLevel": 0,
    "window.titleBarStyle": "custom",
    "window.menuBarVisibility": "toggle",
    
    // 搜索设置
    "search.exclude": {
        "**/node_modules": true,
        "**/dist": true,
        "**/build": true,
        "**/coverage": true
    },
    
    // 更新设置
    "update.mode": "default",
    "update.enableWindowsBackgroundUpdates": true
}
```

### 2. 快捷键配置 (keybindings.json)
**位置**：与 settings.json 同目录

```json
[
    // 自定义快捷键
    {
        "key": "ctrl+shift+n",
        "command": "workbench.action.files.newUntitledFile"
    },
    {
        "key": "ctrl+alt+down",
        "command": "editor.action.copyLinesDownAction",
        "when": "editorTextFocus && !editorReadonly"
    },
    {
        "key": "ctrl+alt+up",
        "command": "editor.action.copyLinesUpAction",
        "when": "editorTextFocus && !editorReadonly"
    },
    {
        "key": "ctrl+shift+up",
        "command": "editor.action.moveLinesUpAction",
        "when": "editorTextFocus && !editorReadonly"
    },
    {
        "key": "ctrl+shift+down",
        "command": "editor.action.moveLinesDownAction",
        "when": "editorTextFocus && !editorReadonly"
    },
    {
        "key": "ctrl+d",
        "command": "editor.action.addSelectionToNextFindMatch",
        "when": "editorFocus"
    },
    {
        "key": "ctrl+shift+l",
        "command": "editor.action.selectHighlights",
        "when": "editorFocus"
    },
    {
        "key": "ctrl+alt+f",
        "command": "editor.action.formatDocument",
        "when": "editorTextFocus"
    },
    {
        "key": "ctrl+k ctrl+c",
        "command": "workbench.action.toggleCenteredLayout"
    },
    {
        "key": "ctrl+shift+v",
        "command": "markdown.showPreview",
        "when": "editorLangId == 'markdown'"
    },
    {
        "key": "ctrl+alt+t",
        "command": "workbench.action.terminal.toggleTerminal"
    },
    {
        "key": "ctrl+shift+t",
        "command": "workbench.action.terminal.new"
    }
]
```

### 3. 工作区设置
在项目根目录创建 `.vscode/settings.json`：

```json
{
    // 项目特定设置
    "files.exclude": {
        "**/node_modules": true,
        "**/dist": true,
        "**/.git": true
    },
    
    // 项目特定的格式化设置
    "editor.tabSize": 2,
    "editor.insertSpaces": true,
    
    // 项目特定的语言设置
    "typescript.preferences.quoteStyle": "single",
    "javascript.preferences.quoteStyle": "single",
    
    // 项目特定的调试配置
    "debug.javascript.autoAttachFilter": "onlyWithFlag",
    
    // 推荐扩展
    "extensions.recommendations": [
        "dbaeumer.vscode-eslint",
        "esbenp.prettier-vscode",
        "ms-vscode.vscode-typescript-next"
    ]
}
```

## 四、任务配置 (tasks.json)

在 `.vscode/tasks.json` 中配置构建任务：

```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Build",
            "type": "shell",
            "command": "npm run build",
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": ["$tsc"]
        },
        {
            "label": "Test",
            "type": "shell",
            "command": "npm test",
            "group": "test",
            "problemMatcher": []
        },
        {
            "label": "Dev Server",
            "type": "shell",
            "command": "npm start",
            "isBackground": true,
            "problemMatcher": {
                "pattern": {
                    "regexp": ".",
                    "file": 1,
                    "location": 2,
                    "message": 3
                },
                "background": {
                    "activeOnStart": true,
                    "beginsPattern": "Starting development server",
                    "endsPattern": "Compiled successfully"
                }
            }
        },
        {
            "label": "Lint",
            "type": "shell",
            "command": "npm run lint",
            "group": "build",
            "problemMatcher": ["$eslint-stylish"]
        },
        {
            "label": "Clean",
            "type": "shell",
            "command": "rm -rf dist",
            "problemMatcher": []
        }
    ]
}
```

## 五、调试配置 (launch.json)

在 `.vscode/launch.json` 中配置调试器：

```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "type": "node",
            "request": "launch",
            "name": "启动程序",
            "skipFiles": ["<node_internals>/**"],
            "program": "${workspaceFolder}/src/index.js",
            "outFiles": ["${workspaceFolder}/dist/**/*.js"],
            "env": {
                "NODE_ENV": "development"
            },
            "console": "integratedTerminal"
        },
        {
            "type": "node",
            "request": "launch",
            "name": "调试当前文件",
            "program": "${file}",
            "console": "integratedTerminal"
        },
        {
            "type": "node",
            "request": "attach",
            "name": "附加到进程",
            "port": 9229,
            "restart": true,
            "localRoot": "${workspaceFolder}",
            "remoteRoot": "/app"
        },
        {
            "type": "chrome",
            "request": "launch",
            "name": "启动 Chrome",
            "url": "http://localhost:3000",
            "webRoot": "${workspaceFolder}",
            "userDataDir": "${workspaceFolder}/.vscode/chrome-debug-profile"
        },
        {
            "type": "node",
            "request": "launch",
            "name": "Jest 测试",
            "program": "${workspaceFolder}/node_modules/jest/bin/jest",
            "args": ["--runInBand", "--config", "jest.config.js"],
            "console": "integratedTerminal",
            "internalConsoleOptions": "neverOpen"
        },
        {
            "name": "Python: 当前文件",
            "type": "python",
            "request": "launch",
            "program": "${file}",
            "console": "integratedTerminal"
        }
    ],
    "compounds": [
        {
            "name": "前后端同时调试",
            "configurations": ["启动程序", "启动 Chrome"]
        }
    ]
}
```

## 六、代码片段 (snippets)

### JavaScript/TypeScript 代码片段
位置：`~/.config/Code/User/snippets/javascript.json`

```json
{
    "Console Log": {
        "prefix": "clg",
        "body": ["console.log('${1:变量名}:', ${1:变量});"],
        "description": "打印日志"
    },
    "Import React": {
        "prefix": "imr",
        "body": ["import React from 'react';"],
        "description": "导入 React"
    },
    "React Function Component": {
        "prefix": "rfc",
        "body": [
            "import React from 'react';",
            "",
            "const ${1:ComponentName} = () => {",
            "  return (",
            "    <div>",
            "      $2",
            "    </div>",
            "  );",
            "};",
            "",
            "export default ${1:ComponentName};"
        ],
        "description": "React 函数组件"
    },
    "UseState": {
        "prefix": "use",
        "body": ["const [${1:state}, set${1/(.*)/${1:/capitalize}/}] = useState(${2:initialValue});"],
        "description": "React useState Hook"
    },
    "Try Catch": {
        "prefix": "try",
        "body": [
            "try {",
            "  ${1:}",
            "} catch (error) {",
            "  console.error('${2:错误}:', error);",
            "}"
        ],
        "description": "try-catch 语句"
    }
}
```

### Python 代码片段
位置：`~/.config/Code/User/snippets/python.json`

```json
{
    "Python Main": {
        "prefix": "main",
        "body": [
            "def main():",
            "    ${1:pass}",
            "",
            "if __name__ == '__main__':",
            "    main()"
        ],
        "description": "Python 主函数"
    },
    "Import Pandas": {
        "prefix": "impd",
        "body": ["import pandas as pd"],
        "description": "导入 pandas"
    },
    "Flask App": {
        "prefix": "flask",
        "body": [
            "from flask import Flask",
            "",
            "app = Flask(__name__)",
            "",
            "@app.route('/')",
            "def hello():",
            "    return '${1:Hello World}'",
            "",
            "if __name__ == '__main__':",
            "    app.run(debug=True)"
        ],
        "description": "Flask 应用模板"
    }
}
```

## 七、扩展配置

### 必需扩展配置
创建 `.vscode/extensions.json`：

```json
{
    "recommendations": [
        "formulahendry.auto-rename-tag",
        "coenraads.bracket-pair-colorizer-2",
        "msjsdiag.debugger-for-chrome",
        "mikestead.dotenv",
        "editorconfig.editorconfig",
        "dbaeumer.vscode-eslint",
        "eamodio.gitlens",
        "ecmel.vscode-html-css",
        "zignd.html-css-class-completion",
        "xabikos.javascriptsnippets",
        "ms-vsliveshare.vsliveshare",
        "yzhang.markdown-all-in-one",
        "esbenp.prettier-vscode",
        "ms-python.python",
        "alefragnani.project-manager",
        "ms-vscode-remote.remote-ssh",
        "ms-vscode-remote.remote-containers",
        "gruntfuggly.todo-tree",
        "pflannery.vscode-versionlens",
        "redhat.vscode-yaml"
    ],
    "unwantedRecommendations": [
        "hookyqr.beautify",
        "ms-vscode.vscode-typescript-tslint-plugin"
    ]
}
```

### 扩展设置示例
```json
// 在 settings.json 中添加扩展特定配置
{
    // GitLens
    "gitlens.codeLens.enabled": false,
    "gitlens.currentLine.enabled": true,
    
    // Todo Tree
    "todo-tree.general.tags": ["TODO", "FIXME", "BUG", "HACK"],
    "todo-tree.highlights.defaultHighlight": {
        "icon": "checklist",
        "type": "text",
        "foreground": "#ffffff",
        "background": "#ffbd2a"
    },
    
    // Bracket Pair Colorizer
    "bracketPairColorizer.consecutivePairColors": [
        "()",
        "[]",
        "{}",
        ["Gold", "Orchid", "LightSkyBlue"],
        "Red"
    ],
    
    // Project Manager
    "projectManager.git.baseFolders": [
        "~/Projects",
        "~/Documents/Projects"
    ]
}
```

## 八、配置备份与同步

### 使用 Settings Sync 扩展
1. 安装 "Settings Sync" 扩展
2. 登录 GitHub 创建 Personal Access Token
3. 上传配置：
   ```bash
   # 快捷键上传
   Shift + Alt + U
   # 或命令面板输入 "Sync: Update/Upload Settings"
   ```
4. 下载配置：
   ```bash
   # 快捷键下载
   Shift + Alt + D
   # 或命令面板输入 "Sync: Download Settings"
   ```

### 手动备份脚本
创建备份脚本 `backup-vscode-config.sh`：

```bash
#!/bin/bash

# 配置备份目录
BACKUP_DIR="$HOME/vscode-backup-$(date +%Y%m%d)"
VSCODE_USER_DIR="$HOME/.config/Code/User"

# 创建备份目录
mkdir -p $BACKUP_DIR

# 备份配置文件
cp "$VSCODE_USER_DIR/settings.json" "$BACKUP_DIR/"
cp "$VSCODE_USER_DIR/keybindings.json" "$BACKUP_DIR/"
cp -r "$VSCODE_USER_DIR/snippets" "$BACKUP_DIR/"

# 备份扩展列表
code --list-extensions > "$BACKUP_DIR/extensions.txt"

# 创建恢复脚本
cat > "$BACKUP_DIR/restore.sh" << 'EOF'
#!/bin/bash
VSCODE_USER_DIR="$HOME/.config/Code/User"

# 恢复配置文件
cp settings.json "$VSCODE_USER_DIR/"
cp keybindings.json "$VSCODE_USER_DIR/"
cp -r snippets "$VSCODE_USER_DIR/"

# 安装扩展
while read extension; do
    code --install-extension $extension
done < extensions.txt

echo "恢复完成！"
EOF

chmod +x "$BACKUP_DIR/restore.sh"

echo "备份完成！备份位置：$BACKUP_DIR"
```

### Windows 备份脚本
创建 `backup-vscode-config.ps1`：

```powershell
$backupDir = "$env:USERPROFILE\vscode-backup-$(Get-Date -Format 'yyyyMMdd')"
$vscodeUserDir = "$env:APPDATA\Code\User"

# 创建备份目录
New-Item -ItemType Directory -Path $backupDir -Force

# 备份配置文件
Copy-Item "$vscodeUserDir\settings.json" $backupDir
Copy-Item "$vscodeUserDir\keybindings.json" $backupDir
Copy-Item -Recurse "$vscodeUserDir\snippets" $backupDir

# 备份扩展列表
code --list-extensions | Out-File "$backupDir\extensions.txt"

# 创建恢复脚本
@"
`$vscodeUserDir = "`$env:APPDATA\Code\User"

Copy-Item settings.json `$vscodeUserDir
Copy-Item keybindings.json `$vscodeUserDir
Copy-Item -Recurse snippets `$vscodeUserDir

Get-Content extensions.txt | ForEach-Object {
    code --install-extension `$_
}

Write-Host "恢复完成！"
"@ | Out-File "$backupDir\restore.ps1"

Write-Host "备份完成！备份位置：$backupDir"
```

## 九、项目模板配置

### 创建项目模板目录结构
```
project-template/
├── .vscode/
│   ├── settings.json      # 项目特定设置
│   ├── launch.json        # 调试配置
│   ├── tasks.json         # 任务配置
│   └── extensions.json    # 推荐扩展
├── .gitignore
├── .editorconfig
├── .eslintrc.js
├── .prettierrc
├── README.md
└── src/
    └── index.js
```

### .editorconfig 文件
```ini
# EditorConfig 配置
root = true

[*]
charset = utf-8
end_of_line = lf
indent_size = 2
indent_style = space
insert_final_newline = true
trim_trailing_whitespace = true

[*.md]
trim_trailing_whitespace = false

[*.{json,yml,yaml}]
indent_size = 2

[*.py]
indent_size = 4
```

### .eslintrc.js 示例
```javascript
module.exports = {
  env: {
    browser: true,
    es2021: true,
    node: true,
  },
  extends: ['eslint:recommended', 'plugin:prettier/recommended'],
  parserOptions: {
    ecmaVersion: 12,
    sourceType: 'module',
  },
  rules: {
    'no-console': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'no-debugger': process.env.NODE_ENV === 'production' ? 'warn' : 'off',
    'prettier/prettier': [
      'error',
      {
        singleQuote: true,
        semi: true,
        trailingComma: 'es5',
        printWidth: 100,
        tabWidth: 2,
      },
    ],
  },
};
```

### .prettierrc 配置
```json
{
  "semi": true,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "es5",
  "printWidth": 100,
  "bracketSpacing": true,
  "arrowParens": "always",
  "endOfLine": "lf"
}
```

## 十、性能优化配置

### 优化 settings.json
```json
{
    // 禁用不需要的功能
    "telemetry.enableTelemetry": false,
    "telemetry.enableCrashReporter": false,
    
    // 优化搜索
    "search.followSymlinks": false,
    "search.useIgnoreFiles": true,
    
    // 优化文件监视
    "files.watcherExclude": {
        "**/.git/objects/**": true,
        "**/.git/subtree-cache/**": true,
        "**/node_modules/**": true,
        "**/dist/**": true,
        "**/build/**": true,
        "**/coverage/**": true
    },
    
    // 优化 Git
    "git.autofetch": false,
    "git.enableSmartCommit": false,
    
    // 优化编辑器
    "editor.minimap.enabled": false,
    "editor.largeFileOptimizations": true,
    "editor.maxTokenizationLineLength": 20000,
    
    // 优化扩展
    "extensions.autoUpdate": false,
    "extensions.ignoreRecommendations": true,
    
    // 优化工作区
    "workbench.enableExperiments": false,
    "workbench.settings.enableNaturalLanguageSearch": false
}
```

## 十一、常用快捷键速查表

| 功能         | Windows/Linux         | macOS            |
| ------------ | --------------------- | ---------------- |
| 命令面板     | `Ctrl+Shift+P`        | `Cmd+Shift+P`    |
| 快速打开文件 | `Ctrl+P`              | `Cmd+P`          |
| 切换侧边栏   | `Ctrl+B`              | `Cmd+B`          |
| 打开终端     | `Ctrl+` ` | `Ctrl+` ` |                  |
| 新建文件     | `Ctrl+N`              | `Cmd+N`          |
| 保存文件     | `Ctrl+S`              | `Cmd+S`          |
| 关闭文件     | `Ctrl+W`              | `Cmd+W`          |
| 多光标选择   | `Alt+Click`           | `Option+Click`   |
| 选择所有匹配 | `Ctrl+Shift+L`        | `Cmd+Shift+L`    |
| 格式化文档   | `Shift+Alt+F`         | `Shift+Option+F` |
| 代码折叠     | `Ctrl+Shift+[`        | `Cmd+Option+[`   |
| 代码展开     | `Ctrl+Shift+]`        | `Cmd+Option+]`   |
| 跳转到定义   | `F12`                 | `F12`            |
| 查看定义     | `Alt+F12`             | `Option+F12`     |
| 重命名符号   | `F2`                  | `F2`             |
| 全局搜索     | `Ctrl+Shift+F`        | `Cmd+Shift+F`    |
| 替换         | `Ctrl+H`              | `Cmd+Option+F`   |
| 调试开始     | `F5`                  | `F5`             |
| 调试停止     | `Shift+F5`            | `Shift+F5`       |
| 注释切换     | `Ctrl+/`              | `Cmd+/`          |
| 块注释       | `Shift+Alt+A`         | `Shift+Option+A` |

## 十二、常见问题解决

### 1. 配置不生效
```bash
# 重启 VSCode
# 检查配置文件语法错误
# 查看开发者工具查看错误
```

### 2. 扩展冲突
```bash
# 禁用所有扩展启动
code --disable-extensions

# 逐个启用排查冲突
```

### 3. 性能问题
```bash
# 检查 CPU/内存使用
# 禁用不必要的扩展
# 排除大文件夹
# 更新 VSCode 到最新版本
```

### 4. 配置丢失
```bash
# 从备份恢复
# 检查同步服务
# 导出配置定期备份
```

