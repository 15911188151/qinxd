# AI Video Generation Platform

基于OpenClaw的AI短剧生成与多平台发布系统

## 项目概述

这是一个完整的AI短剧生成和发布平台，集成以下功能：

- 🎬 **自动内容爬取**：每天抓取最新热门短剧类型
- 🤖 **AI生成引擎**：使用OpenClaw自动生成短剧
- 📱 **多平台发布**：发布到抖音、小红书等主流平台
- 📊 **智能管理台**：实时监控和数据分析

## 架构

```
┌─────────────────────────────────────────┐
│        React前端 - 管理Dashboard        │
└──────────────────┬──────────────────────┘
                   │
        ┌──────────┼──────────┐
        ▼          ▼          ▼
┌─────────────┐ ┌────────┐ ┌────────┐
│ 内容爬取    │ │AI生成  │ │平台发布│
│ 模块        │ │引擎    │ │模块    │
└──────┬──────┘ └───┬────┘ └────┬───┘
       │            │           │
       └────────┬───┴───────┬───┘
                ▼           ▼
         ┌──────────────┬──────────────┐
         │  PostgreSQL  │   Redis      │
         │  数据库      │   缓存队列   │
         └──────────────┴──────────────┘
```

## 技术栈

### 后端
- Java 11+
- Spring Boot 2.7+
- Spring Data JPA
- PostgreSQL
- Redis
- Maven

### 前端
- React 18
- Ant Design Pro
- Echarts（数据可视化）
- Axios

### 部署
- Docker
- Docker Compose

## 快速开始

### 前置条件
- Docker Desktop
- Java 11+
- Node.js 14+
- OpenClaw已安装

### 本地开发运行

```bash
# 1. 克隆项目
git clone https://github.com/15911188151/qinxd.git
cd qinxd

# 2. 启动所有服务（Docker）
docker-compose up -d

# 3. 后端启动
cd backend
mvn clean install
mvn spring-boot:run

# 4. 前端启动
cd frontend
npm install
npm start
```

### 访问

- 前端管理台: http://localhost:3000
- 后端API: http://localhost:8080
- API文档: http://localhost:8080/swagger-ui.html

## 项目结构

```
ai-video/
├── backend/                    # Java后端
│   ├── src/
│   │   ├── main/java/com/drama/
│   │   │   ├── config/         # 配置类
│   │   │   ├── controller/     # API控制器
│   │   │   ├── service/        # 业务逻辑
│   │   │   ├── entity/         # 数据实体
│   │   │   ├── repository/     # 数据访问
│   │   │   ├── dto/            # 数据传输对象
│   │   │   ├── mapper/         # 对象映射
│   │   │   ├── utils/          # 工具类
│   │   │   └── DramaApplication.java
│   │   ├── resources/
│   │   │   ├── application.yml
│   │   │   └── db/migration/
│   ├── pom.xml
│   └── Dockerfile
├── frontend/                   # React前端
│   ├── src/
│   │   ├── components/         # React组件
│   │   ├── pages/              # 页面
│   │   ├── services/           # API调用
│   │   ├── styles/
│   │   └── App.jsx
│   ├── package.json
│   └── Dockerfile
├── docker-compose.yml          # Docker编排
├── docs/                       # 文档
│   ├── API.md
│   ├── DATABASE.md
│   └── DEPLOYMENT.md
└── README.md
```

## 核心功能

### 1. 内容爬取模块
- 自动定时爬取热门短剧
- 支持多个数据源
- 热度分析和排序

### 2. AI生成模块
- OpenClaw集成
- 自动脚本生成
- 视频合成
- 字幕配音生成

### 3. 平台发布模块
- 抖音API集成
- 小红书API集成
- 多账号管理
- 智能发布策略

### 4. 管理Dashboard
- 实时数据监控
- 视频库管理
- 账号管理
- 收益统计

## API文档

详见 `docs/API.md`

## 数据库设计

详见 `docs/DATABASE.md`

## 部署指南

详见 `docs/DEPLOYMENT.md`

## 配置说明

### 后端配置 (backend/src/main/resources/application.yml)

```yaml
spring:
  datasource:
    url: jdbc:postgresql://localhost:5432/drama_db
    username: drama_user
    password: drama_pass
  jpa:
    hibernate:
      ddl-auto: update
  
redis:
  host: localhost
  port: 6379

openClaw:
  apiKey: your_openclaw_api_key
  apiSecret: your_openclaw_api_secret

platform:
  douyin:
    clientId: your_douyin_client_id
    clientSecret: your_douyin_client_secret
  xiaohongshu:
    clientId: your_xiaohongshu_client_id
    clientSecret: your_xiaohongshu_client_secret
```

## 常见问题

### Q: 如何配置OpenClaw？
A: 在 `application.yml` 中配置 `openClaw` 部分的API Key和Secret

### Q: 如何连接抖音/小红书？
A: 需要在各平台开发者后台申请API权限，然后配置到 `platform` 部分

### Q: 如何启动定时爬取任务？
A: 系统自动启动，可在Dashboard中配置爬取频率和规则

## 贡献指南

欢迎提交Issue和Pull Request！

## License

MIT

## 联系方式

有任何问题，欢迎提Issue或联系我
