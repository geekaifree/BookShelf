# DNS 与广告拦截

> 本文档整合了以下源文件：dns.md, dns2.md, adguard.md

---

## 来源：dns.md

## 简介

Technitium DNS Server 是一款开源、跨平台的 DNS 服务器，可用作个人 DNS 服务器或中小型组织使用。它支持递归和权威 DNS 解析，提供基于 Web 的管理界面。

| 特性 | 描述 |
|---------|-------------|
| 递归解析 | 带缓存的完整递归 DNS 解析器 |
| 权威区域 | 托管您自己的 DNS 区域 |
| Web GUI | 基于浏览器的管理界面 |
| DNS over HTTPS | 通过 HTTPS 的安全 DNS 查询 |
| 拦截 | 内置广告拦截和域名过滤 |

## 架构

### DNS 概念

| 概念 | 描述 |
|---------|-------------|
| 递归解析器 | 通过查询权威服务器来解析 DNS 查询 |
| 权威服务器 | 为已配置区域提供权威答案 |
| 转发器 | 将查询转发到上游 DNS 服务器 |
| 缓存 | 存储已解析查询以加快响应速度 |
| 区域 | 由服务器管理的 DNS 命名空间的一部分 |

### 记录类型

| 记录 | 用途 | 示例 |
|--------|---------|---------|
| A | 将主机名映射到 IPv4 地址 | example.com -> 93.184.216.34 |
| AAAA | 将主机名映射到 IPv6 地址 | example.com -> 2606:2800:220:1:... |
| CNAME | 另一个主机名的别名 | www.example.com -> example.com |
| MX | 邮件交换服务器 | mail.example.com 优先级 10 |
| TXT | 文本记录（SPF、DKIM 等） | "v=spf1 include:example.com ~all" |
| NS | 名称服务器记录 | ns1.example.com |
| PTR | 反向 DNS 查找 | 34.216.184.93 -> example.com |
| SRV | 服务位置记录 | _sip._tcp.example.com |
| SOA | 区域的起始授权 | 区域元数据 |

## 安装

### 独立安装

```bash
# 从官方发布版本下载
# Windows：运行安装程序
# Linux：解压并运行

# 启动 DNS 服务器
sudo dotnet DnsServerApp.dll
```

### Docker 部署

```bash
docker run -d \
  --name=technitium-dns \
  -p 53:53/udp \
  -p 53:53/tcp \
  -p 5380:5380/tcp \
  -v ./config:/etc/dns/config \
  --restart unless-stopped \
  technitium/dns:latest
```

### Docker Compose

```yaml
version: "3.8"
services:
  dns:
    image: technitium/dns:latest
    container_name: technitium-dns
    ports:
      - "53:53/udp"
      - "53:53/tcp"
      - "5380:5380/tcp"
    volumes:
      - ./config:/etc/dns/config
    restart: unless-stopped
    cap_add:
      - NET_ADMIN
```

## 初始配置

### 首次设置

| 步骤 | 操作 |
|------|--------|
| 1 | 打开 Web 界面 http://server-ip:5380 |
| 2 | 使用默认凭证登录（admin/admin） |
| 3 | 立即更改管理员密码 |
| 4 | 配置网络接口 |
| 5 | 添加上游转发器 |
| 6 | 创建您的第一个区域 |

### 服务器设置

| 设置 | 描述 |
|---------|-------------|
| DNS 服务器端口 | DNS 默认 53，Web GUI 默认 5380 |
| 启用递归 | 允许客户端的递归解析 |
| 启用缓存 | 缓存已解析的查询 |
| 允许的网络 | 限制哪些客户端可以查询 |
| 转发器 | 未解析查询的上游 DNS 服务器 |

## 区域管理

### 创建区域

| 区域类型 | 描述 | 使用场景 |
|-----------|-------------|----------|
| 主区域 | 具有完全控制权的权威区域 | 您自己的域名 |
| 辅助区域 | 来自另一台服务器的主区域副本 | 冗余 |
| 转发器 | 转发特定区域的查询 | 分裂 DNS |
| 存根 | 最小区域信息 | 委派 |

### 区域记录

