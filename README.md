# Babylon 3D Tool 容器化部署指南

本项目已完成 Docker 化配置，支持通过 Docker Compose 一键启动前后端服务。

## 目录结构说明

```text
ModelData3d/
├── backend/
│   ├── Dockerfile          # 后端镜像构建文件
│   └── .dockerignore       # 构建忽略文件
├── frontend/
│   ├── Dockerfile          # 前端镜像构建文件
│   ├── .dockerignore       # 构建忽略文件
│   └── nginx.conf          # 前端 Nginx 配置文件
├── backend-image.tar       # 预构建的后端镜像包
├── frontend-image.tar      # 预构建的前端镜像包
└── docker-compose.yml      # 多容器编排文件
```

## 准备工作

1. 确保机器上已安装 [Docker](https://www.docker.com/) 和 [Docker Compose](https://docs.docker.com/compose/)。
2. 将此 `ModelData3d` 文件夹拷贝到项目的根目录下（即与 `frontend` 和 `backend` 文件夹同级）。

## 部署说明

此文件夹专为“离线分发”设计。由于分发包中不包含源代码，因此**必须**先加载镜像包。

## 启动步骤

在 `ModelData3d` 目录下打开终端，执行以下命令：

1. **加载镜像包**（仅第一次或镜像更新时需要）：
   ```bash
   docker load -i backend-image.tar
   docker load -i frontend-image.tar
   ```

2. **启动服务**：
   ```bash
   docker-compose up -d
   ```

启动成功后：
- **前端地址**: [http://localhost:3695](http://localhost:3695)
- **后端 API**: [http://localhost:3358/api/v1](http://localhost:3358/api/v1)

## 数据持久化

项目的数据（SQLite 数据库和上传的资产文件）将持久化在 `ModelData3d/storage` 目录下。即使删除容器，数据也不会丢失。

## 停止服务

```bash
docker-compose down
```