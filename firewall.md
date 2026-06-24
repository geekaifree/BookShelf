# Firezone 教程：VPN 和防火墙网关

## 简介

Firezone 是一个基于 WireGuard 构建的开源 VPN 网关和防火墙。它提供安全的远程访问，支持基于身份的策略、分流隧道以及与流行身份提供商的集成，实现零信任网络访问。

## 架构

| 组件 | 用途 |
|------|------|
| Gateway（网关） | 处理 WireGuard 隧道的 VPN 服务器 |
| Control Plane（控制平面） | API 和 Web 管理界面 |
| Relay（中继） | 用于 NAT 穿越的 STUN/TURN 服务器 |
| 客户端应用 | 所有平台的原生应用 |
| 数据库 | 用于配置存储的 PostgreSQL |

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| CPU | 2 核 | 4 核 |
| 内存 | 2 GB | 4 GB |
| 操作系统 | Linux x86_64 | Ubuntu 22.04 或更新 |
| 端口 | UDP 51820 | UDP 51820, TCP 443 |
| 网络 | 公网 IP 地址 | 带 DNS 的公网 IP |

## 安装

### Docker Compose

```yaml
version: '3.8'
services:
  firezone:
    image: firezone/firezone:latest
    ports:
      - "443:443"
      - "51820:51820/udp"
    env_file:
      - .env
    volumes:
      - ./firezone-data:/var/firezone
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.ip_forward=1
      - net.ipv6.conf.all.forwarding=1
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15
    volumes:
      - pg-data:/var/lib/postgresql/data
    environment:
      POSTGRES_DB: firezone
      POSTGRES_USER: firezone
      POSTGRES_PASSWORD: changeme
    restart: unless-stopped

volumes:
  pg-data:
```

### 环境配置

```bash
# .env
EXTERNAL_URL=https://vpn.example.com
DEFAULT_ADMIN_EMAIL=admin@example.com
DEFAULT_ADMIN_PASSWORD=securepassword
DATABASE_URL=postgres://firezone:changeme@db/firezone
SECRET_KEY_BASE=generate-a-long-random-string-here
WIREGUARD_PORT=51820
WIREGUARD_IPV4_ADDRESS=10.3.2.1
WIREGUARD_IPV6_ADDRESS=fd00::3:2:1
```

## 核心概念

| 概念 | 说明 |
|------|------|
| Site（站点） | 包含网关的网络位置 |
| Resource（资源） | 受保护的端点（CIDR、DNS 名称或 IP） |
| Policy（策略） | 将组链接到资源的访问规则 |
| Group（组） | 具有共享访问权限的用户集合 |
| Gateway（网关） | 站点内的 VPN 服务器实例 |
| Client（客户端） | 通过 VPN 连接的用户设备 |

## 网关管理

### 网关部署类型

| 类型 | 部署方式 | 用途 |
|------|---------|------|
| Docker | 服务器上的容器 | Linux 服务器环境 |
| Systemd | 原生二进制服务 | 裸机 Linux 安装 |
| Gateway Group（网关组） | 多个网关 | 高可用配置 |

### 网关配置设置

| 设置 | 说明 | 默认值 |
|------|------|--------|
| Listen Port | WireGuard UDP 端口 | 51820 |
| DNS Servers | 推送到客户端的 DNS | Cloudflare 1.1.1.1 |
| MTU | 最大传输单元 | 1280 |
| Persistent Keepalive | NAT 保活间隔 | 25 秒 |

## 资源配置

### 资源类型

| 类型 | 示例 | 用途 |
|------|------|------|
| CIDR | 10.0.0.0/24 | 子网访问 |
| IP 地址 | 192.168.1.100 | 单主机访问 |
| DNS 名称 | internal.example.com | 基于域名的访问 |

### 创建资源

| 字段 | 说明 | 示例 |
|------|------|------|
| 名称 | 资源显示名称 | "Internal Network" |
| 地址 | CIDR、IP 或 DNS | 10.0.0.0/24 |
| 站点 | 关联站点 | "Main Office" |
| 流量过滤器 | 允许的端口和协议 | TCP 80, 443 |

## 策略管理

### 策略结构

| 组件 | 说明 |
|------|------|
| Group（组） | 谁获得访问权限 |
| Resource（资源） | 他们可以访问什么 |
| Action（操作） | 允许或拒绝 |

### 策略示例

| 组 | 资源 | 操作 | 用途 |
|----|------|------|------|
| Engineers | Dev Servers | 允许 | 开发访问 |
| All Staff | Intranet | 允许 | 内部 Wiki 访问 |
| Contractors | Production DB | 拒绝 | 限制敏感访问 |
| Admins | All Resources | 允许 | 完全管理访问 |

## 身份提供商集成

### 支持的提供商

| 提供商 | 协议 | 功能 |
|--------|------|------|
| Google Workspace | OIDC | 组同步 |
| Microsoft Entra | OIDC / SAML | 条件访问策略 |
| Okta | OIDC / SAML | MFA 支持 |
| Keycloak | OIDC / SAML | 自托管 IdP |
| Auth0 | OIDC | 自定义认证规则 |
| JumpCloud | OIDC / SAML | 目录同步 |
| Local | 邮箱和密码 | 无需外部 IdP |

### OIDC 配置字段

