# 知识宝库：工具与技术

## 简介

本指南是为系统管理员、DevOps 工程师、安全专业人员和高级用户精心整理的工具、资源和技术集合。涵盖命令行工具、网络、安全、容器、监控等领域。

## 目录

- [命令行工具](#命令行工具)
- [文本编辑器](#文本编辑器)
- [网络](#网络)
- [安全](#安全)
- [容器](#容器)
- [监控](#监控)
- [操作系统工具](#操作系统工具)
- [Shell 脚本](#shell-脚本)
- [数据库](#数据库)
- [Web 服务器](#web-服务器)
- [备份方案](#备份方案)
- [云工具](#云工具)

---

## 命令行工具

命令行是系统管理最强大的界面。这些工具扩展了它的能力。

### 文件和目录工具

| 工具 | 用途 | 平台 | 安装 |
|------|------|------|------|
| ripgrep (rg) | 快速递归搜索 | 全平台 | `apt install ripgrep` |
| fd | 快速 find 替代 | 全平台 | `apt install fd-find` |
| fzf | 模糊查找器 | 全平台 | `apt install fzf` |
| bat | 带语法高亮的 cat | 全平台 | `apt install bat` |
| exa/eza | 现代 ls 替代 | 全平台 | `apt install exa` |
| dust | 磁盘使用分析器 | 全平台 | `cargo install du-dust` |
| duf | 现代 df 替代 | 全平台 | `apt install duf` |
| ncdu | NCurses 磁盘使用 | 全平台 | `apt install ncdu` |
| ranger | 文件管理器（Vim 风格） | 全平台 | `apt install ranger` |
| midnight commander | 文件管理器（Norton 风格） | 全平台 | `apt install mc` |

### 文本处理

| 工具 | 用途 | 示例 |
|------|------|------|
| awk | 模式处理 | `awk '{print $1}' file` |
| sed | 流编辑器 | `sed 's/old/new/g' file` |
| jq | JSON 处理器 | `jq '.items[]' data.json` |
| yq | YAML 处理器 | `yq '.key' config.yml` |
| xsv | CSV 处理 | `xsv stats data.csv` |
| miller | 数据处理 | `mlr --csv cut -f name file.csv` |

### 系统监控

| 工具 | 用途 | 核心功能 |
|------|------|----------|
| htop | 进程查看器 | 交互式进程管理 |
| btop | 系统监控 | 精美 UI、GPU 支持 |
| glances | 系统监控 | 可选 Web 界面 |
| iotop | I/O 监控 | 按进程查看磁盘 I/O |
| nethogs | 按进程查看网络 | 按进程查看带宽 |
| iftop | 网络流量 | 实时带宽 |
| dstat | 系统统计 | CPU、磁盘、网络、内存综合 |

### 效率工具

| 工具 | 用途 | 核心功能 |
|------|------|----------|
| tmux | 终端复用器 | 持久会话 |
| screen | 终端复用器 | 传统、广泛可用 |
| zellij | 终端复用器 | 现代、用户友好 |
| direnv | 环境变量 | 按目录设置环境 |
| autojump | 目录导航 | 从使用中学习 |
| zoxide | 智能 cd | 更快的导航 |
| tldr | 简化版 man 页面 | 社区示例 |

---

## 文本编辑器

选择合适的编辑器对效率至关重要。

### 编辑器对比

| 编辑器 | 类型 | 学习曲线 | 可扩展性 | 速度 |
|--------|------|----------|----------|------|
| Vim/Neovim | 模态 | 高 | 非常高 | 非常快 |
| Emacs | 模态/标准 | 高 | 非常高 | 快 |
| VS Code | GUI | 低 | 高 | 中等 |
| Sublime Text | GUI | 低 | 中等 | 非常快 |
| Nano | 简单 | 非常低 | 低 | 快 |
| Micro | 简单 | 非常低 | 中等 | 快 |

### Vim 核心知识

| 模式 | 按键 | 用途 |
|------|------|------|
| 普通模式 | Esc | 导航、命令 |
| 插入模式 | i、a、o | 文本输入 |
| 可视模式 | v、V、Ctrl+v | 选择 |
| 命令模式 | : | Ex 命令 |

**常用 Vim 命令：**

| 命令 | 操作 |
|------|------|
| `dd` | 删除行 |
| `yy` | 复制行 |
| `p` | 粘贴 |
| `u` | 撤销 |
| `/pattern` | 搜索 |
| `:%s/old/new/g` | 全部替换 |
| `:w` | 保存 |
| `:q` | 退出 |

### Neovim 配置

现代 Neovim 使用 Lua 进行配置：

```lua
-- 基本设置
vim.opt.number = true
vim.opt.relativenumber = true
vim.opt.tabstop = 4
vim.opt.shiftwidth = 4
vim.opt.expandtab = true

-- 插件管理器 (lazy.nvim)
require("lazy").setup({
    "nvim-telescope/telescope.nvim",
    "nvim-treesitter/nvim-treesitter",
    "neovim/nvim-lspconfig",
})
```

---

## 网络

网络诊断、监控和管理的工具与技术。

### 网络诊断工具

| 工具 | 用途 | 平台 |
|------|------|------|
| ping | 连通性测试 | 全平台 |
| traceroute/mtr | 路由追踪 | 全平台 |
| dig/nslookup | DNS 查询 | 全平台 |
| netstat/ss | Socket 统计 | 全平台 |
| nmap | 网络扫描 | 全平台 |
| tcpdump | 数据包捕获 | Linux/macOS |
| wireshark | 数据包分析 | 全平台 |
| curl | HTTP 客户端 | 全平台 |
| iperf3 | 带宽测试 | 全平台 |

### DNS 工具

| 工具 | 用途 | 示例 |
|------|------|------|
| dig | DNS 查询 | `dig example.com A` |
| host | 简单 DNS 查询 | `host example.com` |
| nslookup | DNS 查询 (Windows) | `nslookup example.com` |
| drill | DNS 查询 (LDNS) | `drill example.com` |
| dog | 现代 DNS 客户端 | `dog example.com` |

### 常见 DNS 记录类型

| 类型 | 用途 | 示例 |
|------|------|------|
| A | IPv4 地址 | `example.com -> 93.184.216.34` |
| AAAA | IPv6 地址 | `example.com -> 2606:2800:220:1:...` |
| CNAME | 别名 | `www.example.com -> example.com` |
| MX | 邮件服务器 | `example.com -> mail.example.com` |
| TXT | 文本记录 | SPF、DKIM、域名验证 |
| NS | 名称服务器 | `example.com -> ns1.example.com` |
| SRV | 服务记录 | `_http._tcp.example.com` |

### 防火墙工具

| 工具 | 平台 | 类型 |
|------|------|------|
| iptables | Linux | 内核级包过滤 |
| nftables | Linux | 现代 iptables 替代 |
| ufw | Linux | iptables 前端 |
| firewalld | Linux | 动态防火墙管理 |
| pf | macOS/BSD | 包过滤 |
| Windows Firewall | Windows | 内置防火墙 |

### SSH 工具和配置

| 工具/功能 | 用途 |
|-----------|------|
| ssh-keygen | 生成密钥对 |
| ssh-copy-id | 复制公钥到服务器 |
| ssh-agent | 在内存中管理密钥 |
| ProxyJump | 通过跳板机连接 |
| ControlMaster | 多路复用连接 |
| 端口转发 | 通过 SSH 隧道传输流量 |

**常用 SSH 配置 (~/.ssh/config)：**

```
Host *
    ServerAliveInterval 60
    ServerAliveCountMax 3
    ControlMaster auto
    ControlPath ~/.ssh/sockets/%r@%h-%p
    ControlPersist 600

Host bastion
    HostName bastion.example.com
    User admin
    Port 22

Host internal
    HostName 10.0.1.50
    ProxyJump bastion
    User deploy
```

---

## 安全

系统和应用安全的工具与实践。

### 漏洞扫描

| 工具 | 类型 | 用途 |
|------|------|------|
| OpenVAS | 扫描器 | 网络漏洞评估 |
| Nessus | 扫描器 | 全面漏洞扫描 |
| Nikto | 扫描器 | Web 服务器扫描 |
| OWASP ZAP | 代理/扫描器 | Web 应用安全 |
| Burp Suite | 代理/扫描器 | Web 应用渗透测试 |
| sqlmap | 工具 | SQL 注入检测和利用 |
| nuclei | 扫描器 | 基于模板的漏洞扫描 |

### 密码工具

| 工具 | 用途 | 类型 |
|------|------|------|
| hashcat | 密码破解 | GPU 加速 |
| John the Ripper | 密码破解 | 基于 CPU |
| Hydra | 在线密码暴力破解 | 网络 |
| KeePassXC | 密码管理器 | 本地存储 |
| Bitwarden | 密码管理器 | 云/自托管 |

### 加密工具

| 工具 | 用途 | 类型 |
|------|------|------|
| GPG | 文件/邮件加密 | 非对称加密 |
| age | 文件加密 | 现代、简单 |
| OpenSSL | 证书/加密工具包 | 库/CLI |
| WireGuard | VPN | 现代、快速 |
| OpenVPN | VPN | 传统、广泛支持 |
| Let's Encrypt | TLS 证书 | 免费、自动化 |

### 安全扫描

| 工具 | 用途 | 目标 |
|------|------|------|
| Lynis | 系统审计 | Linux/macOS |
| ClamAV | 杀毒 | 全平台 |
| rkhunter | Rootkit 检测 | Linux |
| chkrootkit | Rootkit 检测 | Linux |
| AIDE | 文件完整性 | Linux |
| OSSEC | 主机 IDS | 全平台 |

### 安全最佳实践清单

| 类别 | 实践 | 优先级 |
|------|------|--------|
| 认证 | 禁用密码 SSH，使用密钥 | 关键 |
| 认证 | 尽可能启用 MFA | 关键 |
| 更新 | 自动安全更新 | 关键 |
| 防火墙 | 默认拒绝，允许特定端口 | 关键 |
| 日志 | 集中日志收集 | 高 |
| 监控 | 入侵检测系统 | 高 |
| 备份 | 加密异地备份 | 高 |
| 网络 | 用 VLAN 分段网络 | 中 |
| 访问 | 最小权限原则 | 关键 |
| 密钥 | 使用 vault 管理密钥 | 高 |

---

## 容器

应用打包和编排的容器技术。

### 容器运行时

| 运行时 | 类型 | 核心功能 |
|--------|------|----------|
| Docker | 完整平台 | 最广泛使用 |
| Podman | 无守护进程 | 默认无 root |
| containerd | 轻量级 | Kubernetes 使用 |
| CRI-O | Kubernetes 原生 | 轻量级 |
| LXC/LXD | 系统容器 | 完整 OS 容器 |

### Docker 常用命令

| 命令 | 用途 |
|------|------|
| `docker build -t name .` | 从 Dockerfile 构建镜像 |
| `docker run -d -p 80:80 name` | 后台运行容器 |
| `docker ps` | 列出运行中的容器 |
| `docker logs container_id` | 查看容器日志 |
| `docker exec -it container_id bash` | 进入运行中的容器 |
| `docker-compose up -d` | 从 compose 文件启动服务 |
| `docker system prune` | 清理未使用的资源 |

### Dockerfile 最佳实践

| 实践 | 原因 |
|------|------|
| 使用多阶段构建 | 更小的最终镜像 |
| 使用具体的 base image 标签 | 可复现的构建 |
| 最小化层数 | 更小的镜像、更快的构建 |
| 先复制依赖 | 更好的层缓存 |
| 以非 root 用户运行 | 安全性 |
| 使用 .dockerignore | 排除不必要的文件 |
| 使用健康检查 | 容器监控 |

### 容器编排

| 工具 | 类型 | 最佳用途 |
|------|------|----------|
| Kubernetes | 编排 | 大规模生产 |
| Docker Swarm | 编排 | 简单集群 |
| Nomad | 编排 | 多工作负载 |
| K3s | 轻量级 K8s | 边缘、IoT、ARM |
| K0s | 轻量级 K8s | 最小占用 |

### Kubernetes 核心概念

| 概念 | 描述 |
|------|------|
| Pod | 最小可部署单元（1+ 容器） |
| Service | Pod 的稳定网络端点 |
| Deployment | 声明式 Pod 管理 |
| ConfigMap | 配置数据 |
| Secret | 敏感数据（base64 编码） |
| Ingress | HTTP 路由到 Service |
| PersistentVolume | Pod 重启后保留的存储 |
| Namespace | 虚拟集群分区 |

---

## 监控

观察系统和应用健康的工具与实践。

### 监控栈组件

| 组件 | 用途 | 示例 |
|------|------|------|
| 指标收集 | 收集数值数据 | Prometheus、Telegraf、collectd |
| 指标存储 | 存储时序数据 | Prometheus、InfluxDB、VictoriaMetrics |
| 可视化 | 展示仪表板 | Grafana、Kibana |
| 告警 | 条件触发通知 | Alertmanager、PagerDuty |
| 日志收集 | 收集日志数据 | Fluentd、Logstash、Promtail |
| 日志存储 | 存储和搜索日志 | Elasticsearch、Loki |
| 追踪 | 分布式请求追踪 | Jaeger、Zipkin、Tempo |

### Prometheus 和 Grafana

最流行的开源监控栈：

| 组件 | 角色 |
|------|------|
| Prometheus | 抓取和存储指标 |
| Alertmanager | 处理来自 Prometheus 的告警 |
| Grafana | 在仪表板中可视化指标 |
| Node Exporter | 暴露主机指标 |
| cAdvisor | 暴露容器指标 |

### 关键监控指标（USE 方法）

| 资源 | 利用率 | 饱和度 | 错误 |
|------|--------|--------|------|
| CPU | 使用百分比 | 运行队列长度 | 机器检查 |
| 内存 | 使用百分比 | Swap 使用 | OOM kills |
| 磁盘 I/O | 繁忙百分比 | 队列长度 | I/O 错误 |
| 网络 | 使用带宽 | 数据包丢弃 | 接口错误 |

### 关键监控指标（RED 方法）

| 指标 | 描述 |
|------|------|
| Rate | 每秒请求数 |
| Errors | 每秒失败请求数 |
| Duration | 请求延迟分布 |

### 日志管理

| 工具 | 类型 | 核心功能 |
|------|------|----------|
| Elasticsearch + Kibana (ELK) | 栈 | 全文搜索、可视化 |
| Loki + Grafana | 栈 | 轻量级、基于标签 |
| Graylog | 平台 | 告警、流水线 |
| Fluentd | 收集器 | 统一日志层 |
| Promtail | 收集器 | Loki 兼容 |
| Vector | 收集器 | 高性能 |

---

## 操作系统工具

Linux 和 macOS 系统管理的核心工具。

### Linux 包管理器

| 发行版 | 管理器 | 命令 |
|--------|--------|------|
| Debian/Ubuntu | apt | `apt install package` |
| Red Hat/Fedora | dnf | `dnf install package` |
| Arch Linux | pacman | `pacman -S package` |
| Alpine | apk | `apk add package` |
| NixOS | nix | `nix-env -iA package` |

### 进程管理

| 命令 | 用途 |
|------|------|
| `ps aux` | 列出所有进程 |
| `top`/`htop` | 交互式进程查看器 |
| `kill PID` | 向进程发送信号 |
| `killall name` | 按名称终止 |
| `nice -n 10 command` | 以较低优先级运行 |
| `nohup command &` | 后台运行，退出登录后保留 |
| `systemctl start/stop/enable` | 管理 systemd 服务 |

### 磁盘和文件系统

| 命令 | 用途 |
|------|------|
| `df -h` | 磁盘空间使用 |
| `du -sh *` | 目录大小 |
| `lsblk` | 列出块设备 |
| `mount / unmount` | 挂载文件系统 |
| `fdisk` | 分区管理 |
| `mkfs` | 创建文件系统 |
| `fsck` | 检查文件系统 |

### 系统信息

| 命令 | 用途 |
|------|------|
| `uname -a` | 内核信息 |
| `lscpu` | CPU 信息 |
| `free -h` | 内存使用 |
| `lsusb` | USB 设备 |
| `lspci` | PCI 设备 |
| `dmidecode` | 硬件信息 |

---

## Shell 脚本

Shell 脚本自动化重复任务和系统管理。

### Bash 脚本基础

**脚本结构：**

```bash
#!/usr/bin/env bash
set -euo pipefail

# 变量
NAME="world"
echo "Hello, ${NAME}!"

# 条件判断
if [[ -f "/etc/passwd" ]]; then
    echo "File exists"
fi

# 循环
for file in *.txt; do
    echo "Processing: ${file}"
done

# 函数
greet() {
    local name="$1"
    echo "Hello, ${name}"
}
greet "User"
```

### 常用模式

| 模式 | 代码 |
|------|------|
| 逐行读取文件 | `while IFS= read -r line; do ... done < file` |
| 检查命令是否存在 | `command -v cmd &>/dev/null` |
| 解析参数 | `while getopts "a:b:" opt; do ... done` |
| 捕获信号 | `trap 'cleanup' EXIT` |
| 错误处理 | `set -euo pipefail` |

### 实用 Shell 单行命令

| 任务 | 命令 |
|------|------|
| 查找大文件 | `find / -type f -size +100M 2>/dev/null` |
| 统计文件行数 | `wc -l *.txt` |
| 按大小排序 | `ls -lhS` |
| 查找并替换 | `sed -i 's/old/new/g' file` |
| 去重 | `sort file \| uniq` |
| 提取列 | `awk '{print $1, $3}' file` |
| JSON 解析 | `curl -s url \| jq '.data'` |
| CSV 处理 | `cut -d',' -f1,3 data.csv` |

### 脚本最佳实践

| 实践 | 原因 |
|------|------|
| 使用 `set -euo pipefail` | 尽早捕获错误 |
| 引用变量 | 防止单词分割 |
| 使用 shellcheck | Shell 脚本静态分析 |
| 添加注释 | 解释非显而易见的逻辑 |
| 使用函数 | 可复用、可测试的代码 |
| 验证输入 | 防止意外行为 |
| 使用日志 | 调试和审计跟踪 |

---

## 数据库

数据库工具、客户端和管理工具。

### 数据库对比

| 数据库 | 类型 | 最佳用途 | 扩展方式 |
|--------|------|----------|----------|
| PostgreSQL | 关系型 | 复杂查询、数据完整性 | 垂直 + 读副本 |
| MySQL/MariaDB | 关系型 | Web 应用 | 垂直 + 读副本 |
| SQLite | 嵌入式 | 单用户、移动端 | 单文件 |
| MongoDB | 文档型 | 灵活模式 | 水平（分片） |
| Redis | 键值型 | 缓存、会话 | 集群模式 |
| Elasticsearch | 搜索 | 全文搜索、分析 | 水平 |
| ClickHouse | 列式 | 分析、OLAP | 水平 |
| InfluxDB | 时序 | 指标、IoT | 集群 |

### 数据库 CLI 工具

| 工具 | 数据库 | 用途 |
|------|--------|------|
| psql | PostgreSQL | 交互式终端 |
| mysql | MySQL | 交互式终端 |
| pgcli | PostgreSQL | 带自动补全的增强 CLI |
| mycli | MySQL | 带自动补全的增强 CLI |
| litecli | SQLite | 增强 CLI |
| redis-cli | Redis | 命令行客户端 |
| mongosh | MongoDB | MongoDB Shell |
| usql | 通用 | 通用 SQL CLI |

### 备份策略

| 策略 | 描述 | RPO | RTO |
|------|------|-----|-----|
| 全量备份 | 完整副本 | 长 | 快 |
| 增量备份 | 自上次备份以来的变更 | 短 | 中 |
| 持续备份 | WAL/binlog 传输 | 接近零 | 快 |
| 快照 | 时间点副本 | 可变 | 快 |

---

## Web 服务器

Web 服务器配置和管理。

### Web 服务器对比

| 服务器 | 类型 | 最佳用途 | 核心功能 |
|--------|------|----------|----------|
| Nginx | 反向代理/Web | 高并发 | 事件驱动 |
| Apache | Web 服务器 | 灵活性 | .htaccess、模块 |
| Caddy | Web 服务器 | 简单性 | 自动 HTTPS |
| Traefik | 反向代理 | 容器 | 自动发现 |
| HAProxy | 负载均衡 | 高可用 | TCP/HTTP 均衡 |

### Nginx 配置

**反向代理：**

```nginx
server {
    listen 80;
    server_name example.com;
    return 301 https://$server_name$request_uri;
}

server {
    listen 443 ssl http2;
    server_name example.com;

    ssl_certificate /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;

    location / {
        proxy_pass http://127.0.0.1:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

### Caddy 配置

Caddy 自动配置 HTTPS：

```
example.com {
    reverse_proxy localhost:3000
    encode gzip
    log {
        output file /var/log/caddy/access.log
    }
}
```

---

## 备份方案

数据保护的备份工具和策略。

### 备份工具

| 工具 | 类型 | 去重 | 加密 | 远程 |
|------|------|------|------|------|
| restic | 去重 | 是 | 是 | 是 |
| borgbackup | 去重 | 是 | 是 | 是 |
| duplicati | GUI/CLI | 是 | 是 | 是 |
| rclone | 云同步 | 否 | 是 | 是 |
| rsync | 文件同步 | 否 | 否 | 是 |
| tar + gpg | 归档 | 否 | 手动 | 手动 |

### 备份策略：3-2-1 法则

| 组件 | 描述 |
|------|------|
| 3 份副本 | 保持至少 3 份数据副本 |
| 2 种介质 | 存储在 2 种不同类型的介质上 |
| 1 份异地 | 保持 1 份异地副本（云或远程） |

### Restic 示例

```bash
# 初始化仓库
restic init --repo /backup/mydata

# 备份
restic backup /home/user/documents --repo /backup/mydata

# 列出快照
restic snapshots --repo /backup/mydata

# 恢复
restic restore latest --target /restore --repo /backup/mydata

# 清理旧备份
restic forget --keep-daily 7 --keep-weekly 4 --keep-monthly 6 --repo /backup/mydata --prune
```

---

## 云工具

管理云基础设施和服务的工具。

### 基础设施即代码

| 工具 | 类型 | 语言 | 最佳用途 |
|------|------|------|----------|
| Terraform | 配置 | HCL | 多云基础设施 |
| Pulumi | 配置 | 通用语言 | 编程式 IaC |
| CloudFormation | 配置 | YAML/JSON | 仅 AWS |
| Ansible | 配置管理 | YAML | 服务器配置 |
| Chef | 配置管理 | Ruby | 企业配置 |
| Puppet | 配置管理 | DSL | 企业配置 |

### 云提供商 CLI 工具

| 提供商 | CLI 工具 | 关键命令 |
|--------|----------|----------|
| AWS | aws-cli | `aws s3 ls`、`aws ec2 describe-instances` |
| Google Cloud | gcloud | `gcloud compute instances list` |
| Azure | az | `az vm list` |
| DigitalOcean | doctl | `doctl compute droplet list` |
| Hetzner | hcloud | `hcloud server list` |

### CI/CD 工具

| 工具 | 类型 | 核心功能 |
|------|------|----------|
| GitHub Actions | 云 | GitHub 集成 |
| GitLab CI | 云/自托管 | GitLab 集成 |
| Jenkins | 自托管 | 插件生态系统 |
| CircleCI | 云 | Docker 原生 |
| ArgoCD | GitOps | Kubernetes 部署 |
| Tekton | 云原生 | Kubernetes 原生流水线 |

---

## 总结

本工具和技术集合涵盖了系统管理员、DevOps 工程师和安全专业人员的核心知识。关键要点：

- **精通命令行**：CLI 工具是系统管理的基础
- **自动化一切**：Shell 脚本和 IaC 减少人为错误并节省时间
- **主动监控**：你看不到的东西就无法修复
- **坚持备份**：遵循 3-2-1 法则保护数据
- **安全第一**：从一开始就应用安全最佳实践，而不是事后补充
- **保持更新**：工具和最佳实践在演进；持续学习是必要的
