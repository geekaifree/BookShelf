# 安全与隐私

> 本文档整合了以下源文件：privacy.md, privacy2.md, survival.md, sentinel.md, security.md, firewall.md, vpn.md

---

## 来源：privacy.md

## 目录

1. [理解 VPN 技术](#understanding-vpn)
2. [Mullvad VPN 概述](#mullvad-overview)
3. [安装与设置](#installation)
4. [配置选项](#configuration)
5. [高级功能](#advanced-features)
6. [隐私最佳实践](#privacy-best-practices)
7. [故障排除](#troubleshooting)
8. [安全考虑](#security-considerations)

---

## 理解 VPN

虚拟专用网络（VPN）在你的设备和远程服务器之间创建加密隧道，隐藏你的 IP 地址并保护你的在线活动免受监控。

### VPN 工作原理

| 组件 | 功能 | 隐私益处 |
|------|------|----------|
| 加密 | 混淆数据 | 防止窃听 |
| IP 隐藏 | 隐藏真实 IP 地址 | 匿名浏览 |
| 隧道 | 安全数据通道 | 在公共 WiFi 上保护数据 |
| 断路器 | VPN 断开时阻止流量 | 防止数据泄露 |

### VPN 协议对比

| 协议 | 速度 | 安全性 | 用途 |
|------|------|--------|------|
| WireGuard | 快 | 现代 | 默认选择 |
| OpenVPN | 中等 | 成熟 | 传统支持 |
| IKEv2 | 快 | 强 | 移动设备 |

### 威胁模型

| 威胁 | 保护级别 | VPN 有效性 |
|------|----------|------------|
| ISP 监控 | 高 | 向 ISP 隐藏浏览记录 |
| 公共 WiFi 攻击 | 高 | 加密所有流量 |
| 政府监控 | 中等 | 隐藏 IP，不能隐藏使用模式 |
| 定向攻击 | 低 | VPN 只是一层保护 |

---

## Mullvad VPN 概述

Mullvad 是一家总部位于瑞典的隐私优先 VPN 服务，以其对用户隐私的坚定承诺和最少数据收集而闻名。

### Mullvad 核心功能

| 功能 | 描述 | 隐私益处 |
|------|------|----------|
| 无日志策略 | 不追踪活动 | 无数据可分享 |
| 账号号码 | 无需邮箱 | 匿名注册 |
| 现金支付 | 邮寄选项 | 不可追踪的支付 |
| 开源 | 可审计代码 | 透明度 |
| WireGuard | 现代协议 | 速度与安全 |

### Mullvad vs 其他 VPN

| 功能 | Mullvad | 典型 VPN |
|------|---------|----------|
| 注册要求 | 仅需账号号码 | 邮箱、姓名 |
| 日志记录 | 无 | 不定 |
| 支付方式 | 现金、加密货币、银行卡 | 仅银行卡 |
| 价格 | 固定 5 欧元/月 | 不定 |
| 审计 | 定期 | 罕见 |

### 服务器网络

| 地区 | 服务器数量 | 用途 |
|------|------------|------|
| 欧洲 | 300+ | 主要覆盖 |
| 北美 | 100+ | 快速连接 |
| 亚太 | 50+ | 区域访问 |
| 南美 | 20+ | 本地连接 |

---

## 安装与设置

在所有主要平台上安装 Mullvad VPN 都很简单。

### 系统要求

| 平台 | 最低版本 | 内存 | 磁盘空间 |
|------|----------|------|----------|
| Windows | 10 或更高 | 2GB | 100MB |
| macOS | 11 或更高 | 2GB | 100MB |
| Linux | Ubuntu 20.04+ | 2GB | 100MB |
| Android | 8.0 或更高 | 1GB | 50MB |
| iOS | 15.0 或更高 | 1GB | 50MB |

### 安装步骤

| 步骤 | 操作 | 命令/位置 |
|------|------|-----------|
| 1 | 下载应用 | mullvad.net/download |
| 2 | 安装应用程序 | 运行安装程序 |
| 3 | 创建账号 | 生成账号号码 |
| 4 | 添加时长 | 支付页面 |
| 5 | 连接 | 选择服务器，点击连接 |

### 账号设置

```
Account Number Format: XXXX XXXX XXXX XXXX

Payment Options:
- Credit Card
- Bitcoin
- Cash (mail to Sweden)
- Bank Wire
- Swish (Sweden only)
```

---

## 配置选项

正确的配置可以针对你的特定需求优化安全性和性能。

### 连接设置

| 设置 | 选项 | 推荐 |
|------|------|------|
| 协议 | WireGuard, OpenVPN | WireGuard |
| 端口 | 自动、自定义 | 自动 |
| DNS | 默认、自定义 | Mullvad DNS |
| 断路器 | 开/关 | 始终开启 |
| 自动连接 | 开/关 | 开启 |

### DNS 配置

| DNS 提供商 | 隐私性 | 速度 | 内容过滤 |
|------------|--------|------|----------|
| Mullvad 默认 | 高 | 快 | 无 |
| Mullvad 过滤 | 高 | 快 | 广告/追踪器 |
| 自定义 | 不定 | 不定 | 不定 |

### 分流隧道

| 应用 | 使用 VPN | 原因 |
|------|----------|------|
| 网页浏览器 | 是 | 隐私关键 |
| 银行应用 | 否 | 可能阻止 VPN |
| 游戏 | 可选 | 对延迟敏感 |
| 流媒体 | 可选 | 内容访问 |

### 高级网络设置

| 设置 | 描述 | 何时使用 |
|------|------|----------|
| IPv6 | 启用/禁用 IPv6 | 兼容性 |
| 本地网络 | 访问局域网设备 | 家庭网络 |
| 混淆 | 隐藏 VPN 流量 | 受限网络 |
| 桥接模式 | 双重 VPN | 最大隐私 |

---

## 高级功能

Mullvad 为需要增强隐私和控制的用户提供高级功能。

### 多跳（双重 VPN）

| 配置 | 路径 | 用途 |
|------|------|------|
| 入口 → 出口 | 国家 A → 国家 B | 增强隐私 |
| 同一国家 | 城市 A → 城市 B | 区域隐私 |
| 不同国家 | 任意组合 | 最大匿名性 |

### Shadowsocks 混淆

| 功能 | 描述 | 好处 |
|------|------|------|
| 协议 | SOCKS5 代理 | 绕过 VPN 封锁 |
| 加密 | 额外层 | 隐藏 VPN 使用 |
| 用途 | 审查网络 | 访问被封锁的内容 |

### 自定义 DNS 服务器

| 服务器 | IP 地址 | 用途 |
|--------|---------|------|
| Cloudflare | 1.1.1.1 | 速度 |
| Google | 8.8.8.8 | 可靠性 |
| Quad9 | 9.9.9.9 | 安全性 |
| AdGuard | 94.140.14.14 | 广告拦截 |

### CLI 命令

```bash
# Connect to specific country
mullvad relay set location se

# Enable kill switch
mullvad lockdown-mode set on

# Check connection status
mullvad status

# Set DNS
mullvad dns set default
```

---

## 隐私最佳实践

将 VPN 与其他隐私措施结合可以创建全面的安全防护。

### 隐私清单

| 实践 | 优先级 | 实施方式 |
|------|--------|----------|
| 断路器 | 关键 | 始终启用 |
| DNS 泄露保护 | 关键 | 使用 Mullvad DNS |
| 自动连接 | 高 | 随系统启动 |
| WebRTC 泄露防护 | 高 | 浏览器设置 |
| HTTPS Everywhere | 中等 | 浏览器扩展 |

### 浏览器配置

| 设置 | 推荐 | 原因 |
|------|------|------|
| WebRTC | 禁用 | 防止 IP 泄露 |
| DNS over HTTPS | 启用 | 加密 DNS |
| Cookies | 阻止第三方 | 减少追踪 |
| 扩展 | uBlock Origin | 拦截广告/追踪器 |

### 设备级隐私

| 层级 | 工具 | 用途 |
|------|------|------|
| 操作系统 | 全盘加密 | 数据保护 |
| 应用 | 应用权限 | 限制访问 |
| 网络 | 防火墙 | 控制流量 |
| 浏览器 | 隐私优先 | 减少指纹识别 |

### 支付隐私

| 方式 | 匿名性 | 便利性 |
|------|--------|--------|
| 现金 | 最高 | 最低 |
| 加密货币 | 高 | 中等 |
| 信用卡 | 低 | 最高 |
| 银行转账 | 低 | 中等 |

---

## 故障排除

Mullvad VPN 常见问题及解决方案。

### 连接问题

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 无法连接 | 防火墙阻止 | 允许 Mullvad 通过防火墙 |
| 速度慢 | 服务器过载 | 切换服务器 |
| 频繁断开 | 网络不稳定 | 更改协议 |
| DNS 泄露 | 配置问题 | 重新安装应用 |

### 速度优化

| 因素 | 影响 | 解决方案 |
|------|------|----------|
| 服务器距离 | 高 | 选择更近的服务器 |
| 服务器负载 | 中等 | 选择较空闲的服务器 |
| 协议 | 中等 | 使用 WireGuard |
| 加密级别 | 低 | 默认设置 |

### 常见错误信息

| 错误 | 含义 | 修复 |
|------|------|------|
| "Blocked" | 断路器已激活 | 重新连接 VPN |
| "DNS error" | DNS 解析失败 | 更改 DNS 设置 |
| "Auth failed" | 账号问题 | 检查账号状态 |
| "Timeout" | 连接太慢 | 尝试其他服务器 |

### 诊断命令

```bash
# Check public IP
curl ifconfig.me

# Test DNS leak
nslookup example.com

# Check connection logs
mullvad relay get

# Reset settings
mullvad reset
```

---

## 安全考虑

了解 VPN 的局限性和补充安全措施。

### VPN 安全模型

| 保护 | VPN 提供 | VPN 不提供 |
|------|----------|------------|
| IP 隐藏 | 是 | - |
| 加密 | 是 | - |
| 匿名性 | 部分 | 完全匿名 |
| 恶意软件防护 | 否 | 需要杀毒软件 |
| 钓鱼防护 | 否 | 需要意识 |

### 威胁缓解矩阵

| 威胁 | VPN | 其他工具 |
|------|-----|----------|
| ISP 窥探 | 有效 | - |
| WiFi 窃听 | 有效 | - |
| 恶意软件 | 否 | 杀毒软件 |
| 钓鱼 | 否 | 邮件过滤器 |
| 浏览器追踪 | 部分 | 隐私浏览器 |
| 社会工程 | 否 | 用户教育 |

### 审计历史

| 年份 | 审计方 | 范围 | 结果 |
|------|--------|------|------|
| 2020 | Assured AB | 基础设施 | 通过 |
| 2021 | Cure53 | 应用安全 | 通过 |
| 2022 | Assured AB | 策略合规 | 通过 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 协议 | WireGuard 提供最佳的速度-安全平衡 |
| 配置 | 启用断路器和 DNS 泄露保护 |
| 隐私 | 结合 VPN 与浏览器和设备隐私 |
| 支付 | 现金或加密货币实现最大匿名性 |
| 维护 | 保持应用更新并检查连接状态 |


---

## 来源：privacy2.md

## 简介

Awesome Privacy 是一个精心策划的尊重隐私的软件和服务列表。本指南涵盖了维护数字隐私的基本工具，涵盖从通信到浏览和文件存储的各个类别。

## 目录

1. [隐私原则](#隐私原则)
2. [通信工具](#通信工具)
3. [Web 浏览器](#web-浏览器)
4. [电子邮件服务](#电子邮件服务)
5. [云存储](#云存储)
6. [VPN 服务](#vpn-服务)
7. [操作系统](#操作系统)
8. [密码管理器](#密码管理器)
9. [搜索引擎](#搜索引擎)

## 隐私原则

| 原则 | 说明 |
|------|------|
| 数据最小化 | 仅收集必要数据 |
| 端到端加密 | 仅发送方和接收方可读 |
| 开源 | 可审计的代码 |
| 无遥测 | 无使用跟踪 |
| 本地处理 | 数据保留在设备上 |
| 零知识 | 提供商无法访问您的数据 |

## 通信工具

### 即时通讯应用

| 应用 | 平台 | E2E 加密 | 开源 | 可自托管 |
|------|------|----------|------|----------|
| Signal | 全平台 | 是 | 是 | 否 |
| Matrix/Element | 全平台 | 是 | 是 | 是 |
| Briar | Android | 是 | 是 | 否 |
| Session | 全平台 | 是 | 是 | 否 |
| Wire | 全平台 | 是 | 部分 | 是 |

### 对比详情

| 功能 | Signal | Matrix | Briar | Session |
|------|--------|--------|-------|---------|
| 需要手机号 | 是 | 否 | 否 | 否 |
| 群聊 | 是 | 是 | 是 | 是 |
| 语音通话 | 是 | 是 | 是 | 否 |
| 视频通话 | 是 | 是 | 否 | 否 |
| 文件共享 | 是 | 是 | 是 | 是 |
| 元数据保护 | 良好 | 中等 | 优秀 | 优秀 |

### 语音和视频

| 应用 | 平台 | 加密 | 可自托管 |
|------|------|------|----------|
| Jitsi Meet | Web | 可选 | 是 |
| BigBlueButton | Web | 是 | 是 |
| Mumble | 桌面 | 是 | 是 |
| Tox | 桌面 | 是 | 否 |

## Web 浏览器

### 浏览器对比

| 浏览器 | 引擎 | 隐私重点 | 扩展 | 移动端 |
|--------|------|----------|------|--------|
| Firefox | Gecko | 高 | 优秀 | 是 |
| Brave | Chromium | 高 | 良好 | 是 |
| Tor Browser | Gecko | 最高 | 有限 | 是 |
| LibreWolf | Gecko | 最高 | 良好 | 否 |
| Mullvad Browser | Gecko | 最高 | 有限 | 否 |

### Firefox 加固设置

| 设置 | 值 | 影响 |
|------|----|------|
| `privacy.resistFingerprinting` | true | 减少指纹识别 |
| `network.http.referer.XOriginPolicy` | 2 | 限制来源数据 |
| `dom.event.clipboardevents.enabled` | false | 阻止剪贴板跟踪 |
| `media.navigator.enabled` | false | 阻止摄像头/麦克风访问 |

### 必备隐私扩展

| 扩展 | 用途 | 浏览器 |
|------|------|--------|
| uBlock Origin | 广告/跟踪器拦截 | 全部 |
| HTTPS Everywhere | 强制 HTTPS | 大多数 |
| NoScript | JavaScript 控制 | Firefox |
| Privacy Badger | 跟踪器拦截 | 大多数 |
| Cookie AutoDelete | Cookie 管理 | 大多数 |

## 电子邮件服务

### 注重隐私的邮件提供商

| 提供商 | E2E 加密 | 存储 | 价格 | 管辖权 |
|--------|----------|------|------|--------|
| ProtonMail | 是 | 1 GB 免费 | 免费增值 | 瑞士 |
| Tutanota | 是 | 1 GB 免费 | 免费增值 | 德国 |
| Mailbox.org | 否 | 2 GB | 1 欧元/月 | 德国 |
| Disroot | 否 | 1 GB | 免费 | 荷兰 |
| Posteo | 否 | 2 GB | 1 欧元/月 | 德国 |

### 邮件安全功能

| 功能 | ProtonMail | Tutanota | Mailbox.org |
|------|------------|----------|-------------|
| 零访问加密 | 是 | 是 | 否 |
| PGP 支持 | 是 | 否 | 是 |
| 日历 | 是 | 是 | 是 |
| 联系人 | 是 | 是 | 是 |
| 自定义域名 | 付费 | 付费 | 是 |
| IMAP/SMTP | Bridge | 否 | 是 |

### 邮件别名服务

| 服务 | 免费额度 | 域名 | 用途 |
|------|----------|------|------|
| SimpleLogin | 10 个别名 | 多个 | 转发 |
| AnonAddy | 20 个别名 | 多个 | 转发 |
| Firefox Relay | 5 个别名 | 1 | 转发 |

## 云存储

### 注重隐私的存储

| 提供商 | E2E 加密 | 开源 | 存储 | 价格 |
|--------|----------|------|------|------|
| Nextcloud | 插件 | 服务器 + 客户端 | 自托管 | 免费 |
| Tresorit | 是 | 否 | 1 GB 免费 | 高级 |
| Cryptomator | 是 | 是 | 任意存储 | 免费 |
| MEGA | 是 | 部分 | 20 GB 免费 | 免费增值 |
| Syncthing | 不适用 | 是 | P2P | 免费 |

### Nextcloud 与替代方案

| 功能 | Nextcloud | Tresorit | MEGA |
|------|-----------|----------|------|
| 可自托管 | 是 | 否 | 否 |
| 文件同步 | 是 | 是 | 是 |
| 日历 | 是 | 否 | 否 |
| 联系人 | 是 | 否 | 否 |
| 办公套件 | 是 | 否 | 否 |
| 最大文件大小 | 无限制 | 5 GB | 不等 |

## VPN 服务

### 可信 VPN 提供商

| 提供商 | 日志 | 管辖权 | 协议 | 价格 |
|--------|------|--------|------|------|
| Mullvad | 无 | 瑞典 | WireGuard | 5 欧元/月 |
| ProtonVPN | 无 | 瑞士 | WireGuard, OpenVPN | 免费增值 |
| IVPN | 无 | 直布罗陀 | WireGuard, OpenVPN | 6 美元/月起 |
| AirVPN | 无 | 意大利 | WireGuard, OpenVPN | 2 欧元/月起 |

### VPN 协议对比

| 协议 | 速度 | 安全性 | 已审计 | 推荐 |
|------|------|--------|--------|------|
| WireGuard | 快 | 高 | 是 | 是 |
| OpenVPN | 中等 | 高 | 是 | 是 |
| IKEv2 | 快 | 高 | 是 | 是 |
| L2TP/IPsec | 中等 | 中等 | 是 | 否 |

### VPN 选择标准

| 标准 | 重要性 | 关注点 |
|------|--------|--------|
| 无日志政策 | 关键 | 独立审计 |
| 管辖权 | 高 | 14 眼联盟之外 |
| 开源 | 高 | 可审计客户端 |
| 支付方式 | 中等 | 接受加密货币 |
| 服务器数量 | 低 | 质量优于数量 |

## 操作系统

### 注重隐私的操作系统

| 操作系统 | 平台 | 基于 | 隐私级别 |
|----------|------|------|----------|
| Tails | 桌面 | Debian | 最高 |
| Qubes OS | 桌面 | Fedora/Xen | 高 |
| GrapheneOS | 移动 | Android | 高 |
| CalyxOS | 移动 | Android | 高 |
| LineageOS | 移动 | Android | 中等 |

### 移动操作系统对比

| 功能 | GrapheneOS | CalyxOS | LineageOS |
|------|------------|---------|-----------|
| 仅 Pixel | 是 | 是 | 否 |
| 沙盒 | 增强 | 标准 | 标准 |
| MicroG | 否 | 是 | 可选 |
| 验证启动 | 是 | 是 | 否 |
| 默认应用 | 最小 | 标准 | 不等 |

## 密码管理器

### 密码管理器对比

| 管理器 | 开源 | E2E 加密 | 平台 | 价格 |
|--------|------|----------|------|------|
| Bitwarden | 是 | 是 | 全平台 | 免费增值 |
| KeePassXC | 是 | 仅本地 | 桌面 | 免费 |
| 1Password | 否 | 是 | 全平台 | 高级 |
| Proton Pass | 是 | 是 | 全平台 | 免费增值 |
| KeePassDX | 是 | 仅本地 | Android | 免费 |

### 功能对比

| 功能 | Bitwarden | KeePassXC | Proton Pass |
|------|-----------|-----------|-------------|
| 云同步 | 是 | 否 | 是 |
| 浏览器扩展 | 是 | 是 | 是 |
| TOTP 支持 | 是 | 是 | 是 |
| 文件附件 | 是 | 否 | 是 |
| 紧急访问 | 是 | 否 | 否 |
| 可自托管 | 是 | 不适用 | 否 |

## 搜索引擎

### 隐私搜索引擎

| 引擎 | 结果来源 | 广告 | 跟踪 | 即时答案 |
|------|----------|------|------|----------|
| DuckDuckGo | Bing | 是（非跟踪） | 否 | 是 |
| Startpage | Google | 是（非跟踪） | 否 | 是 |
| SearXNG | 多个 | 否 | 否 | 是 |
| Brave Search | 自有索引 | 否 | 否 | 是 |
| Mojeek | 自有索引 | 否 | 否 | 有限 |

### 搜索引擎选择

| 使用场景 | 推荐 |
|----------|------|
| 通用隐私 | DuckDuckGo 或 Brave Search |
| Google 结果 | Startpage |
| 可自托管 | SearXNG |
| 无跟踪 | Mojeek |
| 学术搜索 | SearXNG 配合学术引擎 |

## 其他工具

### DNS 隐私

| 提供商 | DNS-over-HTTPS | DNS-over-TLS | 日志 |
|--------|----------------|--------------|------|
| Cloudflare | 是 | 是 | 临时 |
| Quad9 | 是 | 是 | 临时 |
| NextDNS | 是 | 是 | 可配置 |
| Mullvad | 是 | 是 | 无 |

### 元数据移除

| 工具 | 平台 | 支持格式 |
|------|------|----------|
| ExifTool | 全平台 | 所有格式 |
| mat2 | Linux | 图像、文档、媒体 |
| ExifCleaner | 桌面 | 图像、PDF |
| Scrambled Exif | Android | 图像 |

## 总结

维护数字隐私需要为通信、浏览、存储和系统安全选择适当的工具。具有端到端加密的开源解决方案提供最强的隐私保障。本指南中列出的工具代表了每个类别的成熟选项，允许用户构建全面的隐私优先工作流。


---

## 来源：survival.md

## The Rule of 3

Survival priorities are governed by a simple framework:

| Priority | Time Limit | Action |
|----------|------------|--------|
| Air / severe bleeding | 3 minutes | Address immediately -- clear airways, stop hemorrhaging |
| Shelter / body temperature | 3 hours | Protect from exposure in extreme conditions |
| Water | 3 days | Secure a water source |
| Food | 3 weeks | Find calories (lowest priority in short-term survival) |

In most outdoor emergencies, **exposure** (hypothermia or hyperthermia) is the first lethal threat, not starvation or dehydration. Build or find shelter before searching for water.

## Shelter Building

### Site Selection

- Avoid dry riverbeds (flash flood risk).
- Avoid lone trees and hilltops (lightning risk).
- Avoid avalanche paths, rockfall zones, and dead trees with hanging branches.
- Look for natural windbreaks: rock faces, dense tree lines, ridges.
- Stay slightly elevated to avoid cold air pooling in valleys.

### Emergency Shelter Types

| Shelter | Materials | Time to Build | Best For |
|---------|-----------|---------------|----------|
| Debris hut | Branches, leaves, pine needles | 1-2 hours | Cold weather, solo |
| Lean-to | Long branches, tarp/poncho | 30-60 min | Moderate conditions |
| Snow cave | Compact snow | 1-3 hours | Deep snow, extreme cold |
| A-frame tarp | Cordage, tarp/poncho | 15-30 min | Rain, mild cold |
| Natural shelter | Caves, rock overhangs | Minimal | Any conditions (check for occupants) |

### Debris Hut Construction

1. Find a ridgepole -- a sturdy branch about 9 feet long.
2. Prop one end on a stump or rock at about 3 feet high, or wedge into a tree fork.
3. Lean shorter branches along both sides to form an A-frame.
4. Pile debris (leaves, pine needles, grass) thickly over the frame -- at least 2 feet deep.
5. Line the inside with dry debris for insulation from the ground.
6. Keep the entrance small and plug it with debris when inside.

The inside should be just large enough for your body. A smaller space retains heat better.

## Water Purification

Dehydration kills within days. Never skip water purification in the backcountry.

### Methods

| Method | Kills Bacteria? | Kills Viruses? | Removes Chemicals? | Notes |
|--------|-----------------|----------------|-------------------|-------|
| Boiling (1 minute at rolling boil) | Yes | Yes | No | Most reliable method |
| Chemical treatment (iodine/chlorine) | Yes | Yes (with wait time) | No | Taste can be unpleasant; follow dosage carefully |
| UV light (SteriPEN) | Yes | Yes | No | Requires batteries; clear water works best |
| Pump filter (0.2 micron) | Yes | No (most models) | No | Fast; backflush to maintain |
| Gravity filter (Sawyer, Platypus) | Yes | No (most models) | No | Good for groups; slow |
| SODIS (sunlight in clear bottles) | Partial | Partial | No | Last resort; requires 6+ hours of direct sun |
| Boiling + charcoal filter | Yes | Yes | Partial | Improves taste after boiling |

### Water Source Priority

1. Spring water emerging from rock -- generally safest natural source.
2. Fast-moving streams in forested, uninhabited areas.
3. Lakes and ponds (requires thorough treatment).
4. Puddles and standing water (last resort; heavy treatment needed).
5. Snow -- melt before drinking. Eating snow lowers body temperature.

## Fire Starting

Fire provides warmth, purifies water (via boiling), signals rescuers, and boosts morale.

### Fire Triangle

You need three elements: **heat** (ignition), **fuel** (wood), and **oxygen** (airflow). Remove any one and the fire dies.

### Ignition Methods

| Method | Reliability | Skill Required | Notes |
|--------|-------------|----------------|-------|
| Waterproof matches | High | Minimal | Carry in sealed container |
| Butane lighter | High | Minimal | May fail at altitude or extreme cold |
| Ferrocerium rod | High | Moderate | Works wet, lasts thousands of strikes |
| Magnifying lens / Fresnel lens | Moderate | Low | Requires direct sunlight |
| Bow drill | Low (for beginners) | High | Friction fire; requires practice |
| Flint and steel | Moderate | Moderate | Traditional; requires char cloth or tinder |

### Fire Lay Structure

1. **Tinder**: Fine, dry material that catches a spark. Examples: birch bark shavings, dryer lint, cotton balls with petroleum jelly, dry grass, cedar bark fibers, fatwood shavings.
2. **Kindling**: Pencil-thin dry sticks and twigs.
3. **Fuel**: Progressively larger wood, from finger-thick to wrist-thick.

Build in a teepee or log cabin structure. Light the tinder, add kindling as the flame grows, then add fuel gradually. Do not smother a young fire with too much wood too soon.

## Navigation

### Map and Compass

The most reliable navigation method. Electronics fail; a compass does not.

**Basic compass use:**
1. Hold the compass flat in front of you.
2. Rotate the bezel until the red magnetic needle aligns with the orienting arrow (red in the shed).
3. Read your bearing at the index line.
4. To follow a bearing: rotate your body until the needle aligns, then walk toward a landmark in that direction.

**Declination**: Magnetic north and true north differ. Adjust your compass or account for the difference (shown on your topographic map).

### Map Reading Essentials

| Symbol | Meaning |
|--------|---------|
| Contour lines close together | Steep terrain |
| Contour lines far apart | Gentle terrain |
| V-shape pointing uphill | Valley or stream |
| V-shape pointing downhill | Ridge |
| Blue lines/shapes | Water features |
| Brown lines | Elevation contours |
| Green shading | Vegetation |

### Natural Navigation

When you lack a compass:

| Method | Technique |
|--------|-----------|
| Sun position | Sun rises in the east, sets in the west. At solar noon it is due south (northern hemisphere) or due north (southern hemisphere). |
| Shadow stick | Plant a stick upright. Mark shadow tip. Wait 15 minutes. Mark again. The line from first to second mark runs roughly west-to-east. |
| North Star (Polaris) | Locate the Big Dipper. The two stars forming the outer edge of the cup point toward Polaris. Polaris indicates true north. |
| Moss and vegetation | Unreliable as a sole indicator. Moss often grows on the shaded side of trees in humid climates, but it grows on all sides too. Use only as a corroborating clue. |
| Prevailing wind | If you know the prevailing wind direction for the area, you can orient from it. |

## Edible Plants

**Critical warning**: Misidentifying plants can be fatal. Do not eat any plant you cannot identify with certainty. When in doubt, do not eat it.

### The Universal Edibility Test

If you must test an unknown plant and have no other food source:

1. Test for contact reaction: Rub on inner wrist. Wait 15 minutes.
2. Test for lip reaction: Touch to corner of mouth. Wait 15 minutes.
3. Test for tongue reaction: Place on tongue. Wait 15 minutes.
4. Test for mouth reaction: Chew and hold in mouth (do not swallow). Wait 15 minutes.
5. Test for digestion: Swallow a small amount. Wait 8 hours.

If any reaction occurs at any stage, stop immediately.

### Commonly Recognizable Edible Plants (Temperate Regions)

| Plant | Parts Eaten | Identification |
|-------|-------------|----------------|
| Cattail | Shoots, roots, pollen | Tall marsh plant with brown cigar-shaped heads |
| Dandelion | Leaves, flowers, roots | All parts edible; unmistakable yellow flower |
| Pine | Inner bark, needles (tea) | Any pine species; needle tea provides vitamin C |
| Acorns (processed) | Nuts | Must leach tannins by soaking in water |
| Wild garlic/ramps | Leaves, bulbs | Onion/garlic smell when crushed |
| Blackberries | Fruit | Thorny brambles; berries in late summer |

### Plants to Avoid

- Any plant with milky or discolored sap.
- Any plant with a bitter or soapy taste.
- Umbrella-shaped flower clusters (resemble poison hemlock).
- Beans or seeds from pods you cannot identify.
- Any plant with a strong almond scent in the leaves (cyanide compounds).

## Signaling for Rescue

| Method | Visibility | How |
|--------|------------|-----|
| Signal fire (3 in a triangle) | 10+ miles in daylight; farther at night | Three fires spaced 100 feet apart is an international distress signal |
| Whistle | 1 mile | Three blasts = distress signal. Easier than shouting and carries farther |
| Mirror / reflective surface | 10+ miles in sunlight | Flash toward aircraft or distant observers |
| Ground-to-air signals | Aircraft altitude | Large letters made with rocks, logs, or stomped in snow. X = need help, V = need assistance, arrow = direction of travel |
| Bright clothing / gear | Visual range | Spread out on open ground for contrast |
| GPS messenger (PLB / inReach) | Satellite | Activates search and rescue directly |

## First Aid Basics

| Situation | Action |
|-----------|--------|
| Severe bleeding | Apply direct pressure with clean cloth. If bleeding cannot be controlled, apply a tourniquet 2-3 inches above the wound and note the time. |
| Fracture | Splint in the position found. Use sticks, trekking poles, or rolled clothing. Immobilize the joints above and below. |
| Hypothermia | Remove wet clothing. Insulate from the ground. Provide warm drinks (not alcohol). Skin-to-skin contact if severe. |
| Heat exhaustion / heat stroke | Move to shade. Remove excess clothing. Cool with water on neck, armpits, groin. Heat stroke (confusion, no sweating) is a medical emergency. |
| Snakebite | Keep calm and still. Remove jewelry near the bite. Do not cut, suck, or tourniquet. Evacuate. |
| Allergic reaction (anaphylaxis) | Use epinephrine auto-injector if available. Elevate legs. Evacuate. |

## Weather Reading

| Sign | Likely Weather |
|------|----------------|
| Rapidly falling barometric pressure | Storm approaching |
| High, thin cirrus clouds thickening | Rain or snow within 24-48 hours |
| Towering cumulus clouds | Thunderstorms possible |
| Red sky at night (clear western horizon) | Fair weather (mid-latitude) |
| Sudden temperature drop with wind | Cold front passing; precipitation likely |
| Increasing wind speed with falling pressure | Deteriorating conditions |
| Ring around the moon | Moisture in upper atmosphere; rain likely within 1-2 days |

## Gear Checklist

### The Ten Essentials

| Item | Purpose |
|------|---------|
| Navigation (map, compass, GPS) | Know where you are and where to go |
| Sun protection (sunscreen, sunglasses, hat) | Prevent sunburn, snow blindness |
| Insulation (extra layers) | Prepare for unexpected weather |
| Illumination (headlamp, spare batteries) | See and be seen after dark |
| First aid kit | Treat injuries |
| Fire starter (matches, lighter, ferro rod) | Warmth, water purification, signaling |
| Repair tools (knife, duct tape, cordage) | Fix gear, build shelter |
| Nutrition (extra food) | Energy for unexpected delays |
| Hydration (extra water, purification) | Prevent dehydration |
| Emergency shelter (tarp, bivvy, space blanket) | Protection from exposure |

### Additional Recommendations

- Tell someone your plan: where you are going, your route, and when you expect to return.
- Carry a whistle on your person, not in your pack.
- A knife with a fixed blade is more reliable than a folding knife in survival situations.
- Duct tape wrapped around a water bottle or trekking pole saves pack weight and is endlessly useful.


---

## 来源：sentinel.md

**Source:** https://github.com/kr-stn/awesome-sentinel

## Overview

This tutorial covers the key resources and tools from the [kr-stn/awesome-sentinel](https://github.com/kr-stn/awesome-sentinel) project.

## Awesome Sentinel

A curated list of awesome tools, tutorials and APIs related to data from the [Copernicus Sentinel Satellites](http://www.copernicus.eu/main/sentinels).

## Data Hubs and National Mirrors

Official datahubs and mirrors by the Copernicus partners and [Collaborative Ground Segment members](https://sentinels.copernicus.eu/web/sentinel/missions/collaborative/national-points-of-contact).

- [**Copernicus Data Spaces Ecosystem (CDSE)**](https://dataspace.copernicus.eu/)
- [**Australia National Mirror**](https://copernicus.nci.org.au/)
- [**Austria National Mirror**](https://data.sentinel.zamg.ac.at/)
- [**Czech Rebublic National Mirror**](https://dhr1.cesnet.cz/#/home)
- [**Estonia National Mirror**](https://geoportaal.maaamet.ee/eng/Spatial-Data/National-Satellite-Data-Centre-ESTHub-p654.html)
- [**Finland National Mirror**](https://finhub.nsdc.fmi.fi/)
- [**France National Mirror (PEPS)**](https://peps.cnes.fr/rocket/)
- [**Germany National Mirror (CODE-DE)**](https://code-de.org/)
- [**Greece National Mirror**](https://sentinels.space.noa.gr/)
- [**Luxembourg National Mirror**](https://www.collgs.lu/)
- [**Norway National Mirror**](https://colhub.met.no/#/home)
- [**Portugal National Mirror**](https://ipsentinel.ipma.pt/dhus/#/home)
- [**United Kingdom National Mirror (SEDAS)**](http://sedas.satapps.org/)

## Partial Mirrors

Initiatives to integrate specific Sentinel data into existing search and discovery platforms.

- [**Alaska Satellite Facility (Sentinel-1)**](https://www.asf.alaska.edu/sentinel/)
- [**Centre for Environmental Data Analysis - CEDA (Sentinel-1, -2)**](http://catalogue.ceda.ac.uk/search/?search_term=sentinel&return_obj=ob&search_obj=ob)
- [**Theia (Sentinel-2)**](https://theia.cnes.fr/atdistrib/rocket/#/search?collection=SENTINEL2)
  - atmospherically corrected L2A products covering several European countries and [areas proposed by scientists](http://www.cesbio.ups-tlse.fr/multitemp/?page_id=7501)
  - published less than two days after L1C is available
- [**USGS EarthExplorer (Sentinel-2)**](https://earthexplorer.usgs.gov/)
- [**EUMETSAT CODA (Sentinel-3 Marine Products)**](https://coda.eumetsat.int/#/home)
  - 14 day rolling archive of Sentinel-3 L1 and L2 marine products in near real-time (NRT), short time critical (STC) and non time critical (NTC) latency mode
- [**DLR Geoservice (Sentinel-2)**](https://geoservice.dlr.de/web/)
  - [Download](https://download.geoservice.dlr.de/S2_L2A_MAJA/files/) 2 years rolling archive of MAJA-corrected Sentinel-2 scenes covering Germany
- [**NOAA CoastWatch**](https://coastwatch.noaa.gov/)
    - Sentinel-3 OLCI and Sentinel-2 over United States coasts
- [**NASA Earthdata**](https://search.earthdata.nasa.gov/)
    - search NASA mirrors for Sentinel-1, Sentinel-3, and Sentinel-5P

## Cloud Providers

Providers that host Copernicus Sentinel data and allow you to bring your own code to process it without the need to download the data.

- [**Open data on AWS**](https://registry.opendata.aws/tag/satellite-imagery/)
  - [Sentinel-2 L1C and L2A](https://registry.opendata.aws/sentinel-2/) hosted in region `eu-central-1` (Frankfurt), requester-pays S3 buckets
  - [Sentinel-2 L2A Cloud-Optimized GeoTIFFs](https://registry.opendata.aws/sentinel-2-l2a-cogs/), hosted in region `us-west-2` (Oregon), S3 buckets
    - [STAC Browser](https://sentinel.stac.cloud/?t=catalogs) for Sentinel-2 COG hosted on AWS
  - [Sentinel-1 GRD](https://registry.opendata.aws/sentinel-1/) hosted in region `eu-central-1` (Frankfurt), requester-pays S3 buckets
  - [Sentinel-1 ARD CONUS](https://registry.opendata.aws/sentinel-1-rtc-indigo/) - analysis ready dataset of Sentinel-1, tiled COGs, for contiguous United States
  - [Sentinel-3 NRT, STC, NTC, COG](https://registry.opendata.aws/sentinel-3/) - all Sentinel-3 products for near-real time, short time critical and not time critical, all products also available converted to COGs
  - [Sentinel-5P L2](https://registry.opendata.aws/sentinel5p/) -  all Level-2 products from Sentinel-5P, also available as COG converted data
- [**Google (Sentinel-2)**](https://cloud.google.com/storage/docs/public-datasets/sentinel-2)
  - public [Google Cloud Storage bucket](https://console.cloud.google.com/storage/browser/gcp-public-data-sentinel-2/?pli=1), `.SAFE` format, EU region
- [**Planet**](https://www.planet.com/pulse/sentinel-2-and-landsat-8-data-now-available-on-the-planet-platform/)
  - Sentinel-2 included in commercial API
- [**Microsoft Planetary Computer**](https://planetarycomputer.microsoft.com)
  - offers many EO catalogs as COGs, including [Sentinel-2 L2A](https://planetarycomputer.microsoft.com/dataset/sentinel-2-l2a) data. provides a STAC-API. data can be obtained free of charge, but must be signed with a [SAS token](https://planetarycomputer.microsoft.com/docs/concepts/sas/).

## DIAS

[Data and Information Access Services (DIAS)](https://www.copernicus.eu/en/access-data/dias), funded by the European Commission "providing  centralised  access  to  Copernicus  data  and  information,  as  well as to processing tools"
- [**CREODIAS**](https://creodias.eu/)
  - full Sentinel archive, free visualization and download through [data discovery portal](https://finder.creodias.eu/www/) and [CREODIAS Browser](http://browser.creodias.eu/)
  - large EO [data archive](https://creodias.eu/data-offer) including Landsat, Envisat and others, next to Copernicus data
- [**MUNDI**](https://mundiwebservices.com)
  - Sentinel archive, free visualization and download through [mundi web services](https://mundiwebservices.com/geodata/)
- [**ONDA DIAS**](https://www.onda-dias.eu/cms/)
  - VM Infrastructure as a Service, with an API for access to hosted Copernicus data
- [**sobloo**](https://sobloo.eu)
  - on-demand processing of thematic products with link to other data-sets (i.e. geo-marketing)
- [**WEkEO**](https://wekeo.eu/)
  - harmonised data access with a REST API, hosted VM options

## Tools

Specific to Copernicus Sentinel data discovery, download and processing.

## Search & Download

- [**`sentinelsat`**](https://github.com/sentinelsat/sentinelsat)
  - search and download from any [DHuS](https://github.com/SentinelDataHub/)-powered Datahub. Comes with an intuitive command line and a flexible Python API.
- [**`Sentinel-download`**](https://github.com/olivierhagolle/Sentinel-download)
  - download Sentinel-2 data from Copernicus SciHub. Supports download of sub-tiles in the old product format (PDS <14).
- [**`peps_download`**](https://github.com/olivierhagolle/peps_download)
  -  download data from the French National Mirror (PEPS).
- [**`Sentinel2ProductIngestor`**](https://github.com/sinergise/Sentinel2ProductIngestor)
  - ingest Sentinel-2 data from SciHub into S3. Used by [Sinergise](https://github.com/sinergise) to populate the [AWS Sentinel-2 mirror](http://sentinel-pds.s3-website.eu-central-1.amazonaws.com/)
- [**`sat-download`**](https://github.com/sat-utils/sat-download)
  - download Sentinel-2 data from AWS
- [**`sat-api`**](https://github.com/sat-utils/sat-api)
  - query Sentinel-2 data on AWS using APIGateWay
  - deployed by Development Seed at [https://api.developmentseed.org/satellites](https://api.developmentseed.org/satellites)
- [**`awsdownload`**](https://github.com/kraftek/awsdownload)
  - downloader for Sentinel-2 products from Amazon or SciHub
- [**`sentinelhub-py`**](https://github.com/sentinel-hub/sentinelhub-py)
  - Python library for downloading Sentinel-2 data from Amazon into ESA .SAFE format and interface [Sentinel Hub OGC services](https://www.sentinel-hub.com/develop/capabilities/wms)
- [**`aws-sat-api`**](https://github.com/RemotePixel/aws-sat-api)
  - Simple Serverless API for satellite data hosted on AWS Public Dataset
- [**`sentinel2-search-api`**](https://github.com/beaorn/sentinel2-search-api)
  - query Sentinel-2 data hosted on AWS by MGRS tile
  - API deployed at [https://sentinel2.satgateway.com](https://sentinel2.satgateway.com), tile preview front-end deployed at [https://s2viewer.satgateway.com](https://s2viewer.satgateway.com)
- [**`sentinel2_aws`**](https://github.com/beaorn/sentinel2_aws)
  - Ruby gem for parsing Sentinel-2 metadata from AWS
- [**`eodag`**](https://github.com/CS-SI/eodag)
  - command line tool and plugin-oriented Python framework for search and download from [multiple providers](https://eodag.readthedocs.io/en/stable/getting_started_guide/providers.html) including all DIAS
- [**`sentinelloader`**](https://github.com/flaviostutz/sentinelloader)
  - Sentinel-2 satellite tiles images downloader from Copernicus. Minimizes data download and combines multiple tiles to return a single area of interest

## Viewers & Portals

- [**AWS/Sinergise "Sentinel Image Browser"**](http://sentinel-pds.s3-website.eu-central-1.amazonaws.com/browser.html)
  - search Sentinel-2 data available on Amazon Webservices
- [**EOS "Land Viewer"**](https://lv.eos.com/)
  - viewer for Landsat-8/7, MODIS and Sentinel-2 data hosted by AWS
  - visualize band combinations on-the-fly
- [**jeobrowser "Rocket"**](https://mapshup.com/projects/rocket)
  - viewer for Sentinel (1,2,3), Landsat-8, SPOT and Pleiades imagery
  - based on [resto](https://github.com/jjrom/resto) search engine and used as frontend for [PEPS](https://peps.cnes.fr/rocket/)
- [**mundialis "EO-me"**](https://www.mundialis.de/en/earth-observation-metadata-enhancer/)
  - viewer for Sentinel-2 and Landsat-8 data with custom metadata filters
  - satellite tiles enriched with additional metadata (e.g. terrain statistics, NDVI at overpass, climatic parameters, population count)
- [**OceanDataLab**](https://www.oceandatalab.com)
  - portals focussing on Ocean Remote Sensing data, including Sentinel-1 and 3
- [**Research and User Support (RUS)**](https://rus-copernicus.eu/)
  - service portal to promote the uptake of Copernicus data and scaling of R&D activities
  - provides [training](https://rus-copernicus.eu/portal/the-rus-offer/training/) and [computing environments](https://rus-copernicus.eu/portal/the-rus-offer/ict-offer/)
- [**Sinergise "Sentinel Playground"**](http://apps.sentinel-hub.com/sentinel-playground)
  - visualize AWS Sentinel-2 data in different band combinations
  - offers a [WMS/WMTS service](http://www.sentinel-hub.com/apps/wms).
- [**Sinergise "Sentinel-Hub"**](https://www.sentinel-hub.com/)
  - search Sentinel-1, 2, 3 and other free satellite data
  - supports pixel based band-math operations and [simple data processing](http://www.sentinel-hub.com/blog/eo-browser-goes-public)
- [**SnapPlanet**](https://snapplanet.io/)
  - [Android](https://play.google.com/store/apps/details?id=io.snapplanet.app) / [iOS](https://itunes.apple.com/WebObjects/MZStore.woa/wa/viewSoftware?id=1175935057) App to to view Sentinel-2 images, compare changes and share
- [**Spectator**](https://spectator.earth/)
  - real-time tracking of EO satellites, set-up custom channels to track ROI overpass and preview images
- [**Thematic Exploitation Platforms "TEPs"**](https://tep.eo.esa.int/)
  - platforms for finding and processing (Sentinel) data relating to a thematic topic
  - available platforms: [Coastal](https://coastal-tep.eo.esa.int/portal), [Forestry](https://forestry-tep.eo.esa.int/), [Geohazards](https://geohazards-tep.eo.esa.int/), [Hydrology](https://hydrology-tep.eo.esa.int/), [Polar](https://polar-tep.eo.esa.int/), [Urban](https://urban-tep.eo.esa.int/#!), [Food Security](https://foodsecurity-tep.eo.esa.int/)
- [**USGS "Sentinel2Look"**](https://landsatlook.usgs.gov/sentinel2/viewer.html)
    - variant of the [LandsatLook Viewer](https://landsatlook.usgs.gov/) to search and download Sentinel-2 data from the USGS archive
- [**ESRI Sentinel-2 Explorer**](https://sentinel2explorer.esri.com/)
    - view Sentinel-2 data rendered with a [number of indexes](https://www.arcgis.com/home/group.html?id=658741129719420f83d503a3ba743def#overview)
    - available as [ArcGIS ImageServer (REST)](https://sentinel.arcgis.com/arcgis/rest/services/Sentinel2/ImageServer)

- ~~[**RemotePixel "Viewer"**](https://viewer.remotepixel.ca)~~ **(no longer active)**
  - [open source](https://github.com/RemotePixel/viewer.remotepixel.ca) viewer for Landsat-8, Sentinel-2 and CBERS-4 data hosted by AWS
  - uses [**`sentinel-tiler`**](https://github.com/mapbox/sentinel-tiler) (tiles server based on AWS Lambda)
- ~~[**RemotePixel "Satellite Search"**](https://remotepixel.ca/projects/satellitesearch.html)~~ **(no longer active)**
  - [open source](https://github.com/RemotePixel/satellitesearch) Browser for Landsat-8 and Sentinel-2 data hosted by AWS
  - supports on-the-fly display and calculation of band combinations
  - uses [**`remotepixel-api`**](https://github.com/RemotePixel/remotepixel-api) (based on AWS Lambda)

## Processing

- [**`SNAP` (Sentinel Application Plattform)**](http://step.esa.int/main/toolboxes/snap/)
  - (pre-)process any Sentinel data
  - also available as [docker](https://github.com/edwardpmorris/docker-snap)
- [**`ARCSI` (Atmospheric and Radiometric Correction of Satellite Imagery)**](https://www.arcsi.remotesensing.info/)
  - atmospheric correction of Sentinel-2 data
- [**Google Earth Engine**](https://earthengine.google.com/)
  - process the global Sentinel archives directly on Google's servers
- [**EOS Processing**](https://processing.eos.com/)
  - workflow library for thematic processing of (Sentinel-2) satellite data
- [**`iCOR`**](https://blog.vito.be/remotesensing/icor_available)
  - atmospheric correction of Sentinel-2 data
  - available as `SNAP` plugin
- [**`MAJA` (MACCS ATCOR Joint Algorithm)** ](https://logiciels.cnes.fr/en/content/maja)
  - atmospheric correction of Sentinel-2 data using time series
  - used for [Theia](https://theia.cnes.fr/atdistrib/rocket/#/search?collection=SENTINEL2) and [`Sen2-Agri`](https://github.com/Sen2Agri/Sen2Agri-System)
- [**`Sen2-Agri`**](https://github.com/Sen2Agri/Sen2Agri-System)
  - toolbox for processing images for agricultural purposes
  - includes modules for atmospheric correction, monthly syntheses, biophysical variables, crop mask, crop-type classification and an [orchestrator](http://www.esa-sen2agri.org/operational-system/system-description/)
- [**`s2cloudless`**](https://github.com/sentinel-hub/sentinel2-cloud-detector)
  - single scene, pixel-based cloud detection algorithm used at [Sentinel-Hub](https://www.sentinel-hub.com/)
  - [accompanying write-up](https://medium.com/sentinel-hub/improving-cloud-detection-with-machine-learning-c09dc5d7cf13) with performance comparison to other cloud detection algorithms
- [**`Sen2Cor`**](http://step.esa.int/main/third-party-plugins-2/sen2cor/)
  - atmospheric correction of Sentinel-2 data
  - basis for [L2A](https://sentinel.esa.int/web/sentinel/technical-guides/sentinel-2-msi/level-2a/algorithm) data published on Copernicus Open Access Hub
- [**`sen2r`**](https://github.com/ranghetti/sen2r)
  - R toolbox to search, download and pre-process Sentinel-2 data
- [**`ACOLITE`**](https://github.com/acolite/acolite)
  - atmospheric correction algorithms for aquatic applications of Landsat and Sentinel-2
- [**`C2RCC`**](https://github.com/bcdev/s3tbx-c2rcc)
  - atmospheric correction of Sentinel-3 and -2 for coast colour applications
  - included in the `SNAP` toolbox for Sentinel-3
- [**`i.sentinel.mask`**](https://grass.osgeo.org/grass7/manuals/addons/i.sentinel.mask.html)
  - GRASS GIS addon for atmospheric correction of Sentinel-2 including cloud and shadow detection
- [**`sat-stac-sentinel`**](https://github.com/sat-utils/sat-stac-sentinel)
  - convert original Sentinel-1 and -2 metadata into [STAC](https://stacspec.org/) items
- [**`EOReader`**](https://github.com/sertit/eoreader)
  - Opensource Python library reading Sentinel-1, 2, 3, and other optical and SAR sensors - loading and stacking bands in a sensor-agnostic way
- [**`xsar`**](https://github.com/umr-lops/xsar)
  -  read Sentinel-1 data into xarray for further processing
- [**`FORCE Processing Framework`**](https://github.com/davidfrantz/force)
  - Generate analysis ready data for Sentinel-2 and Landsat-4/5/7/8/9 (including atmospheric correction and homogenization of Sentinel-2 and Landsat data)

## Key Resources

| Resource | Link |
|----------|------|
| Copernicus Sentinel Satellites | [http://www.copernicus.eu/main/sentinels](http://www.copernicus.eu/main/sentinels) |
| Collaborative Ground Segment members | [https://sentinels.copernicus.eu/web/sentinel/missions/collaborative/national-points-of-contact](https://sentinels.copernicus.eu/web/sentinel/missions/collaborative/national-points-of-contact) |
| **Copernicus Data Spaces Ecosystem (CDSE)** | [https://dataspace.copernicus.eu/](https://dataspace.copernicus.eu/) |
| **Australia National Mirror** | [https://copernicus.nci.org.au/](https://copernicus.nci.org.au/) |
| **Austria National Mirror** | [https://data.sentinel.zamg.ac.at/](https://data.sentinel.zamg.ac.at/) |
| **Czech Rebublic National Mirror** | [https://dhr1.cesnet.cz/#/home](https://dhr1.cesnet.cz/#/home) |
| **Estonia National Mirror** | [https://geoportaal.maaamet.ee/eng/Spatial-Data/National-Satellite-Data-Centre-ESTHub-p654.html](https://geoportaal.maaamet.ee/eng/Spatial-Data/National-Satellite-Data-Centre-ESTHub-p654.html) |
| **Finland National Mirror** | [https://finhub.nsdc.fmi.fi/](https://finhub.nsdc.fmi.fi/) |
| **France National Mirror (PEPS)** | [https://peps.cnes.fr/rocket/](https://peps.cnes.fr/rocket/) |
| **Germany National Mirror (CODE-DE)** | [https://code-de.org/](https://code-de.org/) |
| **Greece National Mirror** | [https://sentinels.space.noa.gr/](https://sentinels.space.noa.gr/) |
| **Luxembourg National Mirror** | [https://www.collgs.lu/](https://www.collgs.lu/) |
| **Norway National Mirror** | [https://colhub.met.no/#/home](https://colhub.met.no/#/home) |
| **Portugal National Mirror** | [https://ipsentinel.ipma.pt/dhus/#/home](https://ipsentinel.ipma.pt/dhus/#/home) |
| **United Kingdom National Mirror (SEDAS)** | [http://sedas.satapps.org/](http://sedas.satapps.org/) |
| **Alaska Satellite Facility (Sentinel-1)** | [https://www.asf.alaska.edu/sentinel/](https://www.asf.alaska.edu/sentinel/) |
| **Centre for Environmental Data Analysis - CEDA (Sentinel-1, -2)** | [http://catalogue.ceda.ac.uk/search/?search_term=sentinel&return_obj=ob&search_obj=ob](http://catalogue.ceda.ac.uk/search/?search_term=sentinel&return_obj=ob&search_obj=ob) |
| **Theia (Sentinel-2)** | [https://theia.cnes.fr/atdistrib/rocket/#/search?collection=SENTINEL2](https://theia.cnes.fr/atdistrib/rocket/#/search?collection=SENTINEL2) |
| areas proposed by scientists | [http://www.cesbio.ups-tlse.fr/multitemp/?page_id=7501](http://www.cesbio.ups-tlse.fr/multitemp/?page_id=7501) |
| **USGS EarthExplorer (Sentinel-2)** | [https://earthexplorer.usgs.gov/](https://earthexplorer.usgs.gov/) |
| **EUMETSAT CODA (Sentinel-3 Marine Products)** | [https://coda.eumetsat.int/#/home](https://coda.eumetsat.int/#/home) |
| **DLR Geoservice (Sentinel-2)** | [https://geoservice.dlr.de/web/](https://geoservice.dlr.de/web/) |
| Download | [https://download.geoservice.dlr.de/S2_L2A_MAJA/files/](https://download.geoservice.dlr.de/S2_L2A_MAJA/files/) |
| **NOAA CoastWatch** | [https://coastwatch.noaa.gov/](https://coastwatch.noaa.gov/) |
| **NASA Earthdata** | [https://search.earthdata.nasa.gov/](https://search.earthdata.nasa.gov/) |
| **Open data on AWS** | [https://registry.opendata.aws/tag/satellite-imagery/](https://registry.opendata.aws/tag/satellite-imagery/) |
| Sentinel-2 L1C and L2A | [https://registry.opendata.aws/sentinel-2/](https://registry.opendata.aws/sentinel-2/) |
| Sentinel-2 L2A Cloud-Optimized GeoTIFFs | [https://registry.opendata.aws/sentinel-2-l2a-cogs/](https://registry.opendata.aws/sentinel-2-l2a-cogs/) |
| STAC Browser | [https://sentinel.stac.cloud/?t=catalogs](https://sentinel.stac.cloud/?t=catalogs) |
| Sentinel-1 GRD | [https://registry.opendata.aws/sentinel-1/](https://registry.opendata.aws/sentinel-1/) |



---

## 来源：security.md

## 简介

本指南提供了一份全面的安全清单，用于保护个人数字资产。基于 Personal Security Checklist 项目，涵盖了个人必备的安全实践。

### 为什么安全很重要

| 威胁 | 影响 | 预防措施 |
|------|------|----------|
| 身份盗窃 | 经济损失 | 强身份验证 |
| 数据泄露 | 隐私暴露 | 加密 |
| 恶意软件 | 系统被入侵 | 软件更新 |
| 钓鱼攻击 | 凭据被盗 | 安全意识培训 |

### 安全层级

| 层级 | 保护 |
|------|------|
| 物理层 | 设备安全 |
| 网络层 | 连接安全 |
| 应用层 | 软件安全 |
| 数据层 | 信息安全 |

## 身份验证

### 密码安全

| 实践 | 描述 |
|------|------|
| 使用唯一密码 | 每个账户使用不同密码 |
| 长密码 | 至少 12 个字符 |
| 密码管理器 | 安全存储密码 |
| 避免个人信息 | 不使用姓名、生日等 |

### 密码管理器推荐

| 管理器 | 平台 | 特性 |
|--------|------|------|
| Bitwarden | 跨平台 | 开源，免费层级 |
| 1Password | 跨平台 | 家庭共享 |
| KeePass | 本地 | 离线，开源 |
| LastPass | 跨平台 | 浏览器集成 |

### 双因素认证

| 方法 | 安全级别 | 便捷性 |
|------|----------|--------|
| 短信验证码 | 低 | 高 |
| 认证器应用 | 中 | 中 |
| 硬件密钥 | 高 | 低 |
| Passkeys | 高 | 高 |

### 2FA 应用推荐

| 应用 | 平台 | 特性 |
|------|------|------|
| Aegis | Android | 开源，加密 |
| Raivo OTP | iOS | iCloud 同步 |
| Authy | 跨平台 | 多设备 |
| EntAuth | 跨平台 | 硬件令牌支持 |

## 设备安全

### 操作系统

| 设置 | Windows | macOS | Linux |
|------|---------|-------|-------|
| 全盘加密 | BitLocker | FileVault | LUKS |
| 防火墙 | 内置 | 内置 | ufw/iptables |
| 自动更新 | 启用 | 启用 | 配置 |
| 杀毒软件 | Defender | XProtect | ClamAV |

### 移动设备

| 设置 | iOS | Android |
|------|-----|---------|
| 锁屏 | 强密码 | PIN + 生物识别 |
| 加密 | 自动 | 非默认时手动启用 |
| 应用权限 | 定期审查 | 定期审查 |
| 远程擦除 | 查找我的 | 查找我的设备 |

### 物理安全

| 实践 | 描述 |
|------|------|
| 锁定设备 | 使用屏幕锁 |
| 安全存放 | 离开时锁定设备 |
| USB 谨慎 | 避免未知 USB 设备 |
| 摄像头遮挡 | 不使用时遮挡摄像头 |

## 网络安全

### 家庭网络

| 设置 | 建议 |
|------|------|
| 路由器密码 | 更改默认密码 |
| WiFi 密码 | 使用强 WPA3/WPA2 |
| 网络名称 | 避免个人信息 |
| 固件 | 定期更新 |
| 访客网络 | 隔离访客设备 |

### 公共 WiFi

| 风险 | 缓解措施 |
|------|----------|
| 中间人攻击 | 使用 VPN |
| 数据包嗅探 | 仅使用 HTTPS |
| 邪恶双子 | 验证网络名称 |
| 会话劫持 | 避免敏感操作 |

### VPN 选择

| 标准 | 注意事项 |
|------|----------|
| 无日志策略 | 经过审计验证 |
| 协议 | WireGuard、OpenVPN |
| 管辖权 | 隐私友好国家 |
| 速度 | 影响最小 |
| 断路器 | 防止数据泄露 |

## 邮件安全

### 邮件最佳实践

| 实践 | 描述 |
|------|------|
| 分离账户 | 个人、工作、临时 |
| 别名服务 | 隐藏真实邮箱 |
| 钓鱼意识 | 验证发件人和链接 |
| 加密 | 敏感邮件使用 PGP |

### 邮件别名服务

| 服务 | 特性 |
|------|------|
| SimpleLogin | 开源，无限别名 |
| AnonAddy | 可自托管 |
| Firefox Relay | Mozilla 集成 |
| Apple Hide My Email | iCloud+ 功能 |

### 钓鱼特征

| 特征 | 示例 |
|------|------|
| 紧急语言 | "账户立即暂停" |
| URL 不匹配 | 显示与实际 URL 不同 |
| 通用称呼 | "亲爱的客户" |
| 可疑附件 | 意外的文件 |
| 语法错误 | 拼写和语法差 |

## 浏览器安全

### 浏览器设置

| 设置 | 建议 |
|------|------|
| 拦截跟踪器 | 启用跟踪保护 |
| HTTPS 模式 | 强制 HTTPS 连接 |
| Cookie 管理 | 拦截第三方 Cookie |
| 密码管理器 | 使用浏览器内置或外部 |
| 扩展程序 | 最少，仅信任的 |

### 推荐扩展

| 扩展 | 用途 |
|------|------|
| uBlock Origin | 广告和跟踪器拦截 |
| HTTPS Everywhere | 强制 HTTPS |
| Privacy Badger | 跟踪器拦截 |
| NoScript | JavaScript 控制 |

### 安全浏览器

| 浏览器 | 专注 |
|--------|------|
| Firefox | 隐私，开源 |
| Brave | 内置广告拦截 |
| Tor Browser | 最大匿名性 |
| Mullvad Browser | 隐私优先 |

## 数据保护

### 加密

| 工具 | 用例 |
|------|------|
| VeraCrypt | 磁盘加密 |
| GPG | 文件和邮件加密 |
| Signal | 消息加密 |
| Cryptomator | 云存储加密 |

### 备份策略

| 组件 | 建议 |
|------|------|
| 频率 | 定期自动备份 |
| 位置 | 多个位置 |
| 加密 | 加密备份 |
| 测试 | 验证备份完整性 |

### 3-2-1 备份规则

| 规则 | 含义 |
|------|------|
| 3 份 | 备份总数 |
| 2 种介质 | 不同存储类型 |
| 1 份异地 | 远程备份位置 |

## 隐私

### 社交媒体

| 设置 | 建议 |
|------|------|
| 资料可见性 | 仅好友 |
| 位置共享 | 关闭 |
| 标签审查 | 需要批准 |
| 应用权限 | 最小化访问 |

### 数据最小化

| 实践 | 描述 |
|------|------|
| 限制分享 | 仅必要信息 |
| 阅读政策 | 了解数据用途 |
| 选择退出 | 行使隐私权利 |
| 删除账户 | 移除未使用的账户 |

### 隐私工具

| 工具 | 用途 |
|------|------|
| DuckDuckGo | 私密搜索 |
| Signal | 私密通讯 |
| ProtonMail | 加密邮件 |
| Tor Browser | 匿名浏览 |

## 软件安全

### 更新实践

| 软件 | 更新频率 |
|------|----------|
| 操作系统 | 自动 |
| 浏览器 | 自动 |
| 杀毒软件 | 每日定义更新 |
| 应用程序 | 可用时更新 |

### 下载安全

| 来源 | 信任级别 |
|------|----------|
| 官方网站 | 高 |
| 应用商店 | 中高 |
| 第三方网站 | 低 |
| 未知来源 | 非常低 |

### 软件推荐

| 类别 | 推荐 |
|------|------|
| 杀毒软件 | Windows Defender、ClamAV |
| 防火墙 | 系统内置防火墙 |
| 密码管理器 | Bitwarden、KeePass |
| VPN | Mullvad、ProtonVPN |

## 事件响应

### 如果被入侵

| 步骤 | 操作 |
|------|------|
| 1 | 立即更改密码 |
| 2 | 在所有账户启用 2FA |
| 3 | 检查未授权访问 |
| 4 | 监控财务账户 |
| 5 | 向相关机构报告 |

### 账户恢复

| 账户类型 | 恢复方式 |
|----------|----------|
| 邮箱 | 恢复邮箱、手机 |
| 银行 | 携带证件到网点 |
| 社交媒体 | 账户恢复流程 |
| 云存储 | 恢复密钥 |

## 安全审计清单

### 月度审查

| 任务 | 状态 |
|------|------|
| 审查账户活动 | |
| 检查数据泄露 | |
| 按需更新密码 | |
| 审查应用权限 | |
| 备份重要数据 | |

### 年度审查

| 任务 | 状态 |
|------|------|
| 全面安全审计 | |
| 更新恢复信息 | |
| 审查隐私设置 | |
| 测试备份恢复 | |
| 更新紧急联系人 | |

## 总结

| 类别 | 关键操作 |
|------|----------|
| 身份验证 | 强密码、2FA |
| 设备 | 加密、更新 |
| 网络 | VPN、安全 WiFi |
| 邮件 | 别名、钓鱼意识 |
| 隐私 | 最小化数据分享 |


---

## 来源：firewall.md

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


---

## 来源：vpn.md

## 简介

SoftEther VPN 是由筑波大学开发的开源、跨平台 VPN 服务器和客户端软件。它支持多种 VPN 协议，提供高性能、灵活性和强大的安全功能。

| 特性 | 描述 |
|---------|-------------|
| 多协议 | 支持 SSL-VPN、L2TP、OpenVPN 和 WireGuard |
| 跨平台 | 支持 Windows、Linux、macOS 和 FreeBSD |
| 高性能 | 针对速度优化，支持 NAT 穿透 |
| 防火墙友好 | 可在防火墙和 NAT 设备后工作 |
| 免费开源 | Apache License 2.0 |

## 架构

### 支持的 VPN 协议

| 协议 | 端口 | 加密 | 备注 |
|----------|------|------------|-------|
| SSL-VPN (HTTPS) | 443 | AES-256、RSA | 内置协议，防火墙友好 |
| L2TP/IPsec | 500、4500 | IPsec ESP | 兼容原生操作系统客户端 |
| OpenVPN | 1194 | OpenSSL | 广泛使用的开源协议 |
| SSTP | 443 | TLS | Windows 原生支持 |
| WireGuard | 51820 | ChaCha20 | 现代轻量级协议 |

### 服务器模式

| 模式 | 描述 | 使用场景 |
|------|-------------|----------|
| VPN Server | 接受来自 VPN 客户端的连接 | 主要服务器部署 |
| VPN Bridge | 通过 VPN 隧道连接网络 | 站点间组网 |
| VPN Client | 连接到 VPN 服务器 | 终端用户访问 |

## 安装

### Linux 安装

```bash
# 下载 SoftEther VPN Server
wget https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.41-9787-beta/softether-vpnserver-v4.41-9787-beta-2022.04.26-linux-x64-64bit.tar.gz

# 解压
tar -xzf softether-vpnserver-*.tar.gz
cd vpnserver

# 编译（Linux 上需要）
make

# 启动服务器
./vpnserver start
```

### Docker 部署

```bash
docker run -d \
  --name=softether-vpn \
  --cap-add=NET_ADMIN \
  -p 443:443 \
  -p 992:992 \
  -p 5555:5555 \
  -p 500:500/udp \
  -p 4500:4500/udp \
  -p 1194:1194/udp \
  -v ./vpn_server.config:/usr/local/vpnserver/vpn_server.config \
  --restart unless-stopped \
  siomiz/softethervpn
```

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|-----------|---------|-------------|
| CPU | 1 核 | 2+ 核 |
| 内存 | 256 MB | 1 GB+ |
| 网络 | 100 Mbps | 1 Gbps+ |
| 操作系统 | Linux、Windows、macOS | Ubuntu 20.04+ 或 Windows Server 2019+ |

## 初始配置

### 服务器管理器设置

| 步骤 | 操作 |
|------|--------|
| 1 | 启动 SoftEther VPN Server Manager（GUI 或 CLI） |
| 2 | 连接到 localhost:443 或使用 ServerAdminPassword |
| 3 | 设置管理员密码 |
| 4 | 配置虚拟 Hub（默认：DEFAULT） |
| 5 | 启用所需的 VPN 协议 |

### 虚拟 Hub 配置

| 设置 | 描述 |
|---------|-------------|
| Hub 名称 | 虚拟网络的标识符 |
| 密码 | Hub 管理密码 |
| 最大会话数 | 最大并发连接数 |
| 在线/离线 | 启用或禁用 Hub |

### 网络设置

| 设置 | 描述 |
|---------|-------------|
| 本地网桥 | 将 Hub 连接到物理网络适配器 |
| SecureNAT | 虚拟 NAT 和 DHCP 服务器 |
| 级联连接 | 连接到另一个 VPN 服务器 |

## 用户管理

### 用户类型

| 类型 | 描述 |
|------|-------------|
| 个人用户 | 具有凭证的特定用户账户 |
| 用户组 | 具有共享设置的用户集合 |
| 匿名 | 未认证的访问（有限使用） |

### 认证方式

| 方式 | 描述 |
|--------|-------------|
| 密码 | 用户名和密码认证 |
| 证书 | 基于 X.509 证书的认证 |
| RADIUS | 外部 RADIUS 服务器认证 |
| NT Domain | Windows 域认证 |
| LDAP | 目录服务认证 |

### 创建用户

```bash
# 使用 vpncmd
./vpncmd localhost /SERVER /CMD UserCreate username /GROUP:none /REALNAME:"User Name" /NOTE:""
./vpncmd localhost /SERVER /CMD UserPasswordSet username /PASSWORD:strongpassword
```

### 用户权限

| 权限 | 描述 |
|-----------|-------------|
| 无限制带宽 | 不限制流量 |
| 最大带宽 | 限制上传/下载速度 |
| 最大会话数 | 限制并发连接 |
| 时间限制 | 指定时长后断开连接 |
| IP 限制 | 仅允许来自特定 IP 的连接 |

## VPN 协议配置

### SSL-VPN 设置

| 设置 | 值 |
|---------|-------|
| 端口 | 443 (HTTPS) |
| 证书 | 服务器 SSL 证书 |
| 加密 | AES-256-GCM |
| 客户端 | SoftEther VPN Client 或 SSTP |

### L2TP/IPsec 设置

| 设置 | 值 |
|---------|-------|
| 端口 | 500 (IKE)、4500 (NAT-T) |
| 预共享密钥 | IPsec 预共享密钥 |
| 加密 | AES-256 配合 SHA-256 |
| 客户端 | 原生操作系统 VPN 客户端 |

### OpenVPN 兼容性

| 设置 | 值 |
|---------|-------|
| 端口 | 1194 (UDP) |
| 协议 | UDP 或 TCP |
| 加密 | AES-256-CBC |
| 客户端 | 使用导出配置的 OpenVPN 客户端 |

## SecureNAT

### SecureNAT 功能

| 功能 | 描述 |
|---------|-------------|
| 虚拟 NAT | VPN 客户端的 NAT 转换 |
| 虚拟 DHCP | 自动 IP 地址分配 |
| DNS 中继 | VPN 客户端的 DNS 解析 |
| 无需驱动 | 无需管理员权限即可工作 |

### SecureNAT 配置

| 设置 | 描述 |
|---------|-------------|
| 虚拟 IP 范围 | 分配给客户端的 IP 地址（如 192.168.30.0/24） |
| NAT 网关 | NAT 的网关 IP（如 192.168.30.1） |
| DHCP 范围 | DHCP 地址池的起始和结束地址 |
| DNS 服务器 | VPN 客户端的 DNS 服务器 |
| 租约时间 | DHCP 租约时长 |

## 级联 VPN 连接

### 站点间 VPN

| 组件 | 位置 A | 位置 B |
|-----------|-----------|-----------|
| 服务器 | 带 Hub 的 VPN Server | 带 Hub 的 VPN Server |
| 网桥 | 到局域网的本地网桥 | 到局域网的本地网桥 |
| 级联 | 连接到远程 Hub | 接受级联连接 |

### 配置步骤

| 步骤 | 操作 |
|------|--------|
| 1 | 在两台服务器上创建匹配的用户账户 |
| 2 | 在服务器 A 上创建到服务器 B 的级联连接 |
| 3 | 在两台服务器上配置本地网桥 |
| 4 | 如需要则启用 IP 路由 |
| 5 | 测试局域网之间的连通性 |

## 安全

### 加密选项

| 算法 | 密钥长度 | 使用场景 |
|-----------|----------|----------|
| AES | 128、192、256 位 | 主要加密标准 |
| Camellia | 128、192、256 位 | AES 的替代方案 |
| RSA | 2048、4096 位 | 密钥交换和证书 |
| SHA | 256、384、512 位 | 哈希和完整性 |

### 安全最佳实践

| 实践 | 描述 |
|----------|-------------|
| 强密码 | 为管理员和用户账户使用复杂密码 |
| 证书认证 | 尽可能使用证书替代密码 |
| 禁用未使用协议 | 仅启用需要的协议 |
| IP 限制 | 将管理员访问限制在特定 IP 地址 |
| 日志记录 | 启用全面的日志记录 |
| 更新 | 保持服务器软件更新 |

## 监控和日志

### 日志类型

| 日志 | 内容 |
|-----|---------|
| 安全日志 | 认证事件、访问尝试 |
| 服务器日志 | 服务器启动/停止、配置更改 |
| 连接日志 | VPN 会话的建立和终止 |
| 数据包日志 | 网络流量捕获 |

### 监控指标

| 指标 | 描述 |
|--------|-------------|
| 活跃会话 | 当前连接的客户端数量 |
| 吞吐量 | 每秒的网络流量（字节） |
| 总流量 | 累计传输数据量 |
| 会话时长 | 每个客户端的连接时间 |

## 客户端配置

### 原生客户端设置

| 设置 | L2TP/IPsec | OpenVPN |
|---------|-----------|---------|
| 服务器地址 | VPN 服务器 IP 或主机名 | VPN 服务器 IP 或主机名 |
| 端口 | 默认（自动） | 1194 |
| 认证 | 预共享密钥 + 用户凭证 | 证书 + 用户凭证 |
| 协议 | UDP | UDP 或 TCP |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 连接被拒绝 | 服务器未运行或端口被阻止 | 启动服务器并检查防火墙 |
| 认证失败 | 凭证错误 | 验证用户名和密码 |
| VPN 无法上网 | NAT/路由配置错误 | 启用 SecureNAT 或配置路由 |
| 性能缓慢 | 加密开销或带宽限制 | 检查服务器资源和网络 |
| L2TP 无法连接 | IPsec 端口被阻止 | 打开 UDP 端口 500 和 4500 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 协议 | 支持 SSL-VPN、L2TP、OpenVPN、SSTP 和 WireGuard |
| 部署 | 在 Linux、Windows、macOS 上运行，支持 Docker |
| 用户 | 灵活的密码、证书和 LDAP 认证 |
| 网络 | SecureNAT 便于设置，本地网桥用于高级配置 |
| 安全 | AES-256 加密配合基于证书的认证 |
| 使用场景 | 远程访问、站点间和桥接组网 |


---
