# 使用 Pi-hole 进行 DNS 广告拦截

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