| 记录 | 字段 | 描述 |
|--------|--------|-------------|
| A | 名称、IP 地址、TTL | IPv4 地址映射 |
| AAAA | 名称、IPv6 地址、TTL | IPv6 地址映射 |
| CNAME | 名称、别名、TTL | 主机名别名 |
| MX | 名称、邮件服务器、优先级、TTL | 邮件服务器 |
| TXT | 名称、文本数据、TTL | 任意文本 |
| NS | 名称、名称服务器、TTL | 名称服务器委派 |
| PTR | IP 地址、主机名、TTL | 反向查找 |
| SRV | 名称、优先级、权重、端口、目标、TTL | 服务位置 |

### 区域文件示例

```
; example.com 的主区域
$ORIGIN example.com.
$TTL 3600

@       IN  SOA   ns1.example.com. admin.example.com. (
                   2024010101  ; 序列号
                   3600        ; 刷新
                   900         ; 重试
                   604800      ; 过期
                   86400       ; 最小 TTL
               )

@       IN  NS    ns1.example.com.
@       IN  NS    ns2.example.com.
@       IN  A     93.184.216.34
www     IN  A     93.184.216.34
mail    IN  A     93.184.216.35
@       IN  MX    10 mail.example.com.
@       IN  TXT   "v=spf1 mx ~all"
```

## 转发配置

### 转发器

| 转发器 | IP 地址 | 使用场景 |
|-----------|-----------|----------|
| Cloudflare | 1.1.1.1、1.0.0.1 | 注重隐私 |
| Google | 8.8.8.8、8.8.4.4 | 通用用途 |
| Quad9 | 9.9.9.9、149.112.112.112 | 注重安全 |
| OpenDNS | 208.67.222.222、208.67.220.220 | 过滤 |

### 条件转发

| 域名 | 转发到 | 使用场景 |
|--------|-----------|----------|
| internal.company.com | 10.0.0.1 | 内部 DNS |
| home.lan | 192.168.1.1 | 家庭网络 |
| vpn.example.com | 172.16.0.1 | VPN DNS |

## DNS over HTTPS (DoH)

### 配置

| 设置 | 描述 |
|---------|-------------|
| 启用 DoH | 激活 DNS over HTTPS 支持 |
| HTTPS 端口 | 默认 443 |
| TLS 证书 | 用于 HTTPS 的 SSL 证书 |
| HTTP 头 | CORS 和安全头 |

### DoH 客户端配置

| 客户端 | 配置 |
|--------|---------------|
| Firefox | 网络设置 > DNS over HTTPS > 自定义 |
| Chrome | chrome://flags/#dns-over-https |
| 系统 | 配置系统 DNS 使用 DoH 服务器 |

## 拦截和过滤

### 拦截列表

| 列表类型 | 描述 | 示例 |
|-----------|-------------|---------|
| 广告拦截 | 拦截广告域名 | AdGuard、Steven Black |
| 恶意软件 | 拦截已知恶意软件域名 | MalwareDomainList |
| 钓鱼 | 拦截钓鱼网站 | PhishTank |
| 自定义 | 用户定义的拦截列表 | 手动条目 |

### 拦截配置

| 设置 | 描述 |
|---------|-------------|
| 启用拦截 | 激活域名拦截 |
| 拦截列表 URL | 拦截列表文件的 URL |
| 拦截动作 | NXDOMAIN、0.0.0.0 或自定义 IP |
| 允许列表 | 拦截规则的例外 |
| 计划 | 基于时间的拦截规则 |

### 自定义拦截规则

```
# 拦截特定域名
ads.example.com
tracker.example.com

# 允许特定域名（例外）
important-service.example.com
```

## 访问控制

### 客户端 ACL

| 规则 | 描述 |
|------|-------------|
| 允许 | 允许来自指定网络的查询 |
| 拒绝 | 阻止来自指定网络的查询 |
| 仅递归 | 仅允许受信任客户端的递归查询 |

### 网络组

| 组 | 网络 | 权限 |
|-------|---------|-------------|
| LAN | 192.168.0.0/16 | 完全访问 |
| DMZ | 10.0.1.0/24 | 仅权威 |
| 访客 | 10.0.2.0/24 | 有限访问 |

## 日志和监控

### 查询日志

| 日志字段 | 描述 |
|-----------|-------------|
| 时间戳 | 查询时间 |
| 客户端 IP | 源 IP 地址 |
| 查询名称 | 被查询的域名 |
| 查询类型 | 请求的记录类型 |
| 响应 | 提供的答案 |
| 响应时间 | 解析所需时间 |

### 统计数据

