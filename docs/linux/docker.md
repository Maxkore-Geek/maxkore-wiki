# Docker 使用指南

## 一、Docker 简介

Docker 是一个开源的容器化平台，允许开发者将应用程序及其依赖打包成轻量级、可移植的容器。容器与虚拟机不同，它们共享主机操作系统内核，因此更轻量、启动更快、资源利用率更高。

### 核心概念
- **镜像（Image）**：只读模板，包含创建容器的指令
- **容器（Container）**：镜像的可运行实例
- **Dockerfile**：自动构建镜像的脚本
- **仓库（Repository）**：存储和分发镜像的地方
- **Docker Hub**：官方的公共镜像仓库

## 二、安装 Docker

### Windows / macOS
1. 下载 [Docker Desktop](https://www.docker.com/products/docker-desktop)
2. 双击安装，按提示完成
3. 启动 Docker Desktop

### Linux (Ubuntu/Debian)
```bash
# 更新包索引
sudo apt update

# 安装依赖
sudo apt install apt-transport-https ca-certificates curl software-properties-common

# 添加 Docker 官方 GPG 密钥
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

# 添加稳定版仓库
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"

# 安装 Docker
sudo apt update
sudo apt install docker-ce

# 启动 Docker
sudo systemctl start docker
sudo systemctl enable docker

# 验证安装
docker --version
```

### 验证安装
```bash
docker run hello-world
```

## 三、Docker 基本命令

### 镜像管理
```bash
# 列出本地镜像
docker images

# 搜索镜像
docker search nginx

# 拉取镜像
docker pull ubuntu:20.04

# 删除镜像
docker rmi nginx

# 构建镜像
docker build -t myapp:1.0 .
```

### 容器管理
```bash
# 创建并启动容器
docker run nginx

# 后台运行
docker run -d nginx

# 指定端口映射
docker run -d -p 8080:80 nginx

# 指定容器名称
docker run -d --name mynginx nginx

# 列出运行中的容器
docker ps

# 列出所有容器（包括停止的）
docker ps -a

# 停止容器
docker stop container_id

# 启动已停止的容器
docker start container_id

# 重启容器
docker restart container_id

# 删除容器
docker rm container_id

# 强制删除运行中的容器
docker rm -f container_id

# 进入容器内部
docker exec -it container_id bash

# 查看容器日志
docker logs container_id

# 查看容器详细信息
docker inspect container_id
```

## 四、Dockerfile 编写指南

### 基础指令
```dockerfile
# 指定基础镜像
FROM ubuntu:20.04

# 设置作者信息
LABEL maintainer="your-email@example.com"

# 设置工作目录
WORKDIR /app

# 复制文件到镜像
COPY . /app

# 添加文件（支持 URL 和解压）
ADD app.tar.gz /app

# 运行命令
RUN apt update && apt install -y python3

# 设置环境变量
ENV NODE_ENV=production

# 暴露端口
EXPOSE 3000

# 定义卷
VOLUME ["/data"]

# 指定用户
USER nobody

# 容器启动时执行的命令
CMD ["python3", "app.py"]

# 入口点（与 CMD 配合使用）
ENTRYPOINT ["docker-entrypoint.sh"]
```

### 示例：Node.js 应用
```dockerfile
FROM node:14-alpine

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 8080

CMD ["node", "server.js"]
```

### 示例：Python Flask 应用
```dockerfile
FROM python:3.9-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

ENV FLASK_APP=app.py

EXPOSE 5000

CMD ["flask", "run", "--host=0.0.0.0"]
```

## 五、Docker Compose

Docker Compose 用于定义和运行多容器 Docker 应用。

### 安装
```bash
# Linux
sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose

# 验证
docker-compose --version
```

### docker-compose.yml 示例
```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    environment:
      - FLASK_ENV=development
    volumes:
      - .:/app
    depends_on:
      - redis
      - db

  redis:
    image: redis:alpine
    ports:
      - "6379:6379"

  db:
    image: postgres:13
    environment:
      - POSTGRES_DB=myapp
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

### 常用命令
```bash
# 启动所有服务
docker-compose up

# 后台启动
docker-compose up -d

# 构建镜像并启动
docker-compose up --build

# 停止服务
docker-compose down

# 停止并删除卷
docker-compose down -v

# 查看日志
docker-compose logs

# 查看服务状态
docker-compose ps

# 执行命令
docker-compose exec web bash

# 重新构建服务
docker-compose build

# 查看配置
docker-compose config
```

## 六、数据管理

### 数据卷（Volumes）
```bash
# 创建卷
docker volume create mydata

# 列出卷
docker volume ls

# 查看卷信息
docker volume inspect mydata

# 使用卷
docker run -d -v mydata:/data nginx

# 删除未使用的卷
docker volume prune
```

### 绑定挂载（Bind Mounts）
```bash
# 将主机目录挂载到容器
docker run -d -v /host/data:/container/data nginx

# 只读挂载
docker run -d -v /host/data:/container/data:ro nginx
```

## 七、网络配置

### 网络模式
```bash
# 列出网络
docker network ls

# 创建网络
docker network create mynetwork

# 运行容器并连接到网络
docker run -d --network mynetwork --name web nginx

# 容器间通信（使用容器名）
docker run -d --network mynetwork --name app myapp

# 查看网络详情
docker network inspect mynetwork

# 断开网络连接
docker network disconnect mynetwork web

# 删除网络
docker network rm mynetwork
```

### 端口映射
```bash
# 映射到随机端口
docker run -d -P nginx

# 指定端口映射
docker run -d -p 8080:80 nginx

# 指定 IP 和端口
docker run -d -p 127.0.0.1:8080:80 nginx

# 多个端口映射
docker run -d -p 8080:80 -p 8443:443 nginx
```

## 八、镜像构建与优化

### 构建优化技巧
```dockerfile
# 合并 RUN 命令减少层数
RUN apt update && \
    apt install -y package1 package2 && \
    apt clean

# 使用 .dockerignore 文件
# .dockerignore 内容：
node_modules
.git
*.log
Dockerfile
README.md

# 多阶段构建
FROM golang:1.16 AS builder
WORKDIR /app
COPY . .
RUN go build -o myapp

FROM alpine:latest
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/myapp .
CMD ["./myapp"]
```

## 九、安全最佳实践

1. **使用官方镜像**或可信的基础镜像
2. **最小化镜像大小**：使用 alpine 等轻量级基础镜像
3. **不以 root 运行**：创建并使用普通用户
   ```dockerfile
   RUN groupadd -r myuser && useradd -r -g myuser myuser
   USER myuser
   ```
4. **定期更新基础镜像**
5. **限制资源使用**
   ```bash
   docker run -d --memory="512m" --cpus="0.5" nginx
   ```
6. **扫描镜像漏洞**
   ```bash
   docker scan myimage:latest
   ```

## 十、常用 Docker 命令速查表

| 命令                                       | 说明                 |
| ------------------------------------------ | -------------------- |
| `docker ps`                                | 列出运行中的容器     |
| `docker ps -a`                             | 列出所有容器         |
| `docker images`                            | 列出镜像             |
| `docker pull <image>`                      | 拉取镜像             |
| `docker run <image>`                       | 运行容器             |
| `docker stop <container>`                  | 停止容器             |
| `docker start <container>`                 | 启动容器             |
| `docker restart <container>`               | 重启容器             |
| `docker rm <container>`                    | 删除容器             |
| `docker rmi <image>`                       | 删除镜像             |
| `docker build -t <name> .`                 | 构建镜像             |
| `docker exec -it <container> bash`         | 进入容器             |
| `docker logs <container>`                  | 查看日志             |
| `docker cp <container>:<path> <host_path>` | 复制文件从容器到主机 |
| `docker system prune`                      | 清理未使用的资源     |
| `docker-compose up`                        | 启动 compose 服务    |
| `docker-compose down`                      | 停止 compose 服务    |

## 十一、常见问题解决

### 1. 权限问题（Linux）
```bash
# 将用户添加到 docker 组
sudo usermod -aG docker $USER
# 重新登录或重启
```

### 2. 清理磁盘空间
```bash
# 清理所有未使用的资源
docker system prune -a

# 清理特定资源
docker container prune
docker image prune
docker volume prune
docker network prune
```

### 3. 容器无法删除
```bash
# 强制删除
docker rm -f container_id

# 删除所有停止的容器
docker container prune
```

## 十二、学习资源

- [Docker 官方文档](https://docs.docker.com/)
- [Docker Hub](https://hub.docker.com/)
- [Docker 课程](https://www.docker.com/101-tutorial)
- [Play with Docker](https://labs.play-with-docker.com/)（在线实验环境）

