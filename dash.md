# Redash 教程：数据仪表板平台

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