| 指标 | 描述 |
|--------|-------------|
| 总查询数 | 处理的 DNS 查询数量 |
| 缓存命中率 | 从缓存提供服务的查询百分比 |
| 查询类型 | 按记录类型的分类 |
| 热门域名 | 最常查询的域名 |
| 被拦截查询 | 被拦截的请求数量 |

## DHCP 集成

### DHCP 设置

| 设置 | 描述 |
|---------|-------------|
| 启用 DHCP | 在 DNS 旁运行 DHCP 服务器 |
| IP 范围 | 要分配的 IP 地址范围 |
| 子网掩码 | 网络子网掩码 |
| 网关 | DHCP 客户端的默认网关 |
| DNS 服务器 | 提供给客户端的 DNS 服务器 |
| 租约时间 | IP 租约时长 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 用途 | 带 Web 管理的自托管 DNS 服务器 |
| 区域 | 支持主区域、辅助区域和转发器区域 |
| 记录 | 完全支持 A、AAAA、CNAME、MX、TXT 等 |
| 安全 | DNS over HTTPS、域名拦截和访问控制 |
| 过滤 | 内置广告拦截，可自定义拦截列表 |
| DHCP | 可选的 DHCP 服务器集成，实现自动配置 |


---

## 来源：dns2.md

## 简介

Pi-hole 是一个 DNS 陷阱，通过拦截 DNS 查询并阻止对已知广告和跟踪域名的请求来保护您的网络免受不需要的内容侵害。它在网络级别运行，覆盖所有设备，无需客户端软件。

## 目录

