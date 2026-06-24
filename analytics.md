# 数据分析与仪表板

> 本文档整合了以下源文件：analytics.md, dashboard.md, dash.md

---

## 来源：analytics.md

## 简介

Apache Superset 是一款开源数据探索和可视化平台。它提供基于 Web 的界面，用于创建交互式仪表板、探索数据集和执行基于 SQL 的分析。

| 特性 | 描述 |
|---------|-------------|
| 可视化 | 多种图表类型和可视化方式 |
| SQL IDE | 内置 SQL 编辑器用于数据探索 |
| 仪表板 | 交互式仪表板创建和分享 |
| 数据源 | 连接各种数据库和数据仓库 |
| 安全 | 基于角色的访问控制和行级安全 |

## 架构

### 系统组件

| 组件 | 用途 |
|-----------|---------|
| Web server | 基于 Flask 的应用服务器 |
| Metadata database | 存储 Superset 配置（PostgreSQL） |
| Cache | Redis 用于缓存查询结果 |
| Message broker | Celery 配合 Redis/RabbitMQ 处理异步任务 |
| Data databases | 用于分析的外部数据源 |

### 支持的数据库

| 数据库 | 连接器 | 备注 |
|----------|-----------|-------|
| PostgreSQL | psycopg2 | 推荐用于元数据 |
| MySQL | mysqlclient | 常见数据源 |
| SQLite | 内置 | 开发和测试 |
| Amazon Redshift | redshift_connector | 数据仓库 |
| Google BigQuery | pybigquery | 云分析 |
| Snowflake | snowflake-connector | 云数据仓库 |
| Apache Druid | pydruid | 实时分析 |
| ClickHouse | clickhouse-connect | 列式 OLAP |

## 安装

### Docker 部署

```bash
# 克隆仓库
git clone https://github.com/apache/superset.git
cd superset

# 使用 Docker Compose 启动
docker-compose -f docker-compose-non-dev.yml up -d
```

### Docker Compose

```yaml
version: "3.8"
services:
  superset:
    image: apache/superset:latest
    container_name: superset
    ports:
      - "8088:8088"
    environment:
      - SUPERSET_SECRET_KEY=your_secret_key
      - SQLALCHEMY_DATABASE_URI=postgresql://superset:password@db:5432/superset
    depends_on:
      - db
      - redis
    restart: unless-stopped

  db:
    image: postgres:15
    container_name: superset-db
    environment:
      - POSTGRES_USER=superset
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=superset
    volumes:
      - postgres_data:/var/lib/postgresql/data
    restart: unless-stopped

  redis:
    image: redis:7
    container_name: superset-redis
    restart: unless-stopped

volumes:
  postgres_data:
```

### 初始设置

```bash
# 初始化数据库
superset db upgrade

# 创建管理员用户
superset fab create-admin \
  --username admin \
  --firstname Admin \
  --lastname User \
  --email admin@example.com \
  --password admin

# 初始化角色和权限
superset init
```

## 数据源

### 连接数据库

| 步骤 | 操作 |
|------|--------|
| 1 | 导航到数据 > 数据库 |
| 2 | 点击 + 数据库 |
| 3 | 选择数据库类型 |
| 4 | 输入连接参数 |
| 5 | 测试连接 |
| 6 | 保存配置 |

### 连接 URI 格式

| 数据库 | URI 格式 |
|----------|-----------|
| PostgreSQL | `postgresql://user:pass@host:5432/db` |
| MySQL | `mysql://user:pass@host:3306/db` |
| SQLite | `sqlite:///path/to/database.db` |
| Redshift | `redshift+psycopg2://user:pass@host:5439/db` |
| BigQuery | `bigquery://project/dataset` |

### 添加数据集

| 方式 | 描述 |
|--------|-------------|
| 表 | 选择现有数据库表 |
| 虚拟表 | SQL 查询作为数据集 |
| 上传 | 上传 CSV 或 Excel 文件 |

## 图表

### 图表类型

| 类别 | 图表 |
|----------|--------|
| 折线图 | 折线图、时间序列、多线 |
| 柱状图 | 柱状图、堆叠柱状图、分组柱状图 |
| 面积图 | 面积图、堆叠面积图 |
| 饼图 | 饼图、环形图 |
| 散点图 | 散点图、气泡图 |
| 表格 | 数据表、透视表 |
| 地理 | 世界地图、国家地图、deck.gl |
| 热力图 | 日历热力图、热力图 |
| 直方图 | 分布直方图 |
| 箱线图 | 统计箱线图 |

