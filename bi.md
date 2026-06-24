# 使用 Metabase 进行商业智能

## 简介

Metabase 是一个开源商业智能工具，可以轻松地可视化和探索数据。它提供了一个用户友好的界面，用于创建仪表盘和对数据提问。

### 什么是 Metabase？

Metabase 是一个 BI 平台，连接到您的数据库，允许组织中的任何人无需 SQL 知识即可提问和创建仪表盘。

| 特性 | 描述 |
|------|------|
| 可视化查询构建器 | 无需 SQL 创建查询 |
| 仪表盘 | 可视化数据展示 |
| SQL 编辑器 | 高级查询模式 |
| 告警 | 数据驱动的通知 |
| 嵌入 | 嵌入到其他应用 |

### 与其他方案的比较

| 特性 | Metabase | Tableau | Power BI |
|------|----------|---------|----------|
| 开源 | 是 | 否 | 否 |
| 自托管 | 是 | 否 | 否 |
| 费用 | 免费 | 付费 | 付费 |
| 易用性 | 高 | 中 | 中 |
| 需要 SQL | 否 | 有时 | 有时 |

## 安装

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| Java | 11+ | 17+ |
| 内存 | 1 GB | 4+ GB |
| CPU | 1 核 | 2+ 核 |
| 存储 | 1 GB | 10+ GB |

### Docker 安装

```bash
docker run -d -p 3000:3000 \
  --name metabase \
  -e MB_DB_TYPE=postgres \
  -e MB_DB_DBNAME=metabase \
  -e MB_DB_PORT=5432 \
  -e MB_DB_USER=metabase \
  -e MB_DB_PASS=password \
  -e MB_DB_HOST=db \
  metabase/metabase
```

### Docker Compose

```yaml
version: '3'
services:
  metabase:
    image: metabase/metabase:latest
    ports:
      - "3000:3000"
    environment:
      - MB_DB_TYPE=postgres
      - MB_DB_DBNAME=metabase
      - MB_DB_PORT=5432
      - MB_DB_USER=metabase
      - MB_DB_PASS=password
      - MB_DB_HOST=db
    volumes:
      - metabase_data:/metabase-data
    depends_on:
      - db

  db:
    image: postgres:13
    environment:
      - POSTGRES_USER=metabase
      - POSTGRES_PASSWORD=password
      - POSTGRES_DB=metabase
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  metabase_data:
  postgres_data:
```

### JAR 安装

```bash
# 下载 JAR
wget https://downloads.metabase.com/v0.47.0/metabase.jar

# 运行 Metabase
java -jar metabase.jar
```

## 数据库连接

### 支持的数据库

| 数据库 | 状态 |
|--------|------|
| PostgreSQL | 完全支持 |
| MySQL | 完全支持 |
| SQLite | 完全支持 |
| MongoDB | 完全支持 |
| SQL Server | 完全支持 |
| BigQuery | 完全支持 |
| Snowflake | 完全支持 |
| Redshift | 完全支持 |

### 添加数据库

1. 进入 Settings > Databases
2. 点击 "Add database"
3. 选择数据库类型
4. 输入连接详情
5. 保存

### 连接设置

| 设置 | 描述 |
|------|------|
| 显示名称 | 友好名称 |
| 主机 | 数据库主机 |
| 端口 | 数据库端口 |
| 数据库名 | 要连接的数据库 |
| 用户名 | 数据库用户 |
| 密码 | 数据库密码 |
| SSL | 启用 SSL |

## 问题

### 可视化问题构建器

| 步骤 | 描述 |
|------|------|
| 1. 选择数据 | 选择表或模型 |
| 2. 过滤 | 添加过滤条件 |
| 3. 汇总 | 添加聚合 |
| 4. 分组 | 按字段分组 |
| 5. 可视化 | 选择图表类型 |

### 问题类型

| 类型 | 描述 |
|------|------|
| Simple | 无需 SQL |
| Custom | SQL 编辑器 |
| Native | 原始 SQL 查询 |

### 聚合

| 聚合 | 描述 |
|------|------|
| Count | 行数 |
| Sum | 值的总和 |
| Average | 平均值 |
| Distinct | 唯一计数 |
| Min/Max | 最小/最大值 |

### 过滤器

| 过滤类型 | 示例 |
|----------|------|
| 等于 | Status = "active" |
| 包含 | Name contains "test" |
| 大于 | Amount > 100 |
| 之间 | Date between range |
| 为空 | Field is empty |

## SQL 编辑器

### 编写 SQL

```sql
SELECT 
  date_trunc('month', created_at) AS month,
  COUNT(*) AS orders,
  SUM(total) AS revenue
FROM orders
WHERE status = 'completed'
GROUP BY date_trunc('month', created_at)
ORDER BY month
```

### SQL 变量

```sql
SELECT *
FROM products
WHERE category = {{category}}
  AND price > {{min_price}}
```

### SQL 参数

| 参数 | 类型 | 描述 |
|------|------|------|
| Text | `{{text}}` | 自由文本输入 |
| Number | `{{number}}` | 数值输入 |
| Date | `{{date}}` | 日期选择器 |
| Field filter | `{{filter}}` | 映射到字段 |

## 可视化

### 图表类型

| 图表 | 最佳用途 |
|------|----------|
| Table | 详细数据 |
| Line | 趋势随时间变化 |
| Bar | 比较 |
| Pie | 占比 |
| Scatter | 相关性 |
| Map | 地理数据 |
| Funnel | 流程步骤 |
| Gauge | 单一指标 |

### 可视化设置

