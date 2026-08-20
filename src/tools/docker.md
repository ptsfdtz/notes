# docker

## 安装与验证

Windows 推荐安装 Docker Desktop，并启用 WSL 2 后端。安装完成后执行：

```powershell
docker version
docker run --rm hello-world
```

## 常用命令

```powershell
docker ps -a
docker images
docker pull nginx:alpine
docker run -d -p 8080:80 --name web nginx:alpine
docker logs -f web
docker exec -it web sh
docker stop web
docker rm web
```

## Compose

在含有 `compose.yaml` 的目录中运行：

```powershell
docker compose up -d
docker compose ps
docker compose logs -f
docker compose down
```

不要把密码、令牌写入镜像或提交到仓库；通过 `.env`、密钥管理服务或 CI 环境变量注入。

## 镜像构建

创建 `Dockerfile`：

```dockerfile
FROM nginx:alpine
COPY ./dist /usr/share/nginx/html
EXPOSE 80
```

构建和运行：

```powershell
docker build -t my-site:latest .
docker run --rm -p 8080:80 my-site:latest
```

## 数据卷和清理

```powershell
docker volume create mysql-data
docker run -d --name mysql -v mysql-data:/var/lib/mysql mysql:8
docker system df
docker image prune
```

## 经验总结

1. `docker ps` 只显示运行中的容器，排查退出的容器使用 `docker ps -a`。
2. 容器内的数据默认随容器删除，数据库等数据必须挂载 volume。
3. 镜像构建上下文不要包含 `node_modules`、密钥和构建产物，使用 `.dockerignore` 排除。