### 创建图表

| 步骤 | 操作 |
|------|--------|
| 1 | 导航到图表 > + 图表 |
| 2 | 选择数据集 |
| 3 | 选择图表类型 |
| 4 | 配置指标和维度 |
| 5 | 应用筛选器 |
| 6 | 自定义外观 |
| 7 | 保存图表 |

### 指标

| 指标类型 | 描述 | 示例 |
|------------|-------------|---------|
| Count | 行计数 | `COUNT(*)` |
| Sum | 值求和 | `SUM(sales)` |
| Average | 平均值 | `AVG(price)` |
| Min/Max | 最小值或最大值 | `MAX(revenue)` |
| Custom SQL | 自定义表达式 | `SUM(profit) / SUM(revenue)` |

### 维度

| 维度类型 | 描述 | 示例 |
|---------------|-------------|---------|
| Column | 直接列引用 | `category` |
| Time | 基于时间的分组 | `order_date`（按月） |
| SQL expression | 自定义表达式 | `CONCAT(first_name, ' ', last_name)` |

## 仪表板

### 创建仪表板

| 步骤 | 操作 |
|------|--------|
| 1 | 导航到仪表板 |
| 2 | 点击 + 仪表板 |
| 3 | 从已保存图表中添加 |
| 4 | 使用网格排列布局 |
| 5 | 添加筛选器和参数 |
| 6 | 配置自动刷新 |
| 7 | 发布仪表板 |

### 仪表板组件

| 组件 | 描述 |
|-----------|-------------|
| Charts | 来自已保存图表的可视化 |
| Markdown | 文本和文档 |
| Divider | 可视分隔符 |
| Filter bar | 所有图表的交互式筛选器 |
| Header | 仪表板标题和元数据 |

### 仪表板筛选器

| 筛选器类型 | 描述 |
|------------|-------------|
| 时间范围 | 按日期/时间段筛选 |
| 列筛选器 | 按特定列值筛选 |
| 数值筛选器 | 按数值范围筛选 |
| 自定义筛选器 | 基于 SQL 的自定义筛选器 |

## SQL IDE

### SQL Lab 功能

| 功能 | 描述 |
|---------|-------------|
| 查询编辑器 | 语法高亮的 SQL 编辑器 |
| 结果表 | 表格格式的查询结果 |
| Schema 浏览器 | 浏览数据库 Schema 和表 |
| 查询历史 | 保存和检索过去的查询 |
| 自动补全 | 表名和列名建议 |

### SQL Lab 界面

| 面板 | 描述 |
|-------|-------------|
| 查询编辑器 | 编写和执行 SQL 查询 |
| 结果 | 查看查询结果 |
| 数据预览 | 表数据快速预览 |
| 已保存查询 | 访问之前保存的查询 |

### 查询功能

| 功能 | 描述 |
|---------|-------------|
| 执行 | 运行 SQL 查询（Ctrl+Enter） |
| 格式化 | 自动格式化 SQL 代码 |
| 保存 | 保存查询供以后使用 |
| 下载 | 将结果导出为 CSV |
| 分享 | 与他人分享查询 |

## 安全

### 用户角色

| 角色 | 权限 |
|------|-------------|
| Admin | 完全系统访问 |
| Alpha | 访问所有数据源 |
| Gamma | 仅访问许可的数据源 |
| sql_lab | 访问 SQL Lab |
| Public | 只读访问已发布的仪表板 |

### 行级安全

| 功能 | 描述 |
|---------|-------------|
| RLS 筛选器 | 按用户限制数据行 |
| 筛选器模板 | 可复用的安全筛选器 |
| 基于组 | 对用户组应用筛选器 |

### 访问控制

| 控制 | 描述 |
|---------|-------------|
| 数据源访问 | 控制用户可查询的数据库 |
| 仪表板访问 | 控制用户可查看的仪表板 |
| 图表访问 | 控制用户可创建的图表 |
| Schema 访问 | 控制用户可浏览的 Schema |

## 告警和报告

### 告警配置

| 设置 | 描述 |
|---------|-------------|
| 条件 | 返回布尔结果的 SQL 查询 |
| 阈值 | 触发告警的值 |
| 通知 | Email、Slack 或 Webhook 通知 |
| 计划 | 检查条件的频率 |

