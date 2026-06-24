# Grafana 教程：监控和可观测性平台

## 简介

Grafana 是一个开源的分析和交互式可视化平台。当连接到支持的数据源时，它提供图表、图形和告警功能，是监控基础设施、应用程序和业务指标的标准工具。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| CPU | 1 核 | 2 核 |
| 内存 | 256 MB | 1 GB |
| 磁盘 | 1 GB | 10 GB |
| 操作系统 | Linux, Windows, macOS | Linux |
| 网络 | HTTP | 通过反向代理使用 HTTPS |

## 安装

### Docker 安装

```bash
docker run -d \
  --name grafana \
  -p 3000:3000 \
  -v grafana-data:/var/lib/grafana \
  grafana/grafana:latest
```

### Docker Compose 搭配 Prometheus

```yaml
version: '3.8'
services:
  grafana:
    image: grafana/grafana:latest
    ports:
      - "3000:3000"
    volumes:
      - grafana-data:/var/lib/grafana
    environment:
      - GF_SECURITY_ADMIN_PASSWORD=admin123
    restart: unless-stopped

  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prom-data:/prometheus
    restart: unless-stopped

volumes:
  grafana-data:
  prom-data:
```

### APT 安装（Debian/Ubuntu）

```bash
sudo apt-get install -y apt-transport-https software-properties-common
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
echo "deb https://packages.grafana.com/oss/deb stable main" | \
  sudo tee /etc/apt/sources.list.d/grafana.list
sudo apt-get update && sudo apt-get install grafana
sudo systemctl start grafana-server
sudo systemctl enable grafana-server
```

## 数据源

### 支持的数据源

| 数据源 | 类型 | 用途 |
|--------|------|------|
| Prometheus | 时序 | 基础设施监控 |
| InfluxDB | 时序 | IoT、指标 |
| Elasticsearch | 搜索/分析 | 日志分析 |
| Loki | 日志聚合 | 日志监控 |
| MySQL | SQL 数据库 | 业务指标 |
| PostgreSQL | SQL 数据库 | 业务指标 |
| Graphite | 时序 | 应用指标 |
| CloudWatch | AWS 指标 | AWS 监控 |
| Azure Monitor | Azure 指标 | Azure 监控 |
| Stackdriver | GCP 指标 | GCP 监控 |
| Jaeger | 分布式追踪 | 追踪分析 |
| Tempo | 分布式追踪 | 追踪存储 |
| TestData | 测试数据 | 仪表板测试 |

### 添加数据源

1. 导航到 **Configuration > Data Sources**
2. 点击 **Add data source**
3. 从列表中选择类型
4. 配置连接详情
5. 点击 **Save & Test**

## 仪表板概念

### 仪表板组件

| 组件 | 说明 |
|------|------|
| Panel（面板） | 单个可视化单元 |
| Row（行） | 面板组 |
| Variable（变量） | 动态过滤值 |
| Annotation（注释） | 图表上的事件标记 |
| Link（链接） | 导航到其他仪表板 |

### 面板类型

| 面板 | 用途 |
|------|------|
| Time Series | 随时间变化的指标 |
| Stat | 带迷你图的单值 |
| Gauge | 范围内的值 |
| Bar Chart | 分类比较 |
| Pie Chart | 比例数据 |
| Table | 详细表格数据 |
| Heatmap | 随时间的密度 |
| State Timeline | 随时间的状态 |
| Logs | 日志行显示 |
| Node Graph | 拓扑可视化 |
| Alert List | 活跃告警 |
| Text | Markdown 或 HTML |

## PromQL 基础

### 查询类型

| 类型 | 函数 | 示例 |
|------|------|------|
| Instant（即时） | 当前值 | `up` |
| Range（范围） | 时间范围 | `rate(http_requests_total[5m])` |
| Aggregation（聚合） | 分组结果 | `sum by (instance) (up)` |

### 常用 PromQL 查询

