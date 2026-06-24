# 使用 Prometheus 进行指标监控

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