### 报告配置

| 设置 | 描述 |
|---------|-------------|
| Dashboard | 要渲染为报告的仪表板 |
| Format | PDF 或图片格式 |
| Schedule | 报告生成频率 |
| Recipients | 投递的邮箱地址 |

## API 访问

### REST API 端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/api/v1/chart/` | GET | 列出图表 |
| `/api/v1/dashboard/` | GET | 列出仪表板 |
| `/api/v1/dataset/` | GET | 列出数据集 |
| `/api/v1/database/` | GET | 列出数据库 |
| `/api/v1/query/` | GET | 列出已保存查询 |

### API 认证

```bash
# 登录获取访问令牌
curl -X POST http://localhost:8088/api/v1/security/login \
  -H "Content-Type: application/json" \
  -d '{"username": "admin", "password": "admin", "provider": "db"}'

# 在请求中使用令牌
curl -H "Authorization: Bearer <token>" \
  http://localhost:8088/api/v1/chart/
```

## 性能优化

### 缓存

| 缓存类型 | 描述 |
|-----------|-------------|
| 查询缓存 | 缓存查询结果以加快加载 |
| 图表缓存 | 缓存渲染的图表数据 |
| 仪表板缓存 | 缓存完整的仪表板状态 |
| 元数据缓存 | 缓存数据库 Schema 信息 |

### 查询优化

| 技术 | 描述 |
|-----------|-------------|
| 索引 | 为频繁查询添加数据库索引 |
| 物化视图 | 预计算复杂聚合 |
| 分区 | 按日期分区大表 |
| 缓存 | 为重复查询启用 Superset 缓存 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 用途 | 开源数据可视化和探索平台 |
| 数据源 | 连接 PostgreSQL、MySQL、BigQuery、Snowflake 等 |
| 图表 | 多种可视化类型 |
| 仪表板 | 带筛选器和自动刷新的交互式仪表板 |
| SQL IDE | 内置 SQL 编辑器用于数据探索 |
| 安全 | 基于角色的访问控制，带行级安全 |


---

## 来源：dashboard.md

## 简介

Dashy 是一个高度可定制的自托管仪表盘应用。它提供了一个基于 Web 的界面，用于组织链接、监控服务和展示小部件。

### 什么是 Dashy？

Dashy 是一个个人仪表盘，帮助您将 Web 服务、书签和系统状态集中在一个地方。

| 特性 | 描述 |
|------|------|
| 可定制布局 | 排列小部件和分区 |
| 状态监控 | 检查服务可用性 |
| 主题 | 多个内置主题 |
| 小部件 | 系统信息、天气等 |
| 认证 | 可选登录保护 |

### 为什么要自托管仪表盘？

| 好处 | 描述 |
|------|------|
| 集中访问 | 所有服务的单一入口 |
| 状态概览 | 一目了然的服务健康状况 |
| 定制化 | 根据工作流程定制 |
| 隐私 | 无第三方跟踪 |

## 安装

### 前置要求

| 要求 | 版本 |
|------|------|
| Node.js | 18 或更高 |
| Docker | 20.10 或更高（可选） |
| npm | 8 或更高 |

### Docker 安装

```bash
docker run -d \
  --name dashy \
  -p 8080:8080 \
  -v /path/to/conf.yml:/app/user-data/conf.yml \
  lissy93/dashy
```

### Docker Compose

```yaml
version: '3'
services:
  dashy:
    image: lissy93/dashy
    container_name: dashy
    ports:
      - "8080:8080"
    volumes:
      - ./conf.yml:/app/user-data/conf.yml
    restart: unless-stopped
```

### 手动安装

```bash
git clone https://github.com/Lissy93/dashy.git
cd dashy
yarn install
yarn build
yarn start
```

## 配置

### 配置文件结构

```yaml
pageInfo:
  title: My Dashboard
  description: Personal dashboard
  navLinks:
    - title: GitHub
      path: https://github.com

sections:
  - name: Services
    displayData:
      cols: 3
    items:
      - title: Portainer
        description: Container management
        icon: hl-portainer
        url: https://portainer.example.com
        statusCheck: true
```

### 基本配置选项

| 部分 | 用途 |
|------|------|
| `pageInfo` | 页面标题、描述、导航链接 |
| `sections` | 仪表盘项目分组 |
| `appConfig` | 全局应用设置 |
| `theme` | 外观样式 |

