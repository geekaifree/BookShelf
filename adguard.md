# AdGuard Home: DNS 级广告拦截

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
