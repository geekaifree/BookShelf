# Netdata：基础设施监控指南

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