### 分区配置

```yaml
sections:
  - name: Media
    icon: fas fa-play
    displayData:
      cols: 2
      collapsed: false
      itemSize: medium
    items:
      - title: Plex
        url: https://plex.example.com
        icon: hl-plex
```

| 分区属性 | 描述 |
|----------|------|
| `name` | 分区标题 |
| `icon` | 分区图标 |
| `cols` | 列数 |
| `collapsed` | 默认折叠 |
| `itemSize` | 项目显示大小 |

## 添加项目

### 项目配置

```yaml
items:
  - title: Service Name
    description: Brief description
    icon: hl-servicename
    url: https://service.example.com
    target: newtab
    statusCheck: true
    tags:
      - media
      - streaming
```

| 项目属性 | 描述 |
|----------|------|
| `title` | 显示名称 |
| `description` | 悬停文本 |
| `icon` | 图标标识符 |
| `url` | 服务 URL |
| `target` | 打开方式 |
| `statusCheck` | 启用健康检查 |
| `tags` | 可搜索标签 |

### 图标来源

| 来源 | 前缀 | 示例 |
|------|------|------|
| HomeLab 图标 | `hl-` | `hl-portainer` |
| Font Awesome | `fas fa-` | `fas fa-home` |
| Material Design | `mdi-` | `mdi-server` |
| Emoji | 无 | `:rocket:` |
| URL | https:// | 自定义图片 URL |

## 状态监控

### 健康检查

```yaml
items:
  - title: Service
    url: https://service.example.com
    statusCheck: true
    statusCheckUrl: https://service.example.com/health
    statusCheckAllowInsecure: true
```

| 状态 | 颜色 | 含义 |
|------|------|------|
| 在线 | 绿色 | 服务正常响应 |
| 离线 | 红色 | 服务无响应 |
| 未知 | 灰色 | 未配置检查 |

### 状态检查选项

| 选项 | 描述 |
|------|------|
| `statusCheck` | 启用基本检查 |
| `statusCheckUrl` | 自定义端点 |
| `statusCheckAllowInsecure` | 允许自签名证书 |
| `statusCheckHeaders` | 自定义请求头 |

## 主题

### 内置主题

| 主题 | 风格 |
|------|------|
| Default | 简洁、现代 |
| Night | 暗色模式 |
| Dracula | 紫色暗色主题 |
| Nord | 冷色调蓝色主题 |
| Pastel | 柔和色彩 |
| Minimal | 简约、干净 |

### 自定义主题

```yaml
appConfig:
  theme: default
  customCss: |
    :root {
      --primary: #4a90d9;
      --background: #1a1a2e;
    }
```

### CSS 变量

| 变量 | 控制 |
|------|------|
| `--primary` | 强调色 |
| `--background` | 页面背景 |
| `--item-background` | 项目背景 |
| `--text-color` | 文本颜色 |
| `--heading-text` | 分区标题 |

## 小部件

### 可用小部件

| 小部件 | 描述 |
|--------|------|
| `clock` | 当前时间 |
| `weather` | 天气预报 |
| `system-info` | CPU、内存使用率 |
| `search-bar` | Web 搜索 |
| `notes` | 便签 |
| `todo-list` | 任务列表 |
| `iframe` | 嵌入外部页面 |

### 小部件配置

```yaml
sections:
  - name: Widgets
    widgets:
      - type: clock
        options:
          format: 24
          showDate: true

      - type: weather
        options:
          API_KEY: your-key
          city: London
          units: metric

      - type: system-info
        options:
          cpu: true
          memory: true
          disk: true
```

### 自定义小部件

```yaml
- type: iframe
  options:
    url: https://grafana.example.com/d/abc/dashboard
    height: 400
    width: 100%
```

## 认证

### 基本认证

```yaml
appConfig:
  auth:
    enableGuestAccess: false
    users:
      - user: admin
        hash: "$2b$12$..."
        type: admin
      - user: guest
        hash: "$2b$12$..."
        type: guest
```

### 生成密码哈希

```bash
npm install -g bcrypt-cli
bcrypt-cli "your-password"
```

### 访问级别

| 级别 | 权限 |
|------|------|
| Admin | 完全访问，编辑模式 |
| Guest | 只读访问 |
| None | 无访问权限 |

## 多页面支持

