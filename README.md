# EasyChat - 大型景区内部通讯平台

一个基于 Spring Boot + Netty + WebSocket 的实时通讯平台，专为大型景区内部管理人员设计的企业级即时通讯解决方案。

## 项目概述

EasyChat 是一个功能完整的内部通讯系统，支持实时消息传输、群组管理、用户管理、文件传输等核心功能。采用现代化技术栈构建，确保高并发、高可靠性的通讯体验。

## 核心功能

### 📱 实时通讯
- 基于 WebSocket 的实时消息推送
- 支持文本、图片、文件等多种消息类型
- 消息状态追踪（已发送、已送达、已读）
- 离线消息存储和推送

### 👥 群组管理
- 群组创建、编辑、解散
- 群组成员管理
- 群组公告发布
- 群组权限控制

### 👤 用户管理
- 用户注册、登录、资料管理
- 好友添加和管理
- 用户状态管理
- 管理员权限体系

### 📎 文件传输
- 支持多种文件格式上传下载
- 文件大小限制控制
- 临时文件清理机制

### 🔧 系统管理
- 应用版本更新管理
- 系统设置配置
- 用户美化头像管理
- 数据统计和监控

## 技术架构

### 后端技术栈
- **Spring Boot 2.6.1** - 主框架
- **Netty 4.1.50** - 高性能网络通信框架
- **WebSocket** - 实时通讯协议
- **MyBatis 1.3.2** - 数据持久化框架
- **MySQL 8.0** - 关系型数据库
- **Redis** - 缓存和会话管理
- **Redisson** - 分布式锁和发布订阅

### 核心组件
- **WebSocket 服务** - 处理实时通讯连接
- **消息处理器** - 消息路由和分发
- **文件管理** - 文件上传下载处理
- **用户认证** - JWT Token 认证
- **缓存管理** - Redis 缓存优化

## 项目结构

```
com.easychat/
├── annotation/          # 自定义注解
├── aspect/             # AOP 切面处理
├── controller/         # REST API 控制器
├── entity/            # 实体类
│   ├── config/        # 配置类
│   ├── constants/     # 常量定义
│   ├── dto/          # 数据传输对象
│   ├── enums/        # 枚举类型
│   ├── po/           # 持久化对象
│   ├── query/        # 查询参数
│   └── vo/           # 视图对象
├── exception/         # 异常处理
├── mappers/          # MyBatis 映射器
├── redis/            # Redis 配置和工具
├── service/          # 业务逻辑层
├── utils/            # 工具类
└── websocket/        # WebSocket 处理
```

## 快速开始

### 环境要求
- JDK 1.8+
- Maven 3.6+
- MySQL 8.0+
- Redis 6.0+

### 安装步骤

1. **克隆项目**
```bash
git clone <repository-url>
cd easychat
```

2. **配置数据库**
```sql
CREATE DATABASE easychat DEFAULT CHARSET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

3. **修改配置文件**
编辑 `src/main/resources/application.properties`：
```properties
# 数据库配置
spring.datasource.url=jdbc:mysql://localhost:3306/easychat?serverTimezone=GMT%2B8&useUnicode=true&characterEncoding=utf8
spring.datasource.username=your_username
spring.datasource.password=your_password

# Redis配置
spring.redis.host=127.0.0.1
spring.redis.port=6379

# 项目目录
project.folder=/path/to/your/project
```

4. **编译运行**
```bash
mvn clean compile
mvn spring-boot:run
```

5. **访问应用**
- HTTP API: http://localhost:5050/api
- WebSocket: ws://localhost:5051

## API 文档

### 用户相关
- `POST /api/account/register` - 用户注册
- `POST /api/account/login` - 用户登录
- `GET /api/userInfo/getUserInfo` - 获取用户信息
- `POST /api/userInfo/updateUserInfo` - 更新用户信息

### 聊天相关
- `POST /api/chat/sendMessage` - 发送消息
- `GET /api/chat/loadMessage` - 加载聊天记录
- `POST /api/chat/uploadFile` - 上传文件

### 群组相关
- `POST /api/group/saveGroup` - 创建/编辑群组
- `POST /api/group/loadGroup` - 获取群组列表
- `POST /api/group/addOrRemoveGroupUser` - 添加/移除群组成员

## 部署指南

### Docker 部署
```dockerfile
FROM openjdk:8-jre-alpine
COPY target/easychat-1.0.jar app.jar
EXPOSE 5050 5051
ENTRYPOINT ["java", "-jar", "/app.jar"]
```

### 生产环境配置
- 配置 Nginx 反向代理
- 设置 SSL 证书
- 配置 Redis 集群
- 数据库主从配置

## 性能特性

- **高并发支持** - 基于 Netty 的异步非阻塞架构
- **消息可靠性** - Redis 发布订阅机制确保消息送达
- **水平扩展** - 支持多实例部署和负载均衡
- **缓存优化** - Redis 缓存热点数据，提升响应速度

## 安全特性

- JWT Token 认证机制
- 密码加密存储
- 文件上传安全检查
- SQL 注入防护
- XSS 攻击防护

---

**EasyChat** - 让景区内部沟通更高效！