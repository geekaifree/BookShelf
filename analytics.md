# Apache Superset 数据分析教程

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
