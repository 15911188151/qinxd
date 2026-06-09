# 快速开始指南

## 前置要求

- Docker Desktop（已安装）
- Java 11+（本地开发）
- Node.js 14+（本地开发）
- Git
- OpenClaw（已安装）

## 5分钟快速启动

### 1. 克隆项目

```bash
git clone https://github.com/15911188151/qinxd.git
cd qinxd
```

### 2. 启动Docker容器

```bash
# 启动所有服务（PostgreSQL + Redis + Backend + Frontend）
docker-compose up -d

# 查看日志
docker-compose logs -f

# 等待所有服务健康（约30-60秒）
```

### 3. 验证服务

```bash
# 检查PostgreSQL
docker exec drama_postgres psql -U drama_user -d drama_db -c "\dt"

# 检查Redis
docker exec drama_redis redis-cli ping

# 检查后端API
curl http://localhost:8080/api/v1/health

# 检查前端
curl http://localhost:3000
```

### 4. 访问管理台

打开浏览器访问：

- **管理Dashboard**: http://localhost:3000
- **API Swagger文档**: http://localhost:8080/swagger-ui.html
- **后端API基地址**: http://localhost:8080/api/v1

## 本地开发（分离运行）

### 后端开发

```bash
# 进入后端目录
cd backend

# 安装依赖
mvn clean install

# 运行Spring Boot
mvn spring-boot:run

# 或使用IDE运行 DramaApplication.java
```

后端服务将在 `http://localhost:8080` 启动

### 前端开发

```bash
# 进入前端目录
cd frontend

# 安装依赖
npm install

# 启动开发服务器
npm start

# 或构建生产版本
npm run build
```

前端应用将在 `http://localhost:3000` 启动

## 初始配置

### 1. 配置OpenClaw

编辑 `backend/src/main/resources/application.yml`：

```yaml
openClaw:
  apiKey: your_openclaw_api_key
  apiSecret: your_openclaw_api_secret
  apiUrl: http://localhost:8000  # OpenClaw服务地址
```

### 2. 配置平台API（可选）

```yaml
platform:
  douyin:
    clientId: your_douyin_client_id
    clientSecret: your_douyin_client_secret
  xiaohongshu:
    clientId: your_xiaohongshu_client_id
    clientSecret: your_xiaohongshu_client_secret
```

### 3. 配置爬取规则

在管理台 Settings → Crawler 中配置：
- 爬取频率（每天/每周）
- 目标平台（抖音/小红书/B站）
- 内容类型过滤

## 常用命令

### Docker相关

```bash
# 启动所有服务
docker-compose up -d

# 停止所有服务
docker-compose down

# 查看日志
docker-compose logs -f [service_name]

# 进入容器
docker exec -it drama_backend bash

# 重启某个服务
docker-compose restart backend

# 删除所有数据（谨慎）
docker-compose down -v
```

### 数据库操作

```bash
# 连接数据库
docker exec -it drama_postgres psql -U drama_user -d drama_db

# 常用命令
\dt                 # 查看所有表
\d table_name       # 查看表结构
SELECT * FROM users; # 查询数据
```

### Redis操作

```bash
# 连接Redis
docker exec -it drama_redis redis-cli

# 常用命令
KEYS *              # 查看所有键
GET key_name        # 获取值
DEL key_name        # 删除键
FLUSHALL            # 清空所有数据
```

## 故障排查

### 问题1：Docker容器启动失败

```bash
# 查看详细错误日志
docker-compose logs backend

# 确保Docker Desktop正在运行
# 检查端口是否被占用
lsof -i :8080  # 检查8080端口
lsof -i :3000  # 检查3000端口
```

### 问题2：数据库连接失败

```bash
# 检查PostgreSQL是否健康
docker-compose ps

# 查看PostgreSQL日志
docker-compose logs postgres

# 重启PostgreSQL
docker-compose restart postgres
```

### 问题3：前端无法连接后端API

检查 `frontend/.env` 中的 `REACT_APP_API_URL` 是否正确

```bash
# 在前端容器中测试连接
docker exec drama_frontend curl http://backend:8080/api/v1/health
```

## 下一步

1. ✅ 系统已成功运行
2. 📖 阅读 [API文档](./API.md) 了解可用接口
3. 📋 查看 [数据库设计](./DATABASE.md) 了解数据结构
4. 🏗️ 学习 [架构设计](./ARCHITECTURE.md) 了解系统设计
5. 🚀 开始开发和定制功能

## 获取帮助

- 查看日志：`docker-compose logs -f`
- 查看API文档：http://localhost:8080/swagger-ui.html
- 提交Issue或联系我
