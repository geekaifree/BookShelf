# 监控与运维

> 本文档整合了以下源文件：monitor.md, infra.md, uptime.md, uptime2.md, metrics.md

---

## 来源：monitor.md

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


---

## 来源：infra.md

## 目录

1. [Netdata 简介](#introduction)
2. [安装方式](#installation)
3. [仪表板概述](#dashboard)
4. [指标与图表](#metrics)
5. [告警与通知](#alerts)
6. [Parent-Child 架构](#architecture)
7. [集成](#integrations)
8. [性能调优](#performance)

---

## 简介

Netdata 是一个实时基础设施监控和故障排查平台。它提供粒度为每秒的指标可视化，无需配置，非常适合快速识别性能瓶颈。

### Netdata 核心功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 实时 | 每秒粒度 | 即时可见性 |
| 零配置 | 自动检测服务 | 快速部署 |
| 低开销 | 1% CPU 使用率 | 可用于生产 |
| 分布式 | Parent-Child 架构 | 可扩展 |
| 开源 | 社区版免费 | 无许可费用 |

### 监控范围

| 层级 | 收集的指标 |
|------|------------|
| 系统 | CPU、内存、磁盘、网络 |
| 容器 | Docker、Kubernetes |
| 应用 | NGINX、PostgreSQL、Redis |
| 自定义 | Prometheus、statsd |

### Netdata vs 其他工具

| 功能 | Netdata | Prometheus/Grafana | Zabbix |
|------|---------|-------------------|--------|
| 设置时间 | 分钟 | 小时 | 天 |
| 实时 | 1s | 15s（默认） | 60s |
| 仪表板 | 内置 | 手动设置 | 手动设置 |
| 资源使用 | 低 | 中等 | 高 |
| 学习曲线 | 低 | 中等 | 高 |

---

## 安装方式

Netdata 为不同环境提供多种安装方式。

### 一键安装

```bash
# Standard installation
curl https://get.netdata.cloud/kickstart.sh > /tmp/netdata-kickstart.sh && sh /tmp/netdata-kickstart.sh

# Non-interactive
curl https://get.netdata.cloud/kickstart.sh > /tmp/netdata-kickstart.sh && sh /tmp/netdata-kickstart.sh --dont-wait
```

### Docker 安装

```bash
# Basic Docker run
docker run -d --name=netdata \
  -p 19999:19999 \
  -v netdataconfig:/etc/netdata \
  -v netdatalib:/var/lib/netdata \
  -v netdatacache:/var/cache/netdata \
  -v /etc/passwd:/host/etc/passwd:ro \
  -v /etc/group:/host/etc/group:ro \
  -v /etc/localtime:/etc/localtime:ro \
  -v /proc:/host/proc:ro \
  -v /sys:/host/sys:ro \
  --cap-add SYS_PTRACE \
  --security-opt apparmor=unconfined \
  netdata/netdata
```

### 包管理器安装

| 发行版 | 命令 |
|--------|------|
| Debian/Ubuntu | `apt install netdata` |
| CentOS/RHEL | `yum install netdata` |
| Fedora | `dnf install netdata` |
| Arch Linux | `pacman -S netdata` |

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2 核 |
| 内存 | 256MB | 1GB |
| 磁盘 | 1GB | 10GB |
| 操作系统 | Linux, macOS | 最新 LTS |

---

## 仪表板概述

Netdata 仪表板提供所有收集指标的实时可视化。

### 仪表板区域

| 区域 | 内容 | 位置 |
|------|------|------|
| 概览 | 摘要图表 | 顶部 |
| 系统 | CPU、内存、磁盘 | 中部 |
| 应用 | 服务指标 | 系统下方 |
| 网络 | 接口流量 | 底部 |
| 自定义 | 用户定义 | 可配置 |

### 导航控制

| 控制 | 操作 | 快捷方式 |
|------|------|----------|
| 放大 | 增加时间分辨率 | 向上滚动 |
| 缩小 | 减少时间分辨率 | 向下滚动 |
| 左移 | 更早时间 | 点击+向左拖动 |
| 右移 | 更晚时间 | 点击+向右拖动 |
| 重置 | 返回实时 | 双击 |

### 仪表板自定义

| 功能 | 描述 | 配置 |
|------|------|------|
| 主题 | 浅色或深色 | 用户偏好 |
| 图表高度 | 调整大小 | 拖动分隔线 |
| 图例 | 显示/隐藏值 | 点击图例 |
| 告警 | 可视化指示器 | 告警标签页 |

### 访问方式

| 方式 | URL | 安全性 |
|------|-----|--------|
| 直接 | http://server:19999 | 无（默认） |
| Nginx 代理 | https://domain.com | SSL + 认证 |
| Cloud | app.netdata.cloud | Netdata Cloud |

---

## 指标与图表

理解 Netdata 中显示的指标和图表。

### 系统指标

| 指标 | 图表类型 | 显示内容 |
|------|----------|----------|
| CPU 使用率 | 堆叠面积图 | 每核利用率 |
| 内存 | 堆叠面积图 | 已用、缓存、空闲 |
| 磁盘 I/O | 折线图 | 读/写吞吐量 |
| 网络 | 面积图 | 进出流量 |

### CPU 指标分解

| 指标 | 颜色 | 含义 |
|------|------|------|
| user | 蓝色 | 用户空间进程 |
| system | 绿色 | 内核操作 |
| iowait | 橙色 | 等待 I/O |
| idle | 灰色 | 未使用容量 |

### 内存指标分解

| 指标 | 描述 | 关注级别 |
|------|------|----------|
| Used | 正在使用 | 监控 |
| Cached | 文件系统缓存 | 正常 |
| Buffers | 内核缓冲 | 正常 |
| Free | 完全未使用 | 如果有缓存可用则低 |

### 磁盘指标

| 指标 | 单位 | 指示内容 |
|------|------|----------|
| Utilization | % | 磁盘繁忙程度 |
| IOPS | ops/s | 每秒操作数 |
| Throughput | MB/s | 数据传输速率 |
| Latency | ms | 响应时间 |

### 图表类型

| 类型 | 最适合 | 示例 |
|------|--------|------|
| 面积图 | 累积值 | CPU 使用率 |
| 折线图 | 单个指标 | 网络流量 |
| 堆叠图 | 构成 | 内存分解 |
| 柱状图 | 对比 | 每核 CPU |

---

## 告警与通知

Netdata 提供灵活的告警系统用于主动监控。

### 告警严重级别

| 级别 | 颜色 | 含义 | 操作 |
|------|------|------|------|
| Clear | 绿色 | 正常 | 无 |
| Warning | 黄色 | 需要关注 | 监控 |
| Critical | 红色 | 立即行动 | 响应 |

### 默认告警

| 指标 | 警告阈值 | 严重阈值 |
|------|----------|----------|
| CPU 使用率 | 80% 持续 10 分钟 | 95% 持续 10 分钟 |
| 内存使用率 | 80% | 95% |
| 磁盘使用率 | 80% | 95% |
| CPU I/O Wait | 20% 持续 10 分钟 | 50% 持续 10 分钟 |

### 自定义告警配置

```yaml
# /etc/netdata/health.d/custom.conf
template: high_cpu_usage
      on: system.cpu
    calc: $average
   every: 10s
    warn: $this > 80
    crit: $this > 95
   delay: down 15m multiplier 1.5 max 1h
    info: CPU usage is high
      to: sysadmin
```

### 通知方式

| 方式 | 配置 | 用途 |
|------|------|------|
| Email | SMTP 设置 | 团队通知 |
| Slack | Webhook URL | 频道告警 |
| PagerDuty | API key | 值班路由 |
| Discord | Webhook URL | 社区告警 |
| 自定义 | Webhook | 任意集成 |

### 通知配置

| 设置 | 描述 | 示例 |
|------|------|------|
| 接收人 | 谁接收通知 | sysadmin, slack |
| 频率 | 重复间隔 | 每 5 分钟 |
| 静默 | 临时禁用 | 维护窗口 |
| 过滤 | 哪些告警 | 仅严重 |

---

## Parent-Child 架构

Netdata 的分布式架构支持大规模集中监控。

### 架构组件

| 组件 | 角色 | 资源 |
|------|------|------|
| Child | 收集指标 | 最少 |
| Parent | 存储、可视化 | 更多资源 |
| Cloud | 集中视图 | Netdata 服务 |

### Parent 配置

```yaml
# /etc/netdata/netdata.conf
[db]
    mode = multi
    replication period = 1d
    
[web]
    bind to = *:19999
```

### Child 配置

```yaml
# /etc/netdata/stream.conf
[stream]
    enabled = yes
    destination = parent:19999
    api key = YOUR_API_KEY
```

### 扩展考虑

| Children 数量 | Parent 资源 | 保留时间 |
|---------------|-------------|----------|
| 10 | 2 CPU, 4GB RAM | 7 天 |
| 50 | 4 CPU, 8GB RAM | 3 天 |
| 100 | 8 CPU, 16GB RAM | 1 天 |
| 500+ | 专用集群 | 小时 |

### 数据保留

| 存储 | 保留 | 磁盘使用 |
|------|------|----------|
| RAM | 1 小时 | 快 |
| DB | 数天到数周 | 中等 |
| 导出 | 无限 | 外部存储 |

---

## 集成

Netdata 开箱即用地与众多服务和平台集成。

### 自动检测服务

| 服务 | 检测方式 | 指标 |
|------|----------|------|
| NGINX | Status 模块 | 连接、请求 |
| Apache | mod_status | Worker、请求 |
| PostgreSQL | pg_stat | 连接、查询 |
| Redis | INFO 命令 | 内存、客户端 |
| Docker | Socket | 容器、资源 |

### Prometheus 集成

| 配置 | 描述 |
|------|------|
| 端点 | /api/v1/allmetrics |
| 格式 | Prometheus text |
| 标签 | 自动添加 |

### 云集成

| 平台 | 功能 | 设置 |
|------|------|------|
| AWS | CloudWatch 指标 | IAM 角色 |
| GCP | Stackdriver 指标 | 服务账号 |
| Azure | Monitor 指标 | 服务主体 |

### 自定义收集器

| 方式 | 语言 | 复杂度 |
|------|------|--------|
| Python | Python | 低 |
| Bash | Shell | 低 |
| Go | Go | 中等 |
| Prometheus | 任意 | 中等 |

### 导出指标

| 目标 | 协议 | 用途 |
|------|------|------|
| Prometheus | Remote write | 长期存储 |
| InfluxDB | HTTP | 时序数据库 |
| Graphite | TCP | 旧系统 |
| JSON | HTTP | 自定义处理 |

---

## 性能调优

针对不同环境和工作负载优化 Netdata。

### 内存优化

| 设置 | 默认 | 低内存 | 高性能 |
|------|------|--------|--------|
| History | 3600s | 900s | 7200s |
| Update every | 1s | 2s | 1s |
| Memory mode | dbengine | ram | dbengine |

### 磁盘优化

| 设置 | 描述 | 推荐 |
|------|------|------|
| dbengine disk space | 最大磁盘使用 | 每节点 1-10GB |
| dbengine pages | 内存页 | 32-128 |
| Cleanup | 移除旧数据 | 启用 |

### CPU 优化

| 设置 | 影响 | 推荐 |
|------|------|------|
| 更新频率 | CPU 使用率 | 1-5 秒 |
| 显示图表 | 渲染 | 限制仪表板 |
| 收集器 | 数据收集 | 禁用未使用的 |

### 网络优化

| 设置 | 描述 | 推荐 |
|------|------|------|
| 压缩 | 流数据 | 为 children 启用 |
| 缓冲区大小 | 流缓冲 | 默认 10MB |
| 超时 | 连接超时 | 60s |

### 监控 Netdata 本身

| 指标 | 关注内容 | 阈值 |
|------|----------|------|
| CPU 使用率 | Netdata 进程 | < 2% |
| 内存 | RAM 消耗 | < 512MB |
| 磁盘 I/O | 写操作 | < 10MB/s |
| 网络 | 流带宽 | < 10Mbps |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 安装 | 一键安装快速设置 |
| 仪表板 | 实时、交互式可视化 |
| 告警 | 灵活的阈值和通知 |
| 架构 | Parent-Child 支持扩展 |
| 集成 | 自动检测多种服务 |
| 性能 | 可针对任何环境调优 |


---

## 来源：uptime.md

## 简介

Beszel 是一个轻量级的自托管系统监控平台，用于跟踪服务器的长期性能表现。它通过简洁的 Web 界面提供实时指标可视化、历史数据分析和告警功能。

本教程涵盖安装、配置、Agent 设置以及如何有效使用 Beszel 监控基础设施。

## 架构概览

Beszel 采用 Hub-Agent 模型：

| 组件 | 角色 | 描述 |
|------|------|------|
| Hub | 中心服务器 | 收集和存储指标，提供 Web UI |
| Agent | 数据采集器 | 运行在每台被监控主机上，向 Hub 报告 |
| Web UI | 仪表板 | 基于浏览器的可视化界面 |
| Database | 存储 | SQLite 或 PostgreSQL 持久化存储指标 |

## 前置条件

安装 Beszel 前，请确保满足以下要求：

| 要求 | 最低配置 | 推荐配置 |
|------|----------|----------|
| RAM | 256 MB | 512 MB |
| 磁盘空间 | 500 MB | 2 GB |
| 操作系统 | Linux, macOS | Ubuntu 22.04+ |
| Docker | 20.10+ | 24.0+ |
| 端口 | 8090 | 可自定义 |

## 安装 Hub

### 使用 Docker Compose

创建 Hub 的 `docker-compose.yml` 文件：

```yaml
version: "3.8"
services:
  beszel:
    image: henrygd/beszel:latest
    container_name: beszel
    restart: unless-stopped
    ports:
      - "8090:8090"
    volumes:
      - ./beszel_data:/beszel_data
    environment:
      - BESZEL_ADMIN_EMAIL=admin@example.com
```

启动 Hub：

```bash
docker compose up -d
```

通过 `http://your-server:8090` 访问 Web 界面。

### 安装后步骤

| 步骤 | 操作 | 详情 |
|------|------|------|
| 1 | 创建管理员账户 | 首次访问时设置邮箱和密码 |
| 2 | 配置设置 | 设置数据保留策略和通知偏好 |
| 3 | 生成 SSH 密钥 | 复制公钥用于 Agent 认证 |
| 4 | 添加首个系统 | 使用密钥连接 Agent |

## 安装 Agent

Agent 运行在每台需要监控的服务器上，负责收集系统指标并报告给 Hub。

### Docker Agent

在每台被监控主机上使用 Docker 部署 Agent：

```yaml
version: "3.8"
services:
  beszel-agent:
    image: henrygd/beszel-agent:latest
    container_name: beszel-agent
    restart: unless-stopped
    network_mode: host
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
    environment:
      - PORT=45876
      - KEY=your-ssh-public-key-here
```

### 独立 Agent

直接在主机上安装 Agent 二进制文件：

```bash
curl -sL https://github.com/henrygd/beszel/releases/latest/download/beszel-agent_linux_amd64.tar.gz | tar xz
./beszel-agent serve --port 45876 --key "your-ssh-public-key"
```

## 核心指标

Beszel 跟踪全面的系统指标：

### CPU 指标

| 指标 | 描述 | 单位 |
|------|------|------|
| CPU 使用率 | 总体处理器利用率 | 百分比 |
| CPU 温度 | 处理器温度读数 | 摄氏度 |
| 负载均值 | 1/5/15 分钟系统负载 | 计数 |
| 每核心使用率 | 单个核心利用率 | 百分比 |

### 内存指标

| 指标 | 描述 | 单位 |
|------|------|------|
| 总内存 | 已安装 RAM | 字节 |
| 已用内存 | 当前已分配 RAM | 字节 |
| 可用内存 | 空闲加可回收内存 | 字节 |
| Swap 使用量 | 交换空间消耗 | 字节 |
| 缓存 | 页面缓存使用量 | 字节 |

### 磁盘指标

| 指标 | 描述 | 单位 |
|------|------|------|
| 磁盘使用量 | 每个分区消耗的空间 | 字节 |
| 读取速率 | 磁盘读取吞吐量 | 字节/秒 |
| 写入速率 | 磁盘写入吞吐量 | 字节/秒 |
| IOPS | 每秒输入/输出操作数 | 计数 |
| 磁盘温度 | 驱动器温度读数 | 摄氏度 |

### 网络指标

| 指标 | 描述 | 单位 |
|------|------|------|
| 入站带宽 | 传入数据速率 | 字节/秒 |
| 出站带宽 | 传出数据速率 | 字节/秒 |
| 总接收量 | 累计传入数据 | 字节 |
| 总发送量 | 累计传出数据 | 字节 |
| 活跃连接数 | 当前网络连接数 | 计数 |

## Docker 容器监控

Beszel 可以监控主机上运行的各个 Docker 容器：

| 指标 | 描述 | 单位 |
|------|------|------|
| CPU 使用率 | 容器 CPU 消耗 | 百分比 |
| 内存使用量 | 容器内存分配 | 字节 |
| 网络 RX | 容器接收的数据 | 字节 |
| 网络 TX | 容器发送的数据 | 字节 |
| 块读取 | 容器磁盘读取 | 字节 |
| 块写入 | 容器磁盘写入 | 字节 |
| 状态 | 容器状态 | 文本 |

要启用 Docker 监控，请确保 Docker socket 已挂载到 Agent 容器中。

## 告警配置

设置告警以在指标超过阈值时接收通知：

### 告警类型

| 类型 | 触发条件 | 示例 |
|------|----------|------|
| CPU 告警 | 使用率超过阈值 | CPU > 90% 持续 5 分钟 |
| 内存告警 | RAM 使用率超过限制 | 内存 > 85% |
| 磁盘告警 | 存储接近满容量 | 磁盘 > 90% 满 |
| 网络告警 | 带宽超过限制 | 流量 > 100 Mbps |
| 状态告警 | 主机不可达 | 2 分钟无数据 |

### 创建告警规则

1. 在 Web UI 中导航到目标系统
2. 打开告警部分
3. 选择指标类型
4. 设置阈值和持续时间
5. 选择通知方式
6. 保存规则

## Web 仪表板

Beszel 仪表板提供多种可视化选项：

| 视图 | 用途 | 内容 |
|------|------|------|
| 概览 | 系统摘要 | 所有主机及其状态指示器 |
| 系统详情 | 单主机分析 | 单台主机的所有指标 |
| 历史 | 趋势分析 | 可选时间范围的时间序列图表 |
| Docker 视图 | 容器指标 | 每个容器的资源使用情况 |

### 仪表板导航

| 操作 | 方法 |
|------|------|
| 选择时间范围 | 使用标题栏中的范围选择器 |
| 缩放图表 | 在时间序列图表上点击并拖动 |
| 切换主机 | 使用侧边栏导航 |
| 导出数据 | 使用任意图表上的导出按钮 |
| 刷新数据 | 点击刷新图标或启用自动刷新 |

## 数据保留

配置 Beszel 存储历史数据的时长：

| 保留期限 | 存储影响 | 使用场景 |
|----------|----------|----------|
| 7 天 | 低 | 开发环境 |
| 30 天 | 中 | 标准监控 |
| 90 天 | 高 | 生产环境 |
| 365 天 | 非常高 | 合规要求 |

在 Hub 配置文件或 Web UI 设置面板中编辑保留设置。

## 备份与恢复

### 备份数据

```bash
# 停止 Hub 容器
docker compose down

# 备份数据目录
tar czf beszel-backup-$(date +%Y%m%d).tar.gz ./beszel_data

# 重启 Hub
docker compose up -d
```

### 从备份恢复

```bash
docker compose down
tar xzf beszel-backup-20260101.tar.gz
docker compose up -d
```

## 性能调优

| 设置 | 默认值 | 影响 | 建议 |
|------|--------|------|------|
| 采集间隔 | 30 秒 | 数据粒度 | 15-60 秒 |
| 数据库类型 | SQLite | 写入性能 | 大规模部署使用 PostgreSQL |
| 最大连接数 | 50 | 内存使用 | 根据主机数量调整 |
| 缓存 TTL | 300 秒 | UI 响应速度 | 实时需求可降低 |

## 多网络配置

跨不同网络监控主机：

| 网络设置 | 方法 | 安全性 |
|----------|------|--------|
| 同一局域网 | 直接 Agent 连接 | SSH 密钥认证 |
| 通过 VPN 远程 | VPN 隧道到 Hub | VPN 加密加 SSH 密钥 |
| 通过反向代理远程 | Nginx 或 Caddy 代理 | TLS 加 SSH 密钥 |
| 云托管 Hub | 公共端点 | TLS 加防火墙规则 |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| Agent 无法连接 | SSH 密钥不正确 | 重新生成并更新密钥 |
| 无 Docker 指标 | Socket 未挂载 | 挂载 `/var/run/docker.sock` |
| 内存使用过高 | 主机过多 | 增加 Hub 资源或减少保留期 |
| 磁盘数据缺失 | 权限不足 | 以提升权限运行 Agent |
| 仪表板响应慢 | 数据集过大 | 切换到 PostgreSQL 后端 |

## 总结

Beszel 提供了一个高效的自托管解决方案，用于跨多台主机监控系统资源。其 Hub-Agent 架构可灵活扩展，轻量级设计确保对被监控系统的开销最小。

关键要点：

- 部署一次 Hub，然后为每台服务器添加 Agent
- 监控 CPU、内存、磁盘、网络和 Docker 容器
- 配置告警以主动通知问题
- 根据运维需求调整数据保留策略
- 使用 Docker Compose 简化部署和更新


---

## 来源：uptime2.md

## 简介

Uptime Kuma 是一个自托管监控工具，用于跟踪网站、API 和服务的可用性和性能。它提供实时状态页面和通知告警。

### 什么是 Uptime Kuma？

Uptime Kuma 监控您的服务，并在服务宕机时通知您。它提供了一个简洁的仪表盘和公开状态页面。

| 特性 | 描述 |
|------|------|
| 监控 | HTTP、TCP、DNS、Docker 检查 |
| 通知 | 邮件、Slack、Discord、Telegram |
| 状态页面 | 公开或私有状态展示 |
| 多语言 | 支持多种语言 |
| 2FA | 双因素认证 |

### 与其他方案的比较

| 特性 | Uptime Kuma | UptimeRobot | Pingdom |
|------|------------|-------------|---------|
| 自托管 | 是 | 否 | 否 |
| 免费 | 是 | 免费增值 | 否 |
| 状态页面 | 是 | 是 | 是 |
| 通知 | 80+ 服务 | 邮件、短信 | 邮件、短信 |
| Docker 支持 | 是 | N/A | N/A |

## 安装

### Docker 安装

```bash
docker run -d \
  --restart=always \
  -p 3001:3001 \
  -v uptime-kuma:/app/data \
  --name uptime-kuma \
  louislam/uptime-kuma
```

### Docker Compose

```yaml
version: '3'
services:
  uptime-kuma:
    image: louislam/uptime-kuma
    container_name: uptime-kuma
    ports:
      - "3001:3001"
    volumes:
      - uptime-kuma:/app/data
    restart: unless-stopped

volumes:
  uptime-kuma:
```

### 手动安装

```bash
git clone https://github.com/louislam/uptime-kuma.git
cd uptime-kuma
npm install
npm run build
node server/server.js
```

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2 核 |
| 内存 | 256 MB | 512 MB |
| 存储 | 1 GB | 5 GB |
| Node.js | 18+ | 20+ |

## 初始设置

### 首次登录

1. 访问 http://localhost:3001
2. 创建管理员账户
3. 添加第一个监控

### 配置文件

```env
# .env
UPTIME_KUMA_PORT=3001
UPTIME_KUMA_HOST=0.0.0.0
NODE_ENV=production
```

## 监控类型

### HTTP 监控

| 设置 | 描述 |
|------|------|
| URL | 要检查的端点 |
| 方法 | GET、POST、HEAD |
| 间隔 | 检查频率 |
| 超时 | 响应超时时间 |
| 状态码 | 期望的 HTTP 码 |

### HTTP 监控配置

```yaml
Name: Website
URL: https://example.com
Method: GET
Interval: 60 seconds
Timeout: 10 seconds
Retry: 3
Accepted Status Codes: 200-299
```

### TCP 监控

| 设置 | 描述 |
|------|------|
| 主机名 | 服务器地址 |
| 端口 | 端口号 |
| 间隔 | 检查频率 |

### DNS 监控

| 设置 | 描述 |
|------|------|
| 域名 | 要解析的域名 |
| 解析器 | DNS 服务器 |
| 记录类型 | A、AAAA、CNAME、MX |

### Docker 监控

| 设置 | 描述 |
|------|------|
| Docker 主机 | Docker daemon URL |
| 容器 | 容器名称或 ID |
| 检查类型 | 运行状态 |

### 监控类型汇总

| 类型 | 用例 |
|------|------|
| HTTP | 网站、API |
| TCP | 数据库、SSH、自定义端口 |
| DNS | 域名解析 |
| Docker | 容器状态 |
| Ping | 服务器可达性 |
| Steam | 游戏服务器 |
| Push | 心跳监控 |

## 通知渠道

### 支持的服务

| 服务 | 类别 |
|------|------|
| Email (SMTP) | 邮件 |
| Slack | 团队聊天 |
| Discord | 社区 |
| Telegram | 消息 |
| Webhook | 自定义 |
| PagerDuty | 事件管理 |
| Gotify | 自托管推送 |
| Matrix | 去中心化聊天 |

### 邮件配置

```yaml
Type: SMTP
Hostname: smtp.gmail.com
Port: 465
Username: your-email@gmail.com
Password: app-password
From: your-email@gmail.com
To: recipient@example.com
Secure: SSL/TLS
```

### Slack 配置

```yaml
Type: Slack
Webhook URL: https://hooks.slack.com/services/xxx/yyy/zzz
Channel: #alerts
Username: Uptime Kuma
Icon Emoji: :warning:
```

### Discord 配置

```yaml
Type: Discord
Webhook URL: https://discord.com/api/webhooks/xxx/yyy
```

### 通知触发器

| 触发器 | 描述 |
|--------|------|
| Up | 服务恢复 |
| Down | 服务宕机 |
| Testing | 测试通知 |

## 状态页面

### 创建状态页面

1. 导航到 Status Pages
2. 点击 "Add New Status Page"
3. 配置标题和 URL
4. 添加要展示的监控

### 状态页面设置

| 设置 | 描述 |
|------|------|
| 标题 | 页面标题 |
| URL slug | 公开 URL 路径 |
| 描述 | 页面描述 |
| 主题 | 亮色或暗色 |
| 自定义 CSS | 自定义样式 |

### 公开与私有

| 类型 | 访问 |
|------|------|
| 公开 | 任何有链接的人 |
| 私有 | 需要登录 |

### 自定义域名

```nginx
server {
    listen 80;
    server_name status.example.com;

    location / {
        proxy_pass http://localhost:3001/status/mypage;
        proxy_set_header Host $host;
    }
}
```

## 事件管理

### 创建事件

1. 进入状态页面
2. 点击 "Add Incident"
3. 输入标题和内容
4. 选择受影响的监控

### 事件状态

| 状态 | 含义 |
|------|------|
| Investigating | 正在调查问题 |
| Identified | 已找到根本原因 |
| Monitoring | 已修复，观察中 |
| Resolved | 问题已解决 |

## 分组和标签

### 监控分组

将监控组织为逻辑分组：

```
Websites
├── Main Website
├── Blog
└── API

Infrastructure
├── Database Server
├── Cache Server
└── Load Balancer
```

### 标签

| 标签 | 颜色 | 用途 |
|------|------|------|
| Production | 红色 | 关键服务 |
| Staging | 黄色 | 测试环境 |
| Internal | 蓝色 | 内部工具 |
| External | 绿色 | 公开服务 |

## 数据保留和备份

### 数据保留

```env
# 保留数据 365 天
KEEP_DATA_PERIOD=365
```

### 备份方式

| 方式 | 描述 |
|------|------|
| 导出 | 从 UI 导出 JSON |
| Docker volume | 备份 Docker volume |
| 文件系统 | 复制数据目录 |

### 备份脚本

```bash
#!/bin/bash
docker exec uptime-kuma \
  node -e "const {exportData} = require('./server/export'); \
  exportData().then(data => console.log(JSON.stringify(data)))" \
  > backup.json
```

## API 访问

### API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/status/page/{slug}` | GET | 状态页面数据 |
| `/api/monitors` | GET | 列出监控 |
| `/api/monitor/{id}` | GET | 监控详情 |

### 身份验证

```bash
# 从 Settings > API 获取 API 令牌
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://status.example.com/api/monitors
```

## 反向代理设置

### Nginx 配置

```nginx
server {
    listen 80;
    server_name status.example.com;

    location / {
        proxy_pass http://localhost:3001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### SSL 配置

```bash
# 安装 Certbot
sudo apt install certbot python3-certbot-nginx

# 获取 SSL 证书
sudo certbot --nginx -d status.example.com
```

## 性能调优

### 数据库优化

| 设置 | 建议 |
|------|------|
| 数据库 | SQLite（默认）或 MariaDB |
| 索引 | 监控自动索引 |
| 清理 | 定期数据修剪 |

### 资源限制

```yaml
# docker-compose.yml
services:
  uptime-kuma:
    deploy:
      resources:
        limits:
          cpus: '1.0'
          memory: 512M
```

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 通知未发送 | 配置错误 | 测试通知设置 |
| CPU 使用率高 | 监控过多 | 增加检查间隔 |
| WebSocket 错误 | 代理配置错误 | 配置 WebSocket 支持 |
| 数据库锁定 | 并发写入 | 生产环境使用 MariaDB |

### 日志

```bash
# 查看日志
docker logs uptime-kuma

# 跟踪日志
docker logs -f uptime-kuma
```

## 总结

| 功能 | 用途 |
|------|------|
| 监控 | 跟踪服务可用性 |
| 通知 | 宕机告警 |
| 状态页面 | 展示服务状态 |
| 分组 | 组织监控 |
| API | 编程访问 |


---

## 来源：metrics.md

## 简介

Prometheus 是一个开源监控和告警工具包，专为可靠性和可扩展性设计。它从配置的目标收集指标，存储在时序数据库中，并支持使用 PromQL 进行查询。

## 目录

1. [架构概览](#架构概览)
2. [安装](#安装)
3. [配置](#配置)
4. [指标类型](#指标类型)
5. [PromQL 查询](#promql-查询)
6. [告警规则](#告警规则)
7. [Exporter](#exporter)
8. [Grafana 集成](#grafana-集成)

## 架构概览

### 核心组件

| 组件 | 用途 |
|------|------|
| Prometheus Server | 抓取和存储指标 |
| Pushgateway | 接收推送的指标 |
| Alertmanager | 处理告警通知 |
| Exporter | 从服务暴露指标 |
| Web UI | 内置表达式浏览器 |

### 数据流程

| 步骤 | 过程 |
|------|------|
| 1 | Prometheus 按配置间隔抓取目标 |
| 2 | 指标存储在本地时序数据库 |
| 3 | PromQL 查询针对存储数据执行 |
| 4 | 基于规则触发告警 |
| 5 | Alertmanager 路由通知 |

## 安装

### Docker Compose

```yaml
# docker-compose.yml
services:
  prometheus:
    image: prom/prometheus:latest
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml
      - prometheus_data:/prometheus
    command:
      - '--config.file=/etc/prometheus/prometheus.yml'
      - '--storage.tsdb.path=/prometheus'
      - '--storage.tsdb.retention.time=15d'

  alertmanager:
    image: prom/alertmanager:latest
    ports:
      - "9093:9093"
    volumes:
      - ./alertmanager.yml:/etc/alertmanager/alertmanager.yml

volumes:
  prometheus_data:
```

### 二进制安装

| 步骤 | 命令 |
|------|------|
| 1 | 从 prometheus.io 下载 |
| 2 | 解压归档 |
| 3 | 编辑 prometheus.yml |
| 4 | 运行 `./prometheus --config.file=prometheus.yml` |

## 配置

### 主配置

```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

alerting:
  alertmanagers:
    - static_configs:
        - targets: ['alertmanager:9093']

rule_files:
  - "alert_rules.yml"

scrape_configs:
  - job_name: 'prometheus'
    static_configs:
      - targets: ['localhost:9090']

  - job_name: 'node'
    static_configs:
      - targets: ['node-exporter:9100']
```

### 全局设置

| 设置 | 默认值 | 说明 |
|------|--------|------|
| `scrape_interval` | 15s | 抓取频率 |
| `evaluation_interval` | 15s | 规则评估频率 |
| `scrape_timeout` | 10s | 抓取请求超时 |
| `external_labels` | 无 | 联邦标签 |

### 抓取配置

| 参数 | 说明 | 示例 |
|------|------|------|
| `job_name` | 唯一作业标识符 | `my_app` |
| `metrics_path` | 抓取端点 | `/metrics` |
| `scheme` | HTTP 或 HTTPS | `http` |
| `static_configs` | 固定目标列表 | `['host:port']` |
| `file_sd_configs` | 基于文件的发现 | JSON/YAML 文件 |

### 服务发现

| 方式 | 配置 |
|------|------|
| 静态 | 直接列出目标 |
| 文件 | JSON/YAML 文件包含目标 |
| DNS | SRV 记录 |
| Kubernetes | Pod/服务发现 |
| Consul | 服务目录 |
| EC2 | AWS 实例发现 |

## 指标类型

### 类型对比

| 类型 | 说明 | 使用场景 |
|------|------|----------|
| Counter | 单调递增 | 请求、错误 |
| Gauge | 可增可减 | 温度、内存 |
| Histogram | 值分布 | 请求持续时间 |
| Summary | 类似 histogram | 分位数 |

### Counter

```python
# Python 示例
from prometheus_client import Counter

requests_total = Counter(
    'http_requests_total',
    'Total HTTP requests',
    ['method', 'endpoint']
)

requests_total.labels(method='GET', endpoint='/api').inc()
```

### Gauge

```python
from prometheus_client import Gauge

temperature = Gauge(
    'room_temperature_celsius',
    'Current room temperature'
)

temperature.set(22.5)
temperature.inc(0.5)
temperature.dec(1.0)
```

### Histogram

```python
from prometheus_client import Histogram

request_duration = Histogram(
    'http_request_duration_seconds',
    'Request duration in seconds',
    buckets=[0.01, 0.05, 0.1, 0.5, 1.0, 5.0]
)

with request_duration.time():
    process_request()
```

### 命名规范

| 组件 | 规范 | 示例 |
|------|------|------|
| 命名空间 | 应用名称 | `myapp` |
| 子系统 | 组件 | `http` |
| 名称 | 基础指标 | `requests_total` |
| 单位 | 度量单位 | `_seconds` |
| 全名 | `{namespace}_{subsystem}_{name}_{unit}` | `myapp_http_requests_total` |

## PromQL 查询

### 基础查询

| 查询 | 说明 |
|------|------|
| `http_requests_total` | 所有请求计数器 |
| `http_requests_total{method="GET"}` | 按标签过滤 |
| `http_requests_total{status=~"5.."}` | 正则过滤 |
| `rate(http_requests_total[5m])` | 每秒速率 |

### 速率函数

| 函数 | 说明 | 使用场景 |
|------|------|----------|
| `rate()` | 每秒速率 | Counter |
| `irate()` | 瞬时速率 | 短期峰值 |
| `increase()` | 总增长 | 某时间段的 Counter |
| `delta()` | 差值 | Gauge |

### 聚合

| 函数 | 说明 |
|------|------|
| `sum()` | 跨维度求和 |
| `avg()` | 平均值 |
| `min()` | 最小值 |
| `max()` | 最大值 |
| `count()` | 时间序列数量 |
| `topk(5, metric)` | 前 5 个值 |

### 聚合示例

```promql
# 按方法统计总请求
sum by (method) (rate(http_requests_total[5m]))

# 平均响应时间
avg(rate(http_request_duration_seconds_sum[5m]) / 
    rate(http_request_duration_seconds_count[5m]))

# 第 95 百分位
histogram_quantile(0.95, rate(http_request_duration_seconds_bucket[5m]))
```

### 比较操作符

| 操作符 | 说明 | 示例 |
|--------|------|------|
| `==` | 等于 | `status == 200` |
| `!=` | 不等于 | `status != 500` |
| `>` | 大于 | `value > 100` |
| `<` | 小于 | `value < 50` |
| `>=` | 大于等于 | `value >= 100` |
| `<=` | 小于等于 | `value <= 50` |

## 告警规则

### 规则结构

```yaml
# alert_rules.yml
groups:
  - name: example
    rules:
      - alert: HighErrorRate
        expr: rate(http_requests_total{status=~"5.."}[5m]) > 0.1
        for: 5m
        labels:
          severity: critical
        annotations:
          summary: High error rate detected
          description: "Error rate is {{ $value }} per second"
```

### 告警状态

| 状态 | 说明 |
|------|------|
| Inactive | 条件未满足 |
| Pending | 条件已满足，等待 `for` 持续时间 |
| Firing | 条件在整个持续时间内满足 |

### 严重级别

| 标签 | 使用场景 | 响应 |
|------|----------|------|
| `critical` | 服务宕机 | 立即处理 |
| `warning` | 性能下降 | 需要处理 |
| `info` | 值得注意的事件 | 稍后审查 |

### Alertmanager 配置

```yaml
# alertmanager.yml
route:
  group_by: ['alertname']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 4h
  receiver: 'email'

receivers:
  - name: 'email'
    email_configs:
      - to: 'team@example.com'
        from: 'alertmanager@example.com'
        smarthost: 'smtp.example.com:587'

  - name: 'slack'
    slack_configs:
      - api_url: 'https://hooks.slack.com/...'
        channel: '#alerts'
```

## Exporter

### 常见 Exporter

| Exporter | 监控对象 | 默认端口 |
|----------|----------|----------|
| Node Exporter | 系统指标 | 9100 |
| cAdvisor | Docker 容器 | 8080 |
| MySQL Exporter | MySQL 数据库 | 9104 |
| Redis Exporter | Redis 实例 | 9121 |
| Nginx Exporter | Nginx Web 服务器 | 9113 |
| Blackbox Exporter | HTTP/TCP 探测 | 9115 |

### Node Exporter 指标

| 指标 | 说明 |
|------|------|
| `node_cpu_seconds_total` | CPU 使用率 |
| `node_memory_MemTotal_bytes` | 总内存 |
| `node_filesystem_size_bytes` | 磁盘大小 |
| `node_network_receive_bytes_total` | 网络接收 |
| `node_load1` | 1 分钟负载均值 |

### 应用埋点

| 语言 | 客户端库 |
|------|----------|
| Python | `prometheus_client` |
| Go | `prometheus/client_golang` |
| Java | `io.prometheus:simpleclient` |
| Node.js | `prom-client` |
| Ruby | `prometheus-client` |

## Grafana 集成

### 添加 Prometheus 数据源

| 步骤 | 设置 |
|------|------|
| 1 | 在端口 3000 打开 Grafana |
| 2 | 导航到 Configuration > Data Sources |
| 3 | 点击 Add data source |
| 4 | 选择 Prometheus |
| 5 | 设置 URL 为 `http://prometheus:9090` |
| 6 | 点击 Save & Test |

### 常用仪表盘面板

| 面板类型 | 使用场景 |
|----------|----------|
| Graph | 时序可视化 |
| Singlestat | 单值显示 |
| Table | 表格数据 |
| Heatmap | Histogram 可视化 |
| Alert list | 活跃告警 |

### 示例仪表盘查询

| 面板 | PromQL 查询 |
|------|-------------|
| 请求速率 | `sum(rate(http_requests_total[5m]))` |
| 错误速率 | `sum(rate(http_requests_total{status=~"5.."}[5m]))` |
| CPU 使用率 | `100 - (avg(rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)` |
| 内存使用率 | `(1 - node_memory_MemAvailable_bytes/node_memory_MemTotal_bytes) * 100` |
| 磁盘使用率 | `(1 - node_filesystem_avail_bytes/node_filesystem_size_bytes) * 100` |

## 存储与保留

### 存储设置

| 设置 | 默认值 | 说明 |
|------|--------|------|
| `storage.tsdb.path` | `data/` | 数据目录 |
| `storage.tsdb.retention.time` | 15d | 数据保留时间 |
| `storage.tsdb.retention.size` | 0（无限制） | 最大存储大小 |
| `storage.tsdb.wal-compression` | false | 压缩 WAL |

### 容量规划

| 因素 | 考虑事项 |
|------|----------|
| 活跃序列 | 唯一时序数量 |
| 抓取间隔 | 指标收集频率 |
| 保留期 | 数据保存时长 |
| 基数 | 标签组合数量 |

## 总结

Prometheus 提供了一个强大的监控解决方案，具有基于拉取的架构、强大的查询语言和丰富的生态系统。它与 Grafana 的可视化集成和 Alertmanager 的通知集成创建了一个完整的监控栈，适用于开发和生产环境。


---