1. [Pi-hole 工作原理](#pi-hole-工作原理)
2. [系统要求](#系统要求)
3. [安装](#安装)
4. [网络配置](#网络配置)
5. [广告列表管理](#广告列表管理)
6. [白名单与黑名单](#白名单与黑名单)
7. [仪表盘与统计](#仪表盘与统计)
8. [上游 DNS](#上游-dns)
9. [高级配置](#高级配置)
10. [故障排除](#故障排除)

## Pi-hole 工作原理

### DNS 查询流程

| 步骤 | 过程 | 说明 |
|------|------|------|
| 1 | 设备请求域名 | 例如 ads.example.com |
| 2 | 查询发送到 Pi-hole | Pi-hole 充当 DNS 服务器 |
| 3 | 检查拦截列表 | 与已知广告域名比对 |
| 4 | 拦截或转发 | 已拦截的进入陷阱，允许的继续转发 |
| 5 | 返回响应 | IP 地址或 0.0.0.0 |

### 拦截方式

| 方式 | 响应 | 用户体验 |
|------|------|----------|
| 陷阱 | 0.0.0.0 | 广告位置显示空白 |
| 空阻止 | NXDOMAIN | 域名未找到 |
| 自定义 IP | 用户定义的 IP | 重定向到自定义页面 |

## 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| 设备 | Raspberry Pi Zero | Raspberry Pi 4 |
| 内存 | 512 MB | 1 GB+ |
| 存储 | 2 GB SD 卡 | 16 GB+ |
| 操作系统 | 基于 Debian 的 Linux | Raspberry Pi OS |
| 网络 | 可用静态 IP | 专用设备 |
| 依赖 | curl, git | 预装 |

## 安装

### 自动安装

```bash
# 一键安装
curl -sSL https://install.pi-hole.net | bash
```

### 安装步骤

| 步骤 | 选择 | 说明 |
|------|------|------|
| 1 | 上游 DNS | 选择 DNS 提供商 |
| 2 | 拦截列表 | 默认广告列表 |
| 3 | 管理界面 | 安装 Web UI |
| 4 | Web 服务器 | 安装 lighttpd |
| 5 | 查询日志 | 启用日志记录 |
| 6 | 隐私模式 | 设置数据可见性 |

### Docker 安装

```yaml
# docker-compose.yml
services:
  pihole:
    image: pihole/pihole:latest
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "80:80/tcp"
    environment:
      TZ: America/New_York
      WEBPASSWORD: your-secure-password
    volumes:
      - ./etc-pihole:/etc/pihole
      - ./etc-dnsmasq.d:/etc/dnsmasq.d
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
```

### 安装后操作

| 任务 | 命令 |
|------|------|
| 设置管理员密码 | `pihole -a -p` |
| 更改 DNS | `pihole -a`（传送菜单） |
| 更新 Pi-hole | `pihole -up` |
| 检查状态 | `pihole status` |

## 网络配置

### 路由器 DNS 设置

| 步骤 | 操作 |
|------|------|
| 1 | 访问路由器管理面板 |
| 2 | 导航到 DHCP/DNS 设置 |
| 3 | 将主 DNS 设置为 Pi-hole IP |
| 4 | 将备用 DNS 设置为 Pi-hole IP 或 0.0.0.0 |
| 5 | 保存并重启路由器 |

### DHCP 模式对比

| 模式 | 说明 | 优点 | 缺点 |
|------|------|------|------|
| 路由器 DHCP | 路由器指向 Pi-hole | 设置简单 | 控制有限 |
| Pi-hole DHCP | Pi-hole 处理 DHCP | 完全控制 | 需要关闭路由器 DHCP |
| 静态 IP | 每设备手动 DNS | 设备特定 | 手动工作量大 |

### 网络拓扑

| 组件 | IP 地址 | 角色 |
|------|---------|------|
| 路由器 | 192.168.1.1 | 网关、DHCP |
| Pi-hole | 192.168.1.2 | DNS 陷阱 |
| 客户端设备 | 192.168.1.x | 使用 Pi-hole DNS |

## 广告列表管理

### 默认列表

| 列表 | URL | 用途 |
|------|-----|------|
| StevenBlack | https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts | 主拦截列表 |
| MalwareDomainList | http://www.malwaredomainlist.com/hostslist/hosts.txt | 恶意软件域名 |
| Cameleon | http://sysctl.org/cameleon/hosts | 广告跟踪 |

### 添加自定义列表

| 步骤 | 操作 |
|------|------|
| 1 | 进入 Pi-hole 管理 > 广告列表 |
| 2 | 在文本框中粘贴列表 URL |
| 3 | 点击"添加" |
| 4 | 点击"更新重力"以应用 |

### 热门附加列表

| 列表 | 重点 | URL |
|------|------|-----|
| OISD | 综合 | https://big.oisd.nl |
| 1Hosts | 平衡 | https://badmojr.github.io/1Hosts/Lite/hosts.txt |
| Energized | 多用途 | https://block.energized.pro/ultimate/formats/hosts.txt |
| Hagezi | 专业级 | https://cdn.jsdelivr.net/gh/hagezi/dns-blocklists@latest/hosts/pro.txt |

### 重力更新

| 命令 | 用途 |
|------|------|
| `pihole -g` | 更新重力（拦截列表） |
| `pihole -g -f` | 强制完整更新 |
| 定时任务 | 每周自动更新 |

## 白名单与黑名单

### 白名单管理

| 方式 | 命令/操作 |
|------|-----------|
| CLI | `pihole -w example.com` |
| Web UI | 设置 > 白名单 |
| 通配符 | `pihole -w *.example.com` |
| 移除 | `pihole -w -d example.com` |

### 黑名单管理

| 方式 | 命令/操作 |
|------|-----------|
| CLI | `pihole -b example.com` |
| Web UI | 设置 > 黑名单 |
| 通配符 | `pihole -b *.ads.example.com` |
| 移除 | `pihole -b -d example.com` |

### 常见白名单条目

| 域名 | 原因 |
|------|------|
| `apple.com` | iOS/Mac 更新 |
| `microsoft.com` | Windows 更新 |
| `googleapis.com` | Google 服务 |
| `github.com` | 开发者工具 |
| `cdn.jsdelivr.net` | 许多网站的 CDN |

## 仪表盘与统计

### 仪表盘指标

| 指标 | 说明 |
|------|------|
| 总查询数 | 已处理的 DNS 请求 |
| 已阻止查询 | Pi-hole 阻止的请求 |
| 阻止百分比 | 拦截率 |
| 列表中的域名 | 总拦截域名数 |
| 唯一客户端 | 使用 Pi-hole 的设备 |

### 查询类型

| 类型 | 说明 |
|------|------|
| A | IPv4 地址查询 |
| AAAA | IPv6 地址查询 |
| PTR | 反向 DNS 查询 |
| CNAME | 规范名称 |
| TXT | 文本记录 |
| SRV | 服务记录 |

### 查询状态

| 状态 | 含义 |
|------|------|
| Blocked | 域名在拦截列表中 |
| Forwarded | 已发送到上游 DNS |
| Cached | 从缓存应答 |
| Pi-holed | 被 Pi-hole 拦截 |

## 上游 DNS

### DNS 提供商对比

| 提供商 | 主 DNS | 备用 DNS | 特点 |
|--------|--------|----------|------|
| Google | 8.8.8.8 | 8.8.4.4 | 快速、可靠 |
| Cloudflare | 1.1.1.1 | 1.0.0.1 | 注重隐私 |
| Quad9 | 9.9.9.9 | 149.112.112.112 | 注重安全 |
| OpenDNS | 208.67.222.222 | 208.67.220.220 | 过滤选项 |
| NextDNS | 自定义 | 自定义 | 可定制 |

### DNS over HTTPS

| 配置 | 设置 |
|------|------|
| 启用 | 设置 > DNS > 使用 DNSSEC |
| 上游 | https://dns.cloudflare.com/dns-query |
| 引导 | 1.1.1.1, 1.0.0.1 |

## 高级配置

### 条件转发

| 设置 | 值 | 用途 |
|------|----|------|
| 本地网络 | 192.168.1.0/24 | 网络范围 |
| 路由器 IP | 192.168.1.1 | 网关地址 |
| 本地域名 | home.arpa | 域名后缀 |

### 速率限制

| 设置 | 默认值 | 说明 |
|------|--------|------|
| 速率限制 | 1000 查询/分钟 | 每客户端限制 |
| 突发大小 | 100 | 允许的突发查询数 |

### 缓存

| 设置 | 默认值 | 影响 |
|------|--------|------|
| 缓存大小 | 10000 条 | 内存使用 |
| 缓存 TTL | 遵循 DNS TTL | 新鲜度 |
| 本地 TTL | 2 秒 | 本地缓存时间 |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 无网络 | DNS 配置错误 | 检查路由器 DNS 设置 |
| 浏览缓慢 | 上游 DNS 慢 | 更换 DNS 提供商 |
| 网站异常 | 过度拦截 | 将域名加入白名单 |
| 未拦截 | 客户端绕过 | 检查 DHCP DNS 设置 |
| CPU 过高 | 查询过多 | 检查是否有循环 |

### 诊断命令

| 命令 | 用途 |
|------|------|
| `pihole status` | 检查 Pi-hole 运行状态 |
| `pihole -t` | 实时查询跟踪 |
| `pihole -q domain.com` | 搜索拦截列表 |
| `pihole -d` | 生成调试日志 |
| `pihole restartdns` | 重启 DNS 服务 |

### 调试日志

| 部分 | 信息 |
|------|------|
| 系统 | 操作系统、硬件、版本 |
| 网络 | 接口、DNS 配置 |
| Pi-hole | 配置、列表 |
| 进程 | 运行中的服务 |
| 数据库 | 查询日志、完整性 |

## 总结

Pi-hole 通过充当所有连接设备的 DNS 陷阱来提供全网络广告拦截。其 Web 仪表盘、广泛的拦截列表支持和最低的资源需求，使其成为在不需要客户端软件的情况下减少整个网络不需要内容的有效解决方案。


---

## 来源：adguard.md

## 简介

AdGuard Home 是一款网络级广告拦截器和隐私保护工具，工作在 DNS 层面。通过在网络中运行 AdGuard Home，你可以为连接到网络的每台设备拦截广告、追踪器和恶意域名，而无需在单个设备上安装软件。

AdGuard Home 充当 DNS 服务器，拦截域名请求并拦截与广告、追踪或恶意软件相关的域名。

## 为什么使用 DNS 级广告拦截？

| 方式 | 设备级拦截器 | DNS 级拦截器 |
|------|-----------|------------|
| 安装 | 每台设备 | 仅网络 |
| 覆盖 | 单设备 | 所有设备 |
| 性能 | 使用设备资源 | 最小开销 |
| 绕过 | 容易禁用 | 更难绕过 |
| IoT 支持 | 否 | 是 |
| 维护 | 每台设备 | 集中管理 |

## 工作原理

当网络中的设备尝试访问网站时，它首先请求 DNS 服务器将域名转换为 IP 地址。AdGuard Home 拦截此请求并根据其拦截列表检查该域名。

| 步骤 | 正常 DNS | 使用 AdGuard Home |
|------|---------|------------------|
| 1 | 设备请求域名 | 设备请求域名 |
| 2 | DNS 解析为 IP | AdGuard 检查拦截列表 |
| 3 | 设备连接到 IP | 如果拦截：返回 0.0.0.0 |
| 4 | 网站加载 | 如果允许：正常解析 |

## 安装

### Docker 部署

```bash
# 创建目录
mkdir -p /opt/adguardhome/work
mkdir -p /opt/adguardhome/conf

# 运行 AdGuard Home
docker run -d \
  --name adguardhome \
  --restart unless-stopped \
  -v /opt/adguardhome/work:/opt/adguardhome/work \
  -v /opt/adguardhome/conf:/opt/adguardhome/conf \
  -p 53:53/tcp \
  -p 53:53/udp \
  -p 3000:3000/tcp \
  -p 80:80/tcp \
  -p 443:443/tcp \
  adguard/adguardhome
```

### Docker Compose

```yaml
version: '3'
services:
  adguardhome:
    image: adguard/adguardhome
    container_name: adguardhome
    restart: unless-stopped
    ports:
      - "53:53/tcp"
      - "53:53/udp"
      - "3000:3000/tcp"
      - "80:80/tcp"
      - "443:443/tcp"
    volumes:
      - ./work:/opt/adguardhome/work
      - ./conf:/opt/adguardhome/conf
```

### 直接安装

```bash
# Linux/macOS
curl -s -S -L https://raw.githubusercontent.com/AdguardTeam/AdGuardHome/master/scripts/install.sh | sh
```

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| 内存 | 128MB | 512MB |
| 存储 | 50MB | 500MB |
| CPU | 1 核 | 2 核 |
| 网络 | 端口 53 | 端口 53、80、443、3000 |

## 初始设置

### 访问仪表板

安装后，通过 `http://your-server-ip:3000` 访问 Web 界面。

| 步骤 | 操作 |
|------|------|
| 1 | 打开浏览器访问端口 3000 |
| 2 | 创建管理员账户 |
| 3 | 配置 DNS 设置 |
| 4 | 添加拦截列表 |
| 5 | 配置 DHCP（可选） |

### DNS 配置

| 设置 | 描述 | 推荐值 |
|------|------|-------|
| 上游 DNS | 转发查询的目标 | 1.1.1.1, 8.8.8.8 |
| 引导 DNS | 解析上游 DNS | 1.1.1.1, 8.8.8.8 |
| 监听端口 | DNS 服务器端口 | 53 |
| 速率限制 | 每秒查询数 | 20 |

## 拦截列表

拦截列表是广告拦截的核心。它们包含与广告、追踪器和恶意软件相关的域名。

### 推荐拦截列表

| 列表 | 类型 | 大小 | 描述 |
|------|------|------|------|
| AdGuard DNS | 广告 | 内置 | AdGuard 自有列表 |
| Steven Black | 统一 | 大 | 合并 hosts 文件 |
| OISD | 广告 | 大 | 综合荷兰列表 |
| EasyList | 广告 | 大 | 最流行的过滤器 |
| EasyPrivacy | 隐私 | 大 | 追踪器拦截 |
| Peter Lowe | 广告 | 中 | 紧凑高效 |
| MalwareDomainList | 安全 | 中 | 恶意软件域名 |
| Phishing Army | 安全 | 中 | 钓鱼网站 |

### 添加自定义拦截列表

1. 转到 过滤器 > DNS 拦截列表
2. 点击"添加拦截列表"
3. 输入拦截列表 URL
4. 点击"保存"

| 拦截列表 URL | 类型 | 更新频率 |
|-------------|------|---------|
| https://adguardteam.github.io/HostlistsRegistry/assets/filter_1.txt | 广告 | 每日 |
| https://big.oisd.nl | 统一 | 每日 |
| https://easylist.to/easylist/easylist.txt | 广告 | 每周 |
| https://easylist.to/easylist/easyprivacy.txt | 隐私 | 每周 |

## DNS 重写

DNS 重写允许你将特定域名重定向到自定义 IP 地址。

| 使用场景 | 域名 | 目标 IP | 描述 |
|---------|------|--------|------|
| 本地服务器 | myapp.local | 192.168.1.100 | 开发服务器 |
| 广告拦截 | ads.example.com | 0.0.0.0 | 拦截域名 |
| Pi-hole 重定向 | pi.hole | 192.168.1.1 | 仪表板访问 |
| 自托管 | nextcloud.home | 192.168.1.50 | Nextcloud 访问 |

### 添加 DNS 重写

1. 转到 过滤器 > DNS 重写
2. 点击"添加 DNS 重写"
3. 输入域名和目标 IP
4. 点击"保存"

## 客户端配置

### 路由器级设置

配置路由器将 AdGuard Home 用作所有网络设备的 DNS 服务器。

| 路由器设置 | 值 |
|-----------|---|
| 主 DNS | AdGuard Home IP |
| 备用 DNS | 1.1.1.1（备用） |
| DHCP DNS | AdGuard Home IP |

### 单设备设置

| 设备 | 配置路径 |
|------|---------|
| Windows | 设置 > 网络 > DNS |
| macOS | 系统偏好设置 > 网络 > DNS |
| iOS | 设置 > Wi-Fi > DNS |
| Android | 设置 > 网络 > 私有 DNS |
| Linux | /etc/resolv.conf |

## 过滤规则

自定义规则允许对拦截内容进行细粒度控制。

### 规则语法

| 规则 | 描述 |
|------|------|
| `\|\|example.com^` | 拦截 example.com 及其子域名 |
| `@@\|\|example.com^` | 允许 example.com（白名单） |
| `\|\|example.com^$important` | 强制拦截（覆盖允许列表） |
| `example.com^$dnsrewrite=NOERROR;A;192.168.1.1` | 重写 DNS |

### 常用自定义规则

| 用途 | 规则 |
|------|------|
| 拦截特定域名 | `\|\|tracking.example.com^` |
| 允许特定域名 | `@@\|\|analytics.example.com^` |
| 按模式拦截 | `\|\|*.ads.*.com^` |
| 允许子域名 | `@@\|\|sub.example.com^` |

## 查询日志

查询日志显示所有 DNS 请求及其状态。

| 状态 | 含义 | 颜色 |
|------|------|------|
| 已允许 | 域名通过 | 绿色 |
| 已拦截 | 域名被过滤器拦截 | 红色 |
| 已重写 | 自定义 DNS 响应 | 蓝色 |
| 已过滤 | 被自定义规则拦截 | 橙色 |

### 日志分析

| 指标 | 用途 |
|------|------|
| 总查询数 | 网络活动水平 |
| 拦截百分比 | 过滤器效果 |
| 热门域名 | 最常访问的网站 |
| 热门拦截 | 最常见的追踪器 |

## DHCP 服务器

AdGuard Home 可以选择性地充当网络的 DHCP 服务器。

| 功能 | 描述 |
|------|------|
| IP 分配 | 自动 IP 分配 |
| DNS 分发 | 将 AdGuard DNS 推送到所有客户端 |
| 租约管理 | 追踪连接设备 |
| 静态租约 | 按 MAC 分配固定 IP |

### DHCP 配置

| 设置 | 值 |
|------|---|
| 网关 IP | 你的路由器 IP |
| 子网掩码 | 255.255.255.0 |
| 范围起始 | 192.168.1.100 |
| 范围结束 | 192.168.1.254 |
| 租约时间 | 24 小时 |

## 性能调优

| 设置 | 描述 | 建议 |
|------|------|------|
| 缓存大小 | DNS 响应缓存 | 4000+ 条目 |
| 缓存 TTL | 生存时间覆盖 | 禁用（使用上游） |
| 速率限制 | 每客户端查询数 | 20/秒 |
| 拒绝 ANY | 拦截 ANY 请求 | 启用 |
| EDNS | 扩展 DNS | 启用 |

## 安全功能

| 功能 | 描述 | 配置 |
|------|------|------|
| HTTPS | 加密 Web 界面 | SSL 证书 |
| DNS-over-HTTPS | 加密 DNS 查询 | 内置支持 |
| DNS-over-TLS | 加密 DNS (TLS) | 内置支持 |
| DNSSEC | DNS 认证 | 在设置中启用 |
| 访问控制 | 客户端白名单 | 按客户端规则 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| DNS 无法解析 | 端口 53 冲突 | 停止其他 DNS 服务 |
| 查询缓慢 | 无缓存 | 增加缓存大小 |
| 广告未拦截 | 缺少拦截列表 | 添加更多列表 |
| 网站异常 | 过度拦截 | 检查查询日志，添加白名单 |
| 无网络 | 上游 DNS 错误 | 验证上游 DNS 设置 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | adguard.com/adguard-home |
| GitHub | github.com/AdguardTeam/AdGuardHome |
| 文档 | github.com/AdguardTeam/AdGuardHome/wiki |
| 过滤列表 | filterlists.com |


---