### 页面配置

```yaml
pages:
  - name: Home
    path: /
    conf: home.yml

  - name: Services
    path: /services
    conf: services.yml

  - name: Monitoring
    path: /monitoring
    conf: monitoring.yml
```

## 备份和恢复

### 导出配置

```bash
# 复制配置文件
cp /path/to/conf.yml ./backup-conf.yml

# 或从 UI 导出
# Settings → Export Config
```

### 导入配置

```bash
# 从备份恢复
cp ./backup-conf.yml /path/to/conf.yml

# 或从 UI 导入
# Settings → Import Config
```

## Web 服务器配置

### Nginx 反向代理

```nginx
server {
    listen 80;
    server_name dashboard.example.com;

    location / {
        proxy_pass http://localhost:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### 使用 Let's Encrypt 配置 SSL

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d dashboard.example.com
```

## 性能

### 优化技巧

| 技巧 | 描述 |
|------|------|
| 启用缓存 | 配置浏览器缓存 |
| 压缩图片 | 优化图标大小 |
| 限制小部件 | 只使用需要的小部件 |
| 懒加载 | 为分区启用懒加载 |

## 移动端支持

### 响应式设计

Dashy 自动适配移动屏幕：

| 屏幕大小 | 布局 |
|----------|------|
| 桌面 | 多列网格 |
| 平板 | 响应式网格 |
| 手机 | 单列 |

### PWA 支持

Dashy 可以作为 Progressive Web App 安装到移动设备上。

## 总结

| 功能 | 配置 |
|------|------|
| 分区 | 将项目分组 |
| 项目 | 指向服务的链接 |
| 小部件 | 系统信息、天气等 |
| 主题 | 外观定制 |
| 状态检查 | 监控服务健康 |
| 认证 | 可选登录保护 |


---

## 来源：dash.md

## 简介

Redash 是一个开源数据可视化和仪表板平台，可连接多种数据源，支持基于 SQL 的查询，并提供交互式仪表板，用于数据探索和团队共享。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| CPU | 2 核 | 4 核 |
| 内存 | 2 GB | 4 GB |
| 磁盘 | 20 GB | 100 GB |
| PostgreSQL | 9.6 | 13+ |
| Redis | 3.0 | 6+ |
| Docker | 20.10 | 最新版 |

## 安装

### Docker Compose

```yaml
version: '3.8'
services:
  redash:
    image: redash/redash:latest
    ports:
      - "5000:5000"
    env_file:
      - .env
    depends_on:
      - postgres
      - redis
    restart: unless-stopped

  postgres:
    image: postgres:15
    volumes:
      - pg-data:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: redash
      POSTGRES_USER: redash
      POSTGRES_PASSWORD: changeme
    restart: unless-stopped

  redis:
    image: redis:7
    restart: unless-stopped

  scheduler:
    image: redash/redash:latest
    command: scheduler
    env_file:
      - .env
    depends_on:
      - postgres
      - redis
    restart: unless-stopped

  worker:
    image: redash/redash:latest
    command: worker
    env_file:
      - .env
    depends_on:
      - postgres
      - redis
    restart: unless-stopped

volumes:
  pg-data:
```

### 环境变量

```bash
# .env
REDASH_DATABASE_URL=postgres://redash:changeme@postgres/redash
REDASH_REDIS_URL=redis://redis:6379/0
REDASH_SECRET_KEY=generate-a-random-secret-key
REDASH_COOKIE_SECRET=generate-another-random-key
REDASH_HOST=http://localhost:5000
```

### 初始化数据库

```bash
docker compose run --rm redash create_db
docker compose up -d
```

## 支持的数据源

| 数据库 | 类型 | 说明 |
|--------|------|------|
| PostgreSQL | SQL | 完全支持 |
| MySQL | SQL | 完全支持 |
| SQLite | SQL | 基于文件 |
| Microsoft SQL Server | SQL | 完全支持 |
| Amazon Redshift | SQL | 数据仓库 |
| Google BigQuery | SQL | 云分析 |
| ClickHouse | SQL | 列式数据库 |
| MongoDB | NoSQL | JSON 查询 |
| Elasticsearch | 搜索 | Query DSL |
| Prometheus | 时序 | PromQL |
| InfluxDB | 时序 | Flux 查询 |
| Google Sheets | 电子表格 | 基于 API |
| CSV | 文件 | 直接上传 |
| JSON API | REST | 基于 URL |