| 字段 | 说明 | 示例 |
|------|------|------|
| Client ID | OAuth 客户端标识 | `firezone-client` |
| Client Secret | OAuth 客户端密钥 | `secret-value` |
| Discovery URL | OIDC well-known URL | `https://accounts.google.com/.well-known/openid-configuration` |
| Redirect URI | 回调 URL | `https://vpn.example.com/auth/oidc/callback` |

## 客户端应用

### 支持的平台

| 平台 | 分发方式 | 主要功能 |
|------|---------|---------|
| macOS | App Store | 原生应用，自动连接 |
| Windows | Microsoft Store | 系统托盘集成 |
| Linux | 包管理器 | CLI 和 GUI 可用 |
| iOS | App Store | 始终在线 VPN 模式 |
| Android | Play Store / F-Droid | 按应用 VPN 路由 |
| Headless | CLI 二进制 | 服务器和脚本使用 |

### 客户端配置选项

| 设置 | 说明 | 默认值 |
|------|------|--------|
| 自动连接 | 应用启动时连接 | 关 |
| 按需连接 | 自动重连 | 开 |
| DNS 覆盖 | 自定义 DNS 服务器 | 使用网关 DNS |
| 分流隧道 | 仅路由资源流量 | 启用 |

## 分流隧道（Split Tunneling）

| 模式 | 说明 | 用途 |
|------|------|------|
| 全隧道 | 所有流量通过 VPN | 最大安全性 |
| 分流隧道 | 仅资源流量通过 VPN | 家庭和办公使用 |
| 排除应用 | 按应用选择隧道 | 移动设备 |

### 分流隧道优势

| 优势 | 说明 |
|------|------|
| 节省带宽 | 仅 VPN 相关流量使用隧道 |
| 速度 | 保留直接互联网访问 |
| 兼容性 | 保持本地网络访问 |
| 隐私 | 资源访问已加密和安全 |

## 高可用

### 多网关架构

| 组件 | 用途 |
|------|------|
| 主网关 | 处理活跃流量 |
| 备用网关 | 故障转移备用 |
| 负载均衡器 | 分配连接 |
| 健康检查 | 监控网关可用性 |

### 故障转移指标

| 指标 | 阈值 | 操作 |
|------|------|------|
| 健康检查失败 | 连续 3 次 | 标记网关不健康 |
| 故障转移时间 | 30 秒以内 | 切换到备用网关 |
| 客户端重连 | 自动 | 客户端自动重连 |

## 网络配置

### 防火墙规则

| 规则 | 来源 | 目标 | 端口 | 操作 |
|------|------|------|------|------|
| 允许 VPN | 任意 | 网关 | 51820/UDP | 接受 |
| 允许 HTTPS | 任意 | 网关 | 443/TCP | 接受 |
| 转发 VPN | VPN CIDR | 资源 | 任意 | 接受 |
| 丢弃其他 | 任意 | 任意 | 任意 | 丢弃 |

### NAT 穿越场景

| 场景 | 解决方案 |
|------|---------|
| 客户端在 NAT 后 | WireGuard 自动处理 NAT |
| 网关在 NAT 后 | 需要在路由器上设置端口转发 |
| 对称 NAT | 需要中继服务器穿越 |

## 监控

### 仪表板指标

| 指标 | 说明 |
|------|------|
| 活跃连接 | 当前连接的 VPN 用户数 |
| 数据传输 | 传入和传出的字节数 |
| 网关健康 | 每个网关的在线/离线状态 |
| 用户活动 | 连接历史和持续时间 |

### 查看日志

```bash
# 网关日志
docker logs firezone-gateway -f

# 控制平面日志
docker logs firezone -f

# 最近的连接流
docker exec firezone-db psql -U firezone \
  -c "SELECT * FROM flows ORDER BY created_at DESC LIMIT 10;"
```

## API 访问

### REST API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/v1/users` | GET / POST | 用户管理 |
| `/api/v1/groups` | GET / POST | 组管理 |
| `/api/v1/resources` | GET / POST | 资源管理 |
| `/api/v1/policies` | GET / POST | 策略管理 |
| `/api/v1/gateways` | GET / POST | 网关管理 |
| `/api/v1/sites` | GET / POST | 站点管理 |

### API 认证

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" \
  https://vpn.example.com/api/v1/users
```

## 安全功能

| 功能 | 说明 |
|------|------|
| WireGuard 协议 | 现代高性能 VPN |
| 零信任模型 | 基于身份的访问控制 |
| MFA 支持 | 多因素认证 |
| 加密 | ChaCha20-Poly1305 密码 |
| 密钥轮换 | 自动 WireGuard 密钥刷新 |
| 审计日志 | 完整的访问审计追踪 |

## 备份

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | pg_dump | 每日 |
| 配置 | .env 文件备份 | 更改时 |
| WireGuard 密钥 | 安全存储 | 生成时 |
| SSL 证书 | 证书备份 | 续期时 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法连接 | 防火墙阻止 UDP | 在防火墙中打开端口 51820 |
| VPN 无互联网 | DNS 配置问题 | 检查网关中的 DNS 设置 |
| VPN 速度慢 | MTU 不匹配 | 将 MTU 降低到 1280 |
| 认证失败 | IdP 配置错误 | 验证 OIDC 设置 |
| 网关离线 | 服务未运行 | 重启网关容器 |

## 总结

Firezone 提供了一个基于 WireGuard 构建的现代 VPN 解决方案，具有基于身份的访问控制。其与身份提供商的集成、分流隧道能力以及多平台客户端支持，使其适合寻求零信任网络访问的各种规模组织。
