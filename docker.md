# Docker 容器化

> 本文档整合了以下源文件：compose.md, docker.md

---

## 来源：compose.md

真实世界 Docker Compose 配置的综合教程，涵盖常见服务。通过示例学习生产就绪的 compose 文件。

## 目录

- [Docker Compose 基础](#docker-compose-基础)
- [Web 服务器](#web-服务器)
- [数据库](#数据库)
- [监控](#监控)
- [媒体服务](#媒体服务)
- [通信](#通信)
- [网络](#网络)
- [卷](#卷)
- [环境变量](#环境变量)
- [反向代理设置](#反向代理设置)

---

## Docker Compose 基础

### 什么是 Docker Compose

Docker Compose 是用于定义和运行多容器 Docker 应用的工具。单个 YAML 文件描述所有服务、网络和卷。

### Compose 文件结构

```yaml
version: "3.8"

services:
  service-name:
    image: image-name:tag
    container_name: custom-name
    ports:
      - "host:container"
    volumes:
      - host-path:container-path
    environment:
      - KEY=VALUE
    networks:
      - network-name
    restart: unless-stopped

networks:
  network-name:
    driver: bridge

volumes:
  volume-name:
```

### 常用命令

| 命令 | 用途 |
|---------|---------|
| `docker compose up -d` | 后台启动所有服务 |
| `docker compose down` | 停止并移除所有服务 |
| `docker compose ps` | 列出运行中的服务 |
| `docker compose logs -f` | 跟踪所有服务日志 |
| `docker compose logs service` | 特定服务的日志 |
| `docker compose restart` | 重启所有服务 |
| `docker compose build` | 从 Dockerfile 构建镜像 |
| `docker compose pull` | 拉取最新镜像 |
| `docker compose exec service bash` | 在容器中打开 shell |
| `docker compose config` | 验证并查看 compose 文件 |
| `docker compose top` | 显示运行中的进程 |

### Compose 文件版本参考

| 版本 | Docker Engine | 特性 |
|---------|--------------|----------|
| 3.0 | 1.13+ | 基本 compose 特性 |
| 3.4 | 17.09+ | target、isolation |
| 3.6 | 17.12+ | secrets、tmpfs size |
| 3.8 | 19.03+ | 最新 v3 特性 |
| 最新（无版本） | 20.10+ | Compose Specification |

---

## Web 服务器

### Nginx

```yaml
version: "3.8"

services:
  nginx:
    image: nginx:alpine
    container_name: nginx
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./html:/usr/share/nginx/html:ro
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./certs:/etc/nginx/certs:ro
    restart: unless-stopped
```

### Apache with PHP

```yaml
version: "3.8"

services:
  web:
    image: php:8.2-apache
    container_name: php-apache
    ports:
      - "80:80"
    volumes:
      - ./src:/var/www/html
    environment:
      - APACHE_DOCUMENT_ROOT=/var/www/html
    restart: unless-stopped
```

### Node.js 应用

```yaml
version: "3.8"

services:
  app:
    build: .
    container_name: node-app
    ports:
      - "3000:3000"
    volumes:
      - .:/app
      - /app/node_modules
    environment:
      - NODE_ENV=production
      - DATABASE_URL=postgres://user:pass@db:5432/mydb
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=pass
      - POSTGRES_DB=mydb
    restart: unless-stopped

volumes:
  pgdata:
```

### Web 服务器对比

| 服务器 | 镜像 | 最适合 | 配置位置 |
|--------|-------|----------|-----------------|
| Nginx | nginx:alpine | 反向代理、静态文件 | /etc/nginx/ |
| Apache | httpd:alpine | PHP 应用、.htaccess | /usr/local/apache2/ |
| Caddy | caddy | 自动 HTTPS | /etc/caddy/ |
| Traefik | traefik | 动态反向代理 | /etc/traefik/ |

---

## 数据库

### PostgreSQL

```yaml
version: "3.8"

services:
  postgres:
    image: postgres:15-alpine
    container_name: postgres
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: secretpassword
      POSTGRES_DB: myapp
    restart: unless-stopped

  pgadmin:
    image: dpage/pgadmin4:latest
    container_name: pgadmin
    ports:
      - "5050:80"
    environment:
      PGADMIN_DEFAULT_EMAIL: admin@example.com
      PGADMIN_DEFAULT_PASSWORD: admin
    depends_on:
      - postgres
    restart: unless-stopped

volumes:
  pgdata:
```

### MySQL

```yaml
version: "3.8"

services:
  mysql:
    image: mysql:8.0
    container_name: mysql
    ports:
      - "3306:3306"
    volumes:
      - mysqldata:/var/lib/mysql
      - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: myapp
      MYSQL_USER: user
      MYSQL_PASSWORD: password
    restart: unless-stopped

  phpmyadmin:
    image: phpmyadmin:latest
    container_name: phpmyadmin
    ports:
      - "8080:80"
    environment:
      PMA_HOST: mysql
      PMA_PORT: 3306
    depends_on:
      - mysql
    restart: unless-stopped

volumes:
  mysqldata:
```

### MongoDB

```yaml
version: "3.8"

services:
  mongo:
    image: mongo:6
    container_name: mongodb
    ports:
      - "27017:27017"
    volumes:
      - mongodata:/data/db
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    restart: unless-stopped

  mongo-express:
    image: mongo-express:latest
    container_name: mongo-express
    ports:
      - "8081:8081"
    environment:
      ME_CONFIG_MONGODB_ADMINUSERNAME: admin
      ME_CONFIG_MONGODB_ADMINPASSWORD: password
      ME_CONFIG_MONGODB_URL: mongodb://admin:password@mongo:27017/
    depends_on:
      - mongo
    restart: unless-stopped

volumes:
  mongodata:
```

### Redis

```yaml
version: "3.8"

services:
  redis:
    image: redis:7-alpine
    container_name: redis
    ports:
      - "6379:6379"
    volumes:
      - redisdata:/data
    command: redis-server --appendonly yes --requirepass password
    restart: unless-stopped

  redis-commander:
    image: rediscommander/redis-commander:latest
    container_name: redis-commander
    ports:
      - "8082:8081"
    environment:
      REDIS_HOSTS: local:redis:6379:0:password
    depends_on:
      - redis
    restart: unless-stopped

volumes:
  redisdata:
```

### 数据库对比

| 数据库 | 镜像 | 端口 | 管理工具 | 最适合 |
|----------|-------|------|------------|----------|
| PostgreSQL | postgres:15-alpine | 5432 | pgAdmin | 复杂查询、JSON |
| MySQL | mysql:8.0 | 3306 | phpMyAdmin | Web 应用 |
| MongoDB | mongo:6 | 27017 | Mongo Express | 文档存储 |
| Redis | redis:7-alpine | 6379 | Redis Commander | 缓存、队列 |
| MariaDB | mariadb:10 | 3306 | phpMyAdmin | MySQL 兼容 |
| SQLite | 不推荐在 Docker 中使用 | - | - | 单文件数据库 |

---

## 监控

### Prometheus 和 Grafana

```yaml
version: "3.8"

services:
  prometheus:
    image: prom/prometheus:latest
    container_name: prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - promdata:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
    restart: unless-stopped

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    ports:
      - "3000:3000"
    volumes:
      - grafdata:/var/lib/grafana
    environment:
      GF_SECURITY_ADMIN_PASSWORD: admin
    depends_on:
      - prometheus
    restart: unless-stopped

  node-exporter:
    image: prom/node-exporter:latest
    container_name: node-exporter
    ports:
      - "9100:9100"
    restart: unless-stopped

volumes:
  promdata:
  grafdata:
```

### ELK Stack（轻量版）

```yaml
version: "3.8"

services:
  elasticsearch:
    image: elasticsearch:8.8.0
    container_name: elasticsearch
    ports:
      - "9200:9200"
    environment:
      - discovery.type=single-node
      - xpack.security.enabled=false
      - "ES_JAVA_OPTS=-Xms512m -Xmx512m"
    volumes:
      - esdata:/usr/share/elasticsearch/data
    restart: unless-stopped

  kibana:
    image: kibana:8.8.0
    container_name: kibana
    ports:
      - "5601:5601"
    environment:
      ELASTICSEARCH_URL: http://elasticsearch:9200
    depends_on:
      - elasticsearch
    restart: unless-stopped

volumes:
  esdata:
```

### 监控方案对比

| 方案 | 组件 | 最适合 | 资源使用 |
|-------|-----------|----------|----------------|
| Prometheus + Grafana | 指标、仪表板 | 基础设施指标 | 中等 |
| ELK Stack | 日志、搜索 | 日志分析 | 高 |
| Loki + Grafana | 日志、仪表板 | 轻量日志 | 低 |
| Uptime Kuma | 可用性监控 | 服务可用性 | 极低 |
| Netdata | 实时指标 | 快速概览 | 低 |

---

## 媒体服务

### Plex Media Server

```yaml
version: "3.8"

services:
  plex:
    image: plexinc/pms-docker:latest
    container_name: plex
    ports:
      - "32400:32400"
    volumes:
      - ./config:/config
      - /path/to/movies:/movies
      - /path/to/tv:/tv
      - /path/to/music:/music
    environment:
      PLEX_CLAIM: claim-xxxx
      TZ: America/New_York
    restart: unless-stopped
```

### Jellyfin（开源替代）

```yaml
version: "3.8"

services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    container_name: jellyfin
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
    image: nextcloud:latest
    container_name: nextcloud
    ports:
      - "8080:80"
    volumes:
      - nextcloud:/var/www/html
      - ./data:/var/www/html/data
    environment:
      MYSQL_HOST: db
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: password
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: mariadb:10
    volumes:
      - dbdata:/var/lib/mysql
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: nextcloud
      MYSQL_USER: nextcloud
      MYSQL_PASSWORD: password
    restart: unless-stopped

volumes:
  nextcloud:
  dbdata:
```

### 媒体服务对比

| 服务 | 类型 | 许可证 | 最适合 |
|---------|------|---------|----------|
| Plex | 媒体服务器 | 专有 | 精美 UI、智能电视应用 |
| Jellyfin | 媒体服务器 | 开源 | 免费、社区驱动 |
| Emby | 媒体服务器 | 免费增值 | 中间选择 |
| Navidrome | 音乐服务器 | 开源 | 音乐流媒体 |
| Immich | 照片管理 | 开源 | Google Photos 替代 |

---

## 通信

### Matrix with Element

```yaml
version: "3.8"

services:
  synapse:
    image: matrixdotorg/synapse:latest
    container_name: synapse
    ports:
      - "8008:8008"
    volumes:
      - ./synapse/data:/data
    environment:
      SYNAPSE_SERVER_NAME: matrix.example.com
      SYNAPSE_REPORT_STATS: "no"
    restart: unless-stopped

  element:
    image: vectorim/element-web:latest
    container_name: element
    ports:
      - "8080:80"
    volumes:
      - ./element/config.json:/app/config.json:ro
    restart: unless-stopped
```

### Rocket.Chat

```yaml
version: "3.8"

services:
  rocketchat:
    image: rocket.chat:latest
    container_name: rocketchat
    ports:
      - "3000:3000"
    environment:
      MONGO_URL: mongodb://mongo:27017/rocketchat
      ROOT_URL: http://localhost:3000
    depends_on:
      - mongo
    restart: unless-stopped

  mongo:
    image: mongo:5
    volumes:
      - mongodata:/data/db
    restart: unless-stopped

volumes:
  mongodata:
```

### 通信服务对比

| 服务 | 类型 | 许可证 | 特性 |
|---------|------|---------|----------|
| Matrix/Element | 聊天 | 开源 | 联邦、端到端加密 |
| Rocket.Chat | 聊天 | 开源 | 线程、视频通话 |
| Mattermost | 聊天 | 开源 | Slack 替代 |
| Zulip | 聊天 | 开源 | 线程模型 |
| Gitea | Git 托管 | 开源 | 轻量 GitHub |

---

## 网络

### Docker Compose 网络

```yaml
version: "3.8"

services:
  web:
    image: nginx:alpine
    networks:
      - frontend

  app:
    image: node:18-alpine
    networks:
      - frontend
      - backend

  db:
    image: postgres:15-alpine
    networks:
      - backend

networks:
  frontend:
    driver: bridge
  backend:
    driver: bridge
    internal: true  # No external access
```

### 网络驱动

| 驱动 | 描述 | 用例 |
|--------|-------------|----------|
| bridge | 默认隔离网络 | 单主机多容器 |
| host | 使用主机网络栈 | 需要高性能 |
| overlay | 多主机网络 | Docker Swarm |
| macvlan | 分配 MAC 地址 | 显示为物理设备 |
| none | 无网络 | 隔离容器 |

### 网络配置

| 选项 | 描述 |
|--------|-------------|
| `internal: true` | 无外部互联网访问 |
| `driver: bridge` | 标准容器网络 |
| `ipam` | IP 地址管理 |
| `external: true` | 使用已存在的网络 |

---

## 卷

### 卷类型

```yaml
version: "3.8"

services:
  app:
    image: myapp
    volumes:
      # 命名卷（持久化）
      - appdata:/app/data
      # 绑定挂载（开发）
      - ./src:/app/src
      # 只读绑定挂载
      - ./config.json:/app/config.json:ro
      # tmpfs（仅内存）
      - type: tmpfs
        target: /tmp
        tmpfs:
          size: 100000000

volumes:
  appdata:
```

### 卷对比

| 类型 | 持久化 | 性能 | 用例 |
|------|-------------|-------------|----------|
| 命名卷 | 是 | 好 | 数据库数据 |
| 绑定挂载 | 取决于主机 | 不定 | 开发代码 |
| tmpfs | 否（仅 RAM） | 最快 | 临时文件 |

### 备份卷

```bash
# 备份卷
docker run --rm -v myvolume:/source -v $(pwd):/backup alpine \
  tar czf /backup/myvolume-backup.tar.gz -C /source .

# 恢复卷
docker run --rm -v myvolume:/target -v $(pwd):/backup alpine \
  tar xzf /backup/myvolume-backup.tar.gz -C /target
```

---

## 环境变量

### 设置变量的方法

```yaml
version: "3.8"

services:
  app:
    image: myapp
    # 方法 1：内联
    environment:
      - DB_HOST=localhost
      - DB_PORT=5432
    # 方法 2：从文件
    env_file:
      - .env
      - .env.production
```

### 环境文件格式

```bash
# .env 文件
DB_HOST=localhost
DB_PORT=5432
DB_USER=admin
DB_PASSWORD=secretpassword
DB_NAME=myapp

# 支持注释
APP_ENV=production
DEBUG=false
```

### 变量替换

```yaml
version: "3.8"

services:
  app:
    image: myapp:${APP_VERSION:-latest}
    ports:
      - "${APP_PORT:-3000}:3000"
    environment:
      - DB_HOST=${DB_HOST:?Database host required}
```

### 环境变量最佳实践

| 实践 | 描述 |
|----------|-------------|
| 使用 .env 文件 | 将密钥从 compose 文件中分离 |
| 将 .env 加入 .gitignore | 永远不要提交密钥 |
| 提供默认值 | 使用 `${VAR:-default}` 语法 |
| 使用 Docker secrets | 用于生产敏感数据 |
| 记录变量 | 包含 .env.example |

---

## 反向代理设置

### Traefik（自动 HTTPS）

```yaml
version: "3.8"

services:
  traefik:
    image: traefik:v2.10
    container_name: traefik
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./traefik.yml:/etc/traefik/traefik.yml
      - traefik-certs:/certs
    restart: unless-stopped

  whoami:
    image: traefik/whoami
    container_name: whoami
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.whoami.rule=Host(`whoami.example.com`)"
      - "traefik.http.routers.whoami.tls.certresolver=letsencrypt"
    restart: unless-stopped

volumes:
  traefik-certs:
```

### Nginx 反向代理

```yaml
version: "3.8"

services:
  nginx:
    image: nginx:alpine
    container_name: nginx-proxy
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - ./certs:/etc/nginx/certs:ro
    restart: unless-stopped

  app:
    image: myapp
    container_name: app
    # 不暴露端口 - 通过 nginx 访问
    restart: unless-stopped
```

### Nginx 代理配置

```nginx
# nginx.conf
events {
    worker_connections 1024;
}

http {
    upstream app {
        server app:3000;
    }

    server {
        listen 80;
        server_name example.com;
        return 301 https://$host$request_uri;
    }

    server {
        listen 443 ssl;
        server_name example.com;

        ssl_certificate /etc/nginx/certs/cert.pem;
        ssl_certificate_key /etc/nginx/certs/key.pem;

        location / {
            proxy_pass http://app;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```

### 反向代理对比

| 代理 | 自动 HTTPS | 配置 | Docker 集成 | 最适合 |
|-------|-----------|--------|-------------------|----------|
| Traefik | 是（Let's Encrypt） | Labels | 优秀 | 动态服务 |
| Nginx | 手动 | 文件 | 好 | 静态配置 |
| Caddy | 是（自动） | 文件 | 好 | 简单设置 |
| HAProxy | 否 | 文件 | 好 | 负载均衡 |

---

## 生产建议

### 健康检查

```yaml
version: "3.8"

services:
  app:
    image: myapp
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
    restart: unless-stopped
```

### 资源限制

```yaml
version: "3.8"

services:
  app:
    image: myapp
    deploy:
      resources:
        limits:
          cpus: '0.5'
          memory: 512M
        reservations:
          cpus: '0.25'
          memory: 256M
    restart: unless-stopped
```

### 日志配置

```yaml
version: "3.8"

services:
  app:
    image: myapp
    logging:
      driver: json-file
      options:
        max-size: "10m"
        max-file: "3"
    restart: unless-stopped
```

---

## 总结

Docker Compose 让定义和运行多容器应用变得简单。从简单的单服务配置开始，然后逐步构建包含多个数据库、监控和反向代理的复杂方案。

关键原则：
- 始终使用命名卷存储持久数据
- 在生产环境设置资源限制
- 使用健康检查确保服务就绪
- 将密钥从 compose 文件中分离
- 使用反向代理处理 HTTPS


---

## 来源：docker.md

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


---
