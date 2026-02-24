\# Linux 命令速查表



\## 文件操作

| 命令 | 说明 | 示例 |

|------|------|------|

| `ls` | 列出文件 | `ls -la` 显示所有文件详细信息 |

| `cd` | 切换目录 | `cd /home/user` 进入目录 |

| `pwd` | 显示当前路径 | `pwd` |

| `mkdir` | 创建目录 | `mkdir newfolder` |

| `rm` | 删除文件/目录 | `rm file.txt` / `rm -rf folder` |

| `cp` | 复制 | `cp file1.txt file2.txt` |

| `mv` | 移动/重命名 | `mv old.txt new.txt` |

| `cat` | 查看文件内容 | `cat file.txt` |

| `less` | 分页查看 | `less largefile.log` |

| `head` | 查看文件开头 | `head -n 20 file.txt` |

| `tail` | 查看文件结尾 | `tail -f log.txt` |



\## 权限管理

| 命令 | 说明 | 示例 |

|------|------|------|

| `chmod` | 修改权限 | `chmod 755 script.sh` |

| `chown` | 修改所有者 | `chown user:group file.txt` |

| `whoami` | 显示当前用户 | `whoami` |

| `sudo` | 超级用户执行 | `sudo apt update` |



\## 进程管理

| 命令 | 说明 | 示例 |

|------|------|------|

| `ps` | 查看进程 | `ps aux` 查看所有进程 |

| `top` | 实时查看进程 | `top` |

| `kill` | 终止进程 | `kill -9 PID` |

| `htop` | 交互式进程查看 | `htop` |



\## 网络命令

| 命令 | 说明 | 示例 |

|------|------|------|

| `ping` | 测试网络连接 | `ping google.com` |

| `curl` | 发送 HTTP 请求 | `curl https://api.example.com` |

| `wget` | 下载文件 | `wget https://file.com/file.zip` |

| `netstat` | 网络状态 | `netstat -tlnp` |

| `ssh` | 远程连接 | `ssh user@server.com` |



\## 系统信息

| 命令 | 说明 | 示例 |

|------|------|------|

| `df` | 磁盘使用情况 | `df -h` |

| `du` | 目录大小 | `du -sh folder` |

| `free` | 内存使用情况 | `free -h` |

| `uname` | 系统信息 | `uname -a` |

| `uptime` | 系统运行时间 | `uptime` |



\## 压缩和解压

| 命令 | 说明 | 示例 |

|------|------|------|

| `tar` | tar 打包 | `tar -czf archive.tar.gz folder/` |

| `zip` | zip 压缩 | `zip -r archive.zip folder/` |

| `unzip` | 解压 zip | `unzip archive.zip` |

| `gzip` | gzip 压缩 | `gzip file.txt` |

| `gunzip` | 解压 gz | `gunzip file.txt.gz` |



\## 文本处理

| 命令 | 说明 | 示例 |

|------|------|------|

| `grep` | 搜索文本 | `grep "error" log.txt` |

| `sed` | 流编辑器 | `sed 's/old/new/g' file.txt` |

| `awk` | 文本处理工具 | `awk '{print $1}' file.txt` |

| `sort` | 排序 | `sort file.txt` |

| `uniq` | 去重 | `uniq file.txt` |

| `wc` | 统计 | `wc -l file.txt` 统计行数 |



\## 快捷键

| 快捷键 | 说明 |

|--------|------|

| `Ctrl + C` | 终止当前命令 |

| `Ctrl + Z` | 挂起当前命令 |

| `Ctrl + D` | 退出终端 |

| `Ctrl + R` | 搜索历史命令 |

| `Tab` | 自动补全 |

| `↑/↓` | 浏览历史命令 |

