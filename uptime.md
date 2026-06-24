# 使用 Beszel 进行系统监控

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