| 指标 | 查询 | 用途 |
|------|------|------|
| CPU 使用率 | `100 - (avg by (instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)` | CPU 利用率 |
| 内存使用率 | `(1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) * 100` | 内存利用率 |
| 磁盘使用率 | `(1 - (node_filesystem_avail_bytes{mountpoint="/"} / node_filesystem_size_bytes{mountpoint="/"})) * 100` | 磁盘利用率 |
| 请求速率 | `rate(http_requests_total[5m])` | 每秒请求数 |
| 错误速率 | `rate(http_requests_total{status=~"5.."}[5m])` | 每秒错误数 |
| P95 延迟 | `histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))` | 第 95 百分位延迟 |

### PromQL 操作符

| 操作符 | 说明 | 示例 |
|--------|------|------|
| `+` | 加法 | `metric_a + metric_b` |
| `-` | 减法 | `metric_a - metric_b` |
| `*` | 乘法 | `metric_a * 100` |
| `/` | 除法 | `metric_a / metric_b` |
| `>` | 大于 | `metric > 100` |
| `<` | 小于 | `metric < 50` |
| `==` | 等于 | `metric == 0` |
| `!=` | 不等于 | `metric != 0` |

## 变量

### 变量类型

| 类型 | 来源 | 用途 |
|------|------|------|
| Query（查询） | 数据源查询 | 来自数据的动态值 |
| Custom（自定义） | 手动列表 | 固定选项 |
| Constant（常量） | 单个值 | 可复用常量 |
| Interval（间隔） | 时间范围 | 步进间隔 |
| Data source（数据源） | 数据源列表 | 切换数据源 |
| Text box（文本框） | 用户输入 | 自由文本过滤 |

### 创建变量

1. 导航到 **Dashboard Settings > Variables**
2. 点击 **Add variable**
3. 设置名称（例如 `instance`）
4. 选择类型（例如 Query）
5. 配置查询：`label_values(up, instance)`
6. 设置显示选项
7. 保存

### 变量用法

| 语法 | 说明 |
|------|------|
| `$variable` | 简单替换 |
| `${variable}` | 显式替换 |
| `${variable:csv}` | CSV 格式 |
| `${variable:pipe}` | 管道分隔 |
| `${variable:regex}` | 正则格式 |

## 告警

### 告警规则

| 组件 | 说明 |
|------|------|
| Condition（条件） | 何时触发 |
| Evaluation（评估） | 多久检查一次 |
| Labels（标签） | 告警元数据 |
| Annotations（注释） | 告警描述 |

### 告警状态

| 状态 | 说明 |
|------|------|
| Normal（正常） | 条件未满足 |
| Pending（待定） | 条件已满足，等待持续时间 |
| Firing（触发） | 条件已满足，告警活跃 |
| NoData | 查询未返回数据 |
| Error（错误） | 查询执行错误 |

### 通知渠道

| 渠道 | 配置 |
|------|------|
| 邮件 | SMTP 设置 |
| Slack | Webhook URL |
| PagerDuty | 集成密钥 |
| Microsoft Teams | Webhook URL |
| Discord | Webhook URL |
| Telegram | Bot token 和 chat ID |
| Webhook | 自定义 HTTP 端点 |

### 告警规则示例

| 字段 | 值 |
|------|-----|
| 名称 | 高 CPU 使用率 |
| 查询 | `100 - (avg(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)` |
| 条件 | 高于 80 |
| 持续 | 5 分钟 |
| 标签 | severity: warning |
| 摘要 | CPU 使用率在 {{ $labels.instance }} 上超过 80% |

## 仪表板供应

### 基于文件的供应

```yaml
# /etc/grafana/provisioning/dashboards/dashboard.yml
apiVersion: 1
providers:
  - name: 'default'
    orgId: 1
    folder: ''
    type: file
    disableDeletion: false
    editable: true
    options:
      path: /var/lib/grafana/dashboards
      foldersFromFilesStructure: true
```

### 数据源供应

