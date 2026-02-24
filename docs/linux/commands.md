# Linux 命令速查表

## 文件操作命令

| 命令     | 说明          | 示例                                               |
| -------- | ------------- | -------------------------------------------------- |
| `ls`     | 列出文件      | `ls -la` 显示所有文件详细信息                      |
| `cd`     | 切换目录      | `cd /home/user` 进入目录                           |
| `pwd`    | 显示当前路径  | `pwd`                                              |
| `mkdir`  | 创建目录      | `mkdir newfolder`                                  |
| `rmdir`  | 删除空目录    | `rmdir emptyfolder`                                |
| `rm`     | 删除文件/目录 | `rm file.txt` / `rm -rf folder`                    |
| `cp`     | 复制          | `cp file1.txt file2.txt` / `cp -r folder1 folder2` |
| `mv`     | 移动/重命名   | `mv old.txt new.txt`                               |
| `touch`  | 创建空文件    | `touch newfile.txt`                                |
| `cat`    | 查看文件内容  | `cat file.txt`                                     |
| `less`   | 分页查看      | `less largefile.log`                               |
| `head`   | 查看文件开头  | `head -n 20 file.txt`                              |
| `tail`   | 查看文件结尾  | `tail -f log.txt`                                  |
| `find`   | 查找文件      | `find . -name "*.txt"`                             |
| `locate` | 快速查找      | `locate filename`                                  |
| `which`  | 查找命令路径  | `which python`                                     |

## 权限管理命令

| 命令       | 说明         | 示例                        |
| ---------- | ------------ | --------------------------- |
| `chmod`    | 修改权限     | `chmod 755 script.sh`       |
| `chown`    | 修改所有者   | `chown user:group file.txt` |
| `chgrp`    | 修改组       | `chgrp group file.txt`      |
| `whoami`   | 显示当前用户 | `whoami`                    |
| `sudo`     | 超级用户执行 | `sudo apt update`           |
| `su`       | 切换用户     | `su - username`             |
| `passwd`   | 修改密码     | `passwd`                    |
| `useradd`  | 添加用户     | `useradd newuser`           |
| `userdel`  | 删除用户     | `userdel username`          |
| `groupadd` | 添加组       | `groupadd newgroup`         |

## 进程管理命令

| 命令      | 说明           | 示例                          |
| --------- | -------------- | ----------------------------- |
| `ps`      | 查看进程       | `ps aux` 查看所有进程         |
| `top`     | 实时查看进程   | `top`                         |
| `htop`    | 交互式进程查看 | `htop`                        |
| `kill`    | 终止进程       | `kill -9 PID`                 |
| `killall` | 按名称终止     | `killall firefox`             |
| `pkill`   | 模式匹配终止   | `pkill -f "python script.py"` |
| `jobs`    | 查看后台作业   | `jobs`                        |
| `bg`      | 后台运行       | `bg %1`                       |
| `fg`      | 前台运行       | `fg %1`                       |
| `nohup`   | 忽略挂起运行   | `nohup command &`             |

## 网络命令

| 命令         | 说明           | 示例                              |
| ------------ | -------------- | --------------------------------- |
| `ping`       | 测试网络连接   | `ping google.com`                 |
| `curl`       | 发送 HTTP 请求 | `curl https://api.example.com`    |
| `wget`       | 下载文件       | `wget https://file.com/file.zip`  |
| `netstat`    | 网络状态       | `netstat -tlnp`                   |
| `ss`         | 套接字统计     | `ss -tuln`                        |
| `ssh`        | 远程连接       | `ssh user@server.com`             |
| `scp`        | 远程复制       | `scp file.txt user@server:/path/` |
| `rsync`      | 同步文件       | `rsync -av source/ dest/`         |
| `ifconfig`   | 网络接口配置   | `ifconfig`                        |
| `ip`         | IP 命令        | `ip addr show`                    |
| `nslookup`   | DNS 查询       | `nslookup google.com`             |
| `dig`        | DNS 详细查询   | `dig google.com`                  |
| `traceroute` | 路由追踪       | `traceroute google.com`           |

## 系统信息命令