### 添加数据源

1. 导航到 **Settings > Data Sources**
2. 点击 **New Data Source**
3. 选择数据库类型
4. 输入连接详情
5. 测试连接
6. 保存

## 查询编辑器

### 编辑器功能

| 功能 | 说明 |
|------|------|
| 语法高亮 | SQL 语法着色 |
| 自动补全 | 表和列建议 |
| Schema 浏览器 | 浏览数据库结构 |
| 查询参数 | 动态用户输入 |
| 执行历史 | 之前的查询运行 |
| 版本历史 | 查询变更追踪 |

### 查询参数

| 参数类型 | 语法 | 用户输入 |
|---------|------|---------|
| 文本 | `{{ param }}` | 自由文本字段 |
| 数字 | `{{ param }}` | 数字输入 |
| 下拉菜单 | `{{ param }}` | 预定义选项 |
| 日期 | `{{ param }}` | 日期选择器 |
| 日期范围 | `{{ start }}` `{{ end }}` | 开始和结束日期 |
| 基于查询 | `{{ param }}` | 来自另一个查询的选项 |

### 参数化查询示例

```sql
SELECT
  date_trunc('{{ period }}', created_at) AS time_period,
  COUNT(*) AS order_count,
  SUM(total) AS revenue
FROM orders
WHERE
  created_at BETWEEN '{{ start_date }}' AND '{{ end_date }}'
  AND status IN ({{ status }})
GROUP BY time_period
ORDER BY time_period
```

## 可视化类型

| 图表类型 | 最佳场景 | 数据形态 |
|---------|---------|---------|
| 表格 | 详细数据探索 | 任意 |
| 折线图 | 随时间变化的趋势 | 时序数据 |
| 柱状图 | 分类比较 | 分类 + 数值 |
| 饼图 | 比例数据 | 整体的部分 |
| 散点图 | 寻找相关性 | 两个数值列 |
| 面积图 | 累积趋势 | 时序数据 |
| 热力图 | 密度模式 | 两个维度 + 值 |
| 队列 | 留存分析 | 基于时间的分组 |
| 漏斗 | 转化步骤 | 顺序阶段 |
| 地图 | 地理数据 | 经纬度 |
| 计数器 | 单指标显示 | 单个值 |
| 透视表 | 交叉表 | 多维度 |

### 图表配置选项

| 设置 | 说明 |
|------|------|
| X 列 | 水平轴数据列 |
| Y 列 | 垂直轴数据列 |
| 分组 | 系列分组列 |
| 排序 | 数据排序方向 |
| 限制 | 最大显示行数 |
| 堆叠 | 垂直堆叠系列值 |

## 仪表板

### 仪表板组件

| 组件 | 说明 |
|------|------|
| 小部件 | 单个查询可视化 |
| 文本框 | Markdown 格式的文本内容 |
| 参数 | 仪表板级过滤控制 |
| 标签 | 组织化的仪表板分区 |

### 仪表板布局设置

| 设置 | 说明 | 默认值 |
|------|------|--------|
| 列数 | 每行网格列数 | 3 |
| 自动高度 | 自动适应内容高度 | 关 |
| 刷新 | 自动刷新间隔 | 关 |
| 参数 | 共享过滤栏 | 开 |

### 创建仪表板

1. 导航到 **Create > Dashboard**
2. 添加名称和描述
3. 点击 **Add Widget**
4. 选择现有查询或创建新查询
5. 选择可视化类型
6. 定位和调整小部件大小
7. 设置仪表板参数
8. 保存

## 告警

### 告警配置

| 字段 | 说明 | 示例 |
|------|------|------|
| 查询 | 数据源查询 | SELECT count(*) FROM errors |
| 列 | 要监控的列 | count |
| 操作符 | 比较操作符 | greater than |
| 阈值 | 触发值 | 100 |
| 频率 | 检查间隔 | 5 minutes |

### 告警状态

| 状态 | 条件 | 操作 |
|------|------|------|
| 正常 | 条件未满足 | 不执行操作 |
| 待定 | 条件已满足，等待持续时间 | 监控中 |
| 触发 | 条件已满足，告警活跃 | 发送通知 |
| 未知 | 查询未返回数据 | 记录错误 |
| 错误 | 查询执行错误 | 记录错误 |

### 通知渠道