```yaml
# /etc/grafana/provisioning/datasources/datasource.yml
apiVersion: 1
datasources:
  - name: Prometheus
    type: prometheus
    access: proxy
    url: http://prometheus:9090
    isDefault: true
    editable: true
```

## 用户管理

### 组织角色

| 角色 | 权限 |
|------|------|
| Viewer（查看者） | 查看仪表板和面板 |
| Editor（编辑者） | 创建和编辑仪表板 |
| Admin（管理员） | 完全访问包括设置 |

### 团队管理

| 功能 | 说明 |
|------|------|
| Teams（团队） | 将用户分组 |
| 文件夹权限 | 按团队的文件夹访问 |
| 仪表板权限 | 按仪表板的访问 |
| 数据源权限 | 按数据源的访问 |

## API

### REST API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/dashboards/uid/{uid}` | GET | 获取仪表板 |
| `/api/dashboards/db` | POST | 创建/更新仪表板 |
| `/api/datasources` | GET / POST | 管理数据源 |
| `/api/alert-rules` | GET / POST | 管理告警规则 |
| `/api/org/users` | GET / POST | 管理用户 |
| `/api/annotations` | GET / POST | 管理注释 |

### API 认证

```bash
# 使用 API key
curl -H "Authorization: Bearer YOUR_API_KEY" \
  http://localhost:3000/api/dashboards/home

# 使用基本认证
curl -u admin:admin123 \
  http://localhost:3000/api/dashboards/home
```

## 常见监控栈

### 基础设施监控

| 组件 | 工具 | 用途 |
|------|------|------|
| 指标收集 | Prometheus | 抓取和存储指标 |
| 可视化 | Grafana | 仪表板和告警 |
| Node Exporter | Prometheus 导出器 | 主机指标 |
| cAdvisor | 容器导出器 | Docker 指标 |

### 应用监控

| 组件 | 工具 | 用途 |
|------|------|------|
| 指标 | Prometheus 客户端库 | 应用指标 |
| 追踪 | Tempo 或 Jaeger | 分布式追踪 |
| 日志 | Loki | 日志聚合 |
| 可视化 | Grafana | 统一仪表板 |

### 日志监控

| 组件 | 工具 | 用途 |
|------|------|------|
| 收集 | Promtail 或 Fluentd | 日志传输 |
| 存储 | Loki | 日志存储 |
| 查询 | LogQL | 日志查询 |
| 可视化 | Grafana | 日志仪表板 |

## 性能

| 设置 | 位置 | 影响 |
|------|------|------|
| 查询缓存 | 数据源配置 | 更快的仪表板加载 |
| 仪表板刷新 | 面板设置 | 服务器负载 |
| 时间范围 | 默认时间范围 | 查询性能 |
| 面板限制 | 最大数据点 | 查询效率 |

## 安全

| 措施 | 配置 |
|------|------|
| HTTPS | 使用 SSL 的反向代理 |
| 认证 | LDAP、OAuth、SAML |
| RBAC | 基于角色的访问控制 |
| API Key | 有范围的 API 访问 |
| 审计 | 审计日志 |
| 加密 | 数据库静态加密 |

## 备份

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | SQLite 文件复制或 SQL 导出 | 每日 |
| 仪表板 | JSON 导出或供应 | 更改时 |
| 数据源 | 配置备份 | 更改时 |
| 告警规则 | 包含在数据库备份中 | 每日 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无数据 | 数据源配置错误 | 检查连接设置 |
| 仪表板缓慢 | 面板太多 | 减少面板数或优化查询 |
| 告警未触发 | 阈值错误 | 检查告警条件 |
| 登录失败 | 认证配置错误 | 检查认证提供商设置 |
| 面板缺失 | 权限问题 | 检查文件夹/仪表板权限 |

## 总结

Grafana 是监控和可观测性的行业标准。其对多种数据源的支持、灵活的可视化选项和强大的告警能力，使其成为任何基础设施或应用监控设置的必备工具。