| 命令       | 说明         | 示例            |
| ---------- | ------------ | --------------- |
| `df`       | 磁盘使用情况 | `df -h`         |
| `du`       | 目录大小     | `du -sh folder` |
| `free`     | 内存使用情况 | `free -h`       |
| `uname`    | 系统信息     | `uname -a`      |
| `uptime`   | 系统运行时间 | `uptime`        |
| `hostname` | 主机名       | `hostname`      |
| `who`      | 登录用户     | `who`           |
| `last`     | 最近登录     | `last`          |
| `date`     | 日期时间     | `date`          |
| `cal`      | 日历         | `cal 2026`      |
| `dmesg`    | 内核日志     | `dmesg \| tail` |
| `lscpu`    | CPU 信息     | `lscpu`         |
| `lsblk`    | 块设备信息   | `lsblk`         |

## 压缩和解压命令

| 命令      | 说明       | 示例                              |
| --------- | ---------- | --------------------------------- |
| `tar`     | tar 打包   | `tar -czf archive.tar.gz folder/` |
| `tar`     | 解压 tar   | `tar -xzf archive.tar.gz`         |
| `zip`     | zip 压缩   | `zip -r archive.zip folder/`      |
| `unzip`   | 解压 zip   | `unzip archive.zip`               |
| `gzip`    | gzip 压缩  | `gzip file.txt`                   |
| `gunzip`  | 解压 gz    | `gunzip file.txt.gz`              |
| `bzip2`   | bzip2 压缩 | `bzip2 file.txt`                  |
| `bunzip2` | 解压 bz2   | `bunzip2 file.txt.bz2`            |

## 文本处理命令

| 命令    | 说明         | 示例                             |
| ------- | ------------ | -------------------------------- |
| `grep`  | 搜索文本     | `grep "error" log.txt`           |
| `egrep` | 扩展正则     | `egrep "error\|warning" log.txt` |
| `sed`   | 流编辑器     | `sed 's/old/new/g' file.txt`     |
| `awk`   | 文本处理工具 | `awk '{print $1}' file.txt`      |
| `sort`  | 排序         | `sort file.txt`                  |
| `uniq`  | 去重         | `uniq file.txt`                  |
| `wc`    | 统计         | `wc -l file.txt` 统计行数        |
| `cut`   | 剪切列       | `cut -d',' -f1 file.csv`         |
| `tr`    | 替换字符     | `tr 'a-z' 'A-Z' < file.txt`      |
| `diff`  | 比较文件     | `diff file1.txt file2.txt`       |

## 软件包管理

### Debian/Ubuntu (apt)
```bash
sudo apt update              # 更新软件源
sudo apt upgrade             # 升级软件包
sudo apt install package     # 安装软件包
sudo apt remove package      # 移除软件包
sudo apt autoremove          # 自动移除不需要的包
apt search keyword           # 搜索软件包
apt show package             # 显示软件包信息
```

### RedHat/CentOS (yum)
```bash
sudo yum install package     # 安装软件包
sudo yum remove package      # 移除软件包
sudo yum update              # 更新软件包
yum search keyword           # 搜索软件包
yum list installed           # 列出已安装包
```

## 系统服务管理

```bash
systemctl status nginx       # 查看服务状态
systemctl start nginx        # 启动服务
systemctl stop nginx         # 停止服务
systemctl restart nginx      # 重启服务
systemctl enable nginx       # 启用开机启动
systemctl disable nginx      # 禁用开机启动
journalctl -u nginx          # 查看服务日志
```

## 快捷键

| 快捷键     | 说明         |
| ---------- | ------------ |
| `Ctrl + C` | 终止当前命令 |
| `Ctrl + Z` | 挂起当前命令 |
| `Ctrl + D` | 退出终端     |
| `Ctrl + R` | 搜索历史命令 |
| `Ctrl + L` | 清屏         |
| `Ctrl + A` | 光标到行首   |
| `Ctrl + E` | 光标到行尾   |
| `Tab`      | 自动补全     |
| `↑/↓`      | 浏览历史命令 |

## 实用技巧

### 重定向和管道
```bash
# 输出重定向
echo "hello" > file.txt      # 覆盖写入
echo "world" >> file.txt     # 追加写入

# 错误重定向
command 2> error.log         # 重定向错误输出
command > output.log 2>&1    # 重定向所有输出

# 管道
ls -la | grep ".txt"         # 过滤输出
cat file.txt | wc -l         # 统计行数
```

### 通配符
```bash
*.txt        # 所有txt文件
file?.txt    # file1.txt, file2.txt 等
file[0-9]    # file0, file1, ..., file9
{1..10}      # 1 2 3 4 5 6 7 8 9 10
```

### 别名
```bash
alias ll='ls -la'
alias gs='git status'
alias ..='cd ..'
```