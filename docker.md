# Docker Compose：多容器应用示例

## 简介

Docker Compose 是一个用于定义和运行多容器 Docker 应用程序的工具。Haxxnet/Compose-Examples 仓库提供了一系列现成的 Docker Compose 配置，适用于常见的软件栈。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Haxxnet/Compose-Examples |
| 许可证 | MIT |
| 语言 | YAML |
| 工具 | Docker Compose |
| 要求 | Docker Engine 20.10+ |

## Docker Compose 基础

### Compose 文件结构

Docker Compose 文件是一个 YAML 文档，定义了服务、网络和卷。

| 顶级键 | 描述 |
|---------------|-------------|
| version | Compose 文件格式版本 |
| services | 容器定义 |
| volumes | 命名卷定义 |
| networks | 自定义网络定义 |

### 常用服务属性

| 属性 | 描述 |
|----------|-------------|
| image | 要使用的 Docker 镜像 |
| build | 自定义镜像的构建上下文 |
| ports | 端口映射（主机:容器） |
| volumes | 卷挂载 |
| environment | 环境变量 |
| depends_on | 服务启动依赖 |
| restart | 重启策略（always, unless-stopped, on-failure） |
| command | 覆盖默认命令 |
| networks | 服务连接的网络 |

## Web 应用栈

### Nginx + PHP + MySQL

```yaml
version: "3.8"

services:
  web:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./html:/var/www/html
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
    depends_on:
      - php

  php:
    image: php:8.2-fpm
    volumes:
      - ./html:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:8.0
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: app
      MYSQL_USER: appuser
      MYSQL_PASSWORD: apppass
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

## 数据库服务

### PostgreSQL 配合 Adminer

```yaml
version: "3.8"

services:
  postgres:
    image: postgres:15
    environment:
      POSTGRES_DB: myapp
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secret
    volumes:
      - pg_data:/var/lib/postgresql/data
    ports:
      - "5432:5432"

  adminer:
    image: adminer
    ports:
      - "8080:8080"
    depends_on:
      - postgres

volumes:
  pg_data:
```

### MongoDB 配合 Mongo Express

```yaml
version: "3.8"

services:
  mongo:
    image: mongo:6
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: secret
    volumes:
      - mongo_data:/data/db
    ports:
      - "27017:27017"

  mongo-express:
    image: mongo-express
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: secret
      ME_CONFIG_MONGODB_URL: mongodb://admin:secret@mongo:27017
    ports:
      - "8081:8081"
    depends_on:
      - mongo

volumes:
  mongo_data:
```

## 监控栈

### Prometheus + Grafana

```yaml
version: "3.8"

services:
  prometheus:
    image: prom/prometheus
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prom_data:/prometheus
    ports:
      - "9090:9090"

  grafana:
    image: grafana/grafana
    environment:
      GF_SECURITY_ADMIN_PASSWORD: admin
    volumes:
      - grafana_data:/var/lib/grafana
    ports:
      - "3000:3000"
    depends_on:
      - prometheus

  node-exporter:
    image: prom/node-exporter
    ports:
      - "9100:9100"

volumes:
  prom_data:
  grafana_data:
```

## 媒体服务

### Jellyfin 媒体服务器

```yaml
version: "3.8"

services:
  jellyfin:
    image: jellyfin/jellyfin
    ports:
      - "8096:8096"
    volumes:
      - ./config:/config
      - ./cache:/cache
      - /path/to/media:/media
    restart: unless-stopped
```

### Nextcloud

```yaml
version: "3.8"

services:
  nextcloud:
    image: nextcloud
    ports:
      - "8080:80"
    volumes:
      - nextcloud_data:/var/www/html
    environment:
      MYSQL_HOST: db
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: secret
    depends_on:
      - db

  db:
    image: mariadb:10
    environment:
      MYSQL_ROOT_PASSWORD: rootsecret
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: secret
    volumes:
      - db_data:/var/lib/mysql

volumes:
  nextcloud_data:
  db_data:
```

## 消息队列

### RabbitMQ

```yaml
version: "3.8"

services:
  rabbitmq:
    image: rabbitmq:3-management
    ports:
      - "5672:5672"
      - "15672:15672"
    environment:
      RABBITMQ_DEFAULT_USER: admin
      RABBITMQ_DEFAULT_PASS: secret
    volumes:
      - rabbit_data:/var/lib/rabbitmq

volumes:
  rabbit_data:
```

### Redis

```yaml
version: "3.8"

services:
  redis:
    image: redis:7-alpine
    ports:
      - "6379:6379"
    volumes:
      - redis_data:/data
    command: redis-server --appendonly yes

  redis-commander:
    image: rediscommander/redis-commander
    environment:
      REDIS_HOSTS: local:redis:6379
    ports:
      - "8081:8081"
    depends_on:
      - redis

volumes:
  redis_data:
```

## 常用命令

| 命令 | 描述 |
|---------|-------------|
| docker compose up | 启动所有服务 |
| docker compose up -d | 以分离模式启动 |
| docker compose down | 停止并移除容器 |
| docker compose down -v | 同时移除卷 |
| docker compose logs | 查看日志 |
| docker compose logs -f | 跟踪日志输出 |
| docker compose ps | 列出运行中的服务 |
| docker compose build | 构建镜像 |
| docker compose pull | 拉取最新镜像 |
| docker compose restart | 重启服务 |
| docker compose exec SERVICE CMD | 在服务中运行命令 |

## 最佳实践

| 实践 | 原因 |
|----------|--------|
| 使用命名卷 | 在容器重启间持久化数据 |
| 设置重启策略 | 确保服务从崩溃中恢复 |
| 使用环境文件 | 将密钥从 compose 文件中分离 |
| 固定镜像版本 | 防止意外更新 |
| 使用 depends_on | 控制启动顺序 |
| 使用健康检查 | 验证服务就绪状态 |
| 限制资源 | 设置 CPU 和内存限制 |

## 健康检查

```yaml
services:
  web:
    image: nginx
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

## 环境文件

将敏感配置存储在 `.env` 文件中，而不是 compose 文件中。

```env
POSTGRES_DB=myapp
POSTGRES_USER=admin
POSTGRES_PASSWORD=secret
```

在 compose 文件中引用变量：

```yaml
services:
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: ${POSTGRES_DB}
      POSTGRES_USER: ${POSTGRES_USER}
      POSTGRES_PASSWORD: ${POSTGRES_PASSWORD}
```

## 结论

Docker Compose 简化了多容器应用程序的管理。Haxxnet/Compose-Recipes 中的示例为常见的软件栈提供了现成的配置，减少了设置时间并确保了一致的部署。