| 设置 | 描述 |
|------|------|
| Data | 配置数据系列 |
| Display | 外观样式 |
| Axes | X 和 Y 轴标签 |
| Colors | 配色方案 |
| Labels | 数据标签 |

## 仪表盘

### 创建仪表盘

1. 进入 Dashboards
2. 点击 "Create dashboard"
3. 添加名称和描述
4. 将问题添加为卡片
5. 排列布局 |

### 仪表盘卡片

| 卡片类型 | 描述 |
|----------|------|
| Question | 展示已保存的问题 |
| Text | Markdown 文本 |
| Link | 外部链接 |
| Iframe | 嵌入内容 |

### 仪表盘过滤器

| 过滤器 | 示例 |
|--------|------|
| 日期范围 | 按日期过滤 |
| 分类 | 按分类过滤 |
| 位置 | 按位置过滤 |
| ID | 按 ID 过滤 |

### 仪表盘布局

| 功能 | 描述 |
|------|------|
| Grid | 18 列网格 |
| 调整大小 | 拖动调整 |
| 移动 | 拖动重新定位 |
| 编辑 | 在编辑模式下修改 |

## 模型

### 什么是模型？

模型是可重用、经过验证的数据集，可以作为问题的起点。

### 创建模型

1. 编写 SQL 查询
2. 保存为模型
3. 添加元数据
4. 定义关系 |

### 模型功能

| 功能 | 描述 |
|------|------|
| 元数据 | 字段描述 |
| 关系 | 模型之间的链接 |
| 指标 | 预定义计算 |
| 过滤 | 默认过滤器 |

## 告警

### 创建告警

1. 创建或选择问题
2. 点击 "Create alert"
3. 设置条件
4. 选择通知方式

### 告警类型

| 类型 | 描述 |
|------|------|
| Goal line | 指标超过阈值 |
| Result change | 数据变化 |
| Custom | 自定义条件 |

### 通知渠道

| 渠道 | 描述 |
|------|------|
| Email | 发送邮件通知 |
| Slack | 发送到 Slack 频道 |
| Webhook | 自定义 HTTP 端点 |

## 权限

### 权限组

| 群组 | 描述 |
|------|------|
| All Users | 默认群组 |
| Admin | 完全访问 |
| Custom | 自定义权限 |

### 权限级别

| 级别 | 访问 |
|------|------|
| Unrestricted | 完全访问 |
| Granular | 按集合 |
| No self-service | 仅查看 |
| Blocked | 无访问 |

### 数据权限

| 权限 | 选项 |
|------|------|
| 数据访问 | Unrestricted、Granular、No self service、Block |
| SQL 查询 | Yes、No |
| 下载 | Yes、No、Limited |

## 嵌入

### 公开嵌入

```html
<iframe
  src="https://metabase.example.com/public/dashboard/your-embed-key"
  frameborder="0"
  width="800"
  height="600"
></iframe>
```

### 签名嵌入

```javascript
// 使用 JWT 生成嵌入 URL
const payload = {
  resource: { dashboard: 1 },
  params: {},
  exp: Math.round(Date.now() / 1000) + (10 * 60)
};
```

### 嵌入选项

| 选项 | 描述 |
|------|------|
| Public | 无认证 |
| Signed | JWT 认证 |
| Interactive | 完整功能 |
| Static | 只读 |

## API 访问

### REST API

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/card` | GET | 列出问题 |
| `/api/dashboard` | GET | 列出仪表盘 |
| `/api/dataset` | POST | 运行查询 |
| `/api/user` | GET | 列出用户 |

### API 认证

```bash
# 获取 API 密钥
# 进入 Settings > API Keys

# 使用 API 密钥
curl -H "x-api-key: YOUR_API_KEY" \
  https://metabase.example.com/api/card
```

## 管理

### 常规设置

| 设置 | 描述 |
|------|------|
| 站点名称 | 应用名称 |
| 站点 URL | 基础 URL |
| 邮件 | SMTP 配置 |
| Slack | Slack 集成 |

### 用户管理

| 操作 | 描述 |
|------|------|
| 创建用户 | 添加新用户 |
| 编辑用户 | 修改用户设置 |
| 停用 | 禁用用户账户 |
| 重置密码 | 更改密码 |

### 性能调优

| 设置 | 描述 |
|------|------|
| JVM 内存 | 分配 RAM |
| 连接池 | 数据库连接 |
| 查询超时 | 最大查询时间 |
| 缓存 | 结果缓存 |

## 缓存

### 缓存配置

```json
{
  "enable-query-caching": true,
  "query-caching-max-kb": 1000,
  "query-caching-max-ttl": 86400
}
```

### 缓存策略

| 策略 | 描述 |
|------|------|
| Duration | 基于时间的过期 |
| Adaptive | 基于查询复杂度 |
| Disabled | 不缓存 |

## 备份和恢复

### 数据库备份

```bash
# PostgreSQL 备份
pg_dump -U metabase metabase > metabase_backup.sql

# 恢复
psql -U metabase metabase < metabase_backup.sql
```

### 应用数据

```bash
# 导出 Metabase 数据
curl -H "x-api-key: YOUR_API_KEY" \
  https://metabase.example.com/api/backup
```

## 监控

### 健康检查

```bash
curl https://metabase.example.com/api/health
```

### 日志

| 日志 | 位置 |
|------|------|
| Application | Metabase 日志 |
| Query | 数据库日志 |
| Error | 错误日志 |

## 总结

| 功能 | 用途 |
|------|------|
| 问题 | 可视化查询数据 |
| 仪表盘 | 可视化展示 |
| 告警 | 数据通知 |
| 权限 | 访问控制 |
| 嵌入 | 与应用集成 |
| API | 编程访问 |