| 渠道 | 需要的配置 |
|------|-----------|
| 邮件 | SMTP 设置 |
| Slack | Webhook URL |
| PagerDuty | 集成密钥 |
| Webhook | 自定义 HTTP 端点 |
| Microsoft Teams | Webhook URL |

## 调度

| 调度选项 | 说明 |
|---------|------|
| 从不 | 仅手动执行 |
| 每分钟 | 持续更新 |
| 每 5 分钟 | 近实时 |
| 每小时 | 每小时刷新 |
| 每天 | 每天刷新 |
| 自定义 | Cron 表达式 |

## API

### REST API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/queries` | GET / POST | 列出或创建查询 |
| `/api/queries/{id}` | GET / PUT / DELETE | 管理特定查询 |
| `/api/dashboards` | GET / POST | 列出或创建仪表板 |
| `/api/query_results/{id}` | GET | 获取查询结果 |
| `/api/data_sources` | GET / POST | 管理数据源 |
| `/api/users` | GET / POST | 管理用户 |

### API 认证

```bash
# 使用用户配置中的 API key
curl -H "Authorization: Key YOUR_API_KEY" \
  http://localhost:5000/api/queries
```

## 用户管理

### 用户角色

| 角色 | 权限 |
|------|------|
| 管理员 | 完全访问，管理所有设置 |
| 默认 | 创建和编辑自己的查询和仪表板 |
| 查看者 | 仅查看共享仪表板 |

### 权限级别

| 级别 | 查询访问 | 仪表板访问 |
|------|---------|-----------|
| 私有 | 仅所有者 | 仅所有者 |
| 查看 | 任何人可查看 | 任何人可查看 |
| 编辑 | 指定用户可编辑 | 指定用户可编辑 |
| 公开 | 公开链接访问 | 公开链接访问 |

## 嵌入

### 嵌入选项

| 方法 | 说明 | 安全性 |
|------|------|--------|
| iframe | 在页面中嵌入仪表板 URL | 需要认证令牌 |
| 公开 URL | 分享公开仪表板链接 | 任何有链接的人 |
| API 小部件 | 编程嵌入 | 需要 API Key |

### iframe 示例

```html
<iframe
  src="https://redash.example.com/public/dashboards/token"
  width="100%"
  height="600"
  frameborder="0">
</iframe>
```

## 安全

| 措施 | 配置 |
|------|------|
| HTTPS | 使用 SSL 证书的反向代理 |
| 认证 | SAML 或 LDAP SSO 集成 |
| API Key | 按用户范围的 API 访问 |
| 速率限制 | 基于代理的请求限制 |
| 查询超时 | 最大执行时间设置 |
| 数据源权限 | 按组的数据源访问 |

## 备份

| 组件 | 方法 | 频率 |
|------|------|------|
| PostgreSQL | pg_dump | 每日 |
| 配置 | .env 文件备份 | 每周 |
| 查询 | 包含在数据库备份中 | 每日 |
| 仪表板 | 包含在数据库备份中 | 每日 |

### 备份脚本

```bash
#!/bin/bash
DATE=$(date +%Y%m%d)
BACKUP_DIR="/var/backups/redash"

pg_dump -h localhost -U redash redash | gzip > "$BACKUP_DIR/redash-$DATE.sql.gz"
find "$BACKUP_DIR" -mtime +30 -delete
```

## 性能建议

| 方面 | 建议 |
|------|------|
| 查询 | 为数据探索添加 LIMIT 子句 |
| 缓存 | 启用查询结果缓存 |
| 索引 | 确保存在适当的数据库索引 |
| 参数 | 在 WHERE 子句中使用索引列 |
| 仪表板 | 限制每个仪表板的小部件数量 |
| 刷新 | 使用适当的刷新间隔 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 查询超时 | 长时间运行的查询 | 优化查询或增加超时时间 |
| 连接失败 | 凭据错误 | 验证数据源连接设置 |
| 仪表板缓慢 | 小部件太多 | 减少小部件数量或启用缓存 |
| 无数据返回 | 查询返回空 | 检查查询逻辑和过滤器 |
| 导入失败 | 格式问题 | 检查 JSON 导出格式兼容性 |

## 总结

Redash 提供了一个强大的数据可视化和仪表板平台。其对多种数据源的支持、参数化查询和交互式可视化，使其适合需要在组织内探索和分享数据洞察的团队。


---
