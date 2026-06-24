# 自托管软件目录

## 目录

- [文件同步与共享](#文件同步与共享)
- [媒体管理](#媒体管理)
- [通讯](#通讯)
- [办公与效率](#办公与效率)
- [财务与记账](#财务与记账)
- [自动化](#自动化)
- [监控](#监控)
- [备份](#备份)
- [内容管理系统](#内容管理系统)
- [电商](#电商)
- [数据分析](#数据分析)
- [书签与稍后阅读](#书签与稍后阅读)
- [密码管理器](#密码管理器)
- [VPN](#vpn)
- [DNS](#dns)
- [邮件](#邮件)

---

## 文件同步与共享

跨设备同步文件和与他人共享的工具。

| 软件 | 说明 | 语言 | 许可证 |
|----------|-------------|----------|---------|
| Nextcloud | 功能齐全的云平台，支持文件同步、日历、通讯录 | PHP | AGPL-3.0 |
| Seafile | 高性能文件同步和共享平台 | Python/C | AGPL-3.0 |
| Syncthing | 设备间持续文件同步 | Go | MPL-2.0 |
| MinIO | S3 兼容对象存储 | Go | AGPL-3.0 |
| Filebrowser | 基于 Web 的文件管理器 | Go | Apache-2.0 |
| Sharry | 文件共享 Web 应用 | Scala | GPL-3.0 |
| Projectsend | 面向客户和团队的文件共享 | PHP | GPL-2.0 |
| Lufi | 加密文件共享 | Perl | AGPL-3.0 |

### 对比

| 功能 | Nextcloud | Seafile | Syncthing |
|---------|-----------|---------|-----------|
| 文件同步 | 是 | 是 | 是 |
| 日历 | 是 | 否 | 否 |
| 通讯录 | 是 | 否 | 否 |
| 移动应用 | 是 | 是 | 是 |
| 端到端加密 | 是 | 是 | 是 |
| 协同编辑 | 是 | 否 | 否 |
| 插件生态 | 丰富 | 有限 | 无 |
| 资源占用 | 高 | 中 | 低 |

---

## 媒体管理

### 媒体服务器

| 软件 | 说明 | 支持的媒体 |
|----------|-------------|-----------------|
| Jellyfin | 免费媒体服务器，无付费功能 | 视频、音频、照片 |
| Emby | 带高级功能的媒体服务器 | 视频、音频、照片 |
| Plex | 流行的媒体服务器，有免费层级 | 视频、音频、照片 |
| Navidrome | 兼容 Subsonic API 的音乐流媒体服务器 | 音频 |
| Audiobookshelf | 有声书和播客服务器 | 音频、播客 |
| Kavita | 漫画和图书数字图书馆 | 漫画、图书 |

### 媒体自动化

| 软件 | 用途 |
|----------|---------|
| Sonarr | 电视剧管理和下载 |
| Radarr | 电影管理和下载 |
| Lidarr | 音乐管理和下载 |
| Readarr | 书籍管理和下载 |
| Bazarr | 字幕管理 |
| Prowlarr | *arr 应用的索引器管理 |
| Overseerr | 媒体请求管理 |
| Jellyseerr | Jellyfin 的媒体请求管理 |

### 媒体播放器和流媒体

| 软件 | 说明 | 平台 |
|----------|-------------|----------|
| Streama | 带 Web 播放器的流媒体服务器 | Web |
| Owncast | 直播服务器 | Web |
| PeerTube | 去中心化视频平台 | Web |
| Koel | 音乐流媒体服务器 | Web |
| Funkwhale | 去中心化音乐平台 | Web |

---

## 通讯

### 聊天和即时通讯

| 软件 | 说明 | 协议 |
|----------|-------------|----------|
| Matrix (Synapse/Conduit) | 去中心化通讯协议 | Matrix |
| Rocket.Chat | 团队通讯平台 | 自定义 |
| Mattermost | 开源 Slack 替代品 | 自定义 |
| Zulip | 线程式团队聊天 | 自定义 |
| Element | Matrix 客户端，支持 Web、桌面、移动端 | Matrix |
| Mumble | 低延迟语音聊天 | 自定义 |
| Jitsi Meet | 视频会议 | WebRTC |

### 邮件服务器

| 软件 | 说明 |
|----------|-------------|
| Mailcow | Docker 化的邮件服务器套件 |
| Mailu | Docker 化的邮件服务器 |
| iRedMail | 即用型邮件服务器方案 |
| Postfix/Dovecot | 传统邮件服务器架构 |
| Maddy | Go 编写的可组合邮件服务器 |
| Stalwart | Rust 编写的现代邮件服务器 |

### 论坛和社区

| 软件 | 说明 |
|----------|-------------|
| Discourse | 现代论坛平台 |
| Flarum | 轻量级论坛软件 |
| NodeBB | 基于 Node.js 的实时论坛 |
| Lemmy | 联邦式链接聚合器（Reddit 替代品） |
| Kbin | 联邦式内容聚合器 |

---

## 办公与效率

### 文档编辑

| 软件 | 说明 | 格式支持 |
|----------|-------------|----------------|
| CryptPad | 端到端加密协作 | 文档、表格、演示文稿 |
| Etherpad | 实时协同文本编辑器 | 富文本 |
| OnlyOffice | 带文档编辑器的办公套件 | MS Office 格式 |
| Collabora Online | 基于 LibreOffice 的在线办公 | 所有格式 |

### 项目管理

| 软件 | 说明 |
|----------|-------------|
| Wekan | 看板（Trello 替代品） |
| Vikunja | 任务和项目管理 |
| Focalboard | 项目管理（Notion 替代品） |
| Taiga | 敏捷项目管理 |
| OpenProject | 带甘特图的项目管理 |
| Leantime | 面向非项目经理的项目管理 |
| Plane | 项目追踪（Jira 替代品） |

### 笔记

| 软件 | 说明 |
|----------|-------------|
| Outline | 团队 Wiki 和知识库 |
| BookStack | Wiki 和文档平台 |
| Wiki.js | 现代 Wiki 引擎 |
| Joplin Server | Joplin 应用的笔记同步服务器 |
| Trilium Notes | 层级式笔记应用 |
| SiYuan | 本地优先的知识管理 |
| Memos | 微博式笔记 |
| Affine | 带文档、Wiki、白板的知识库 |

### 群件

| 软件 | 说明 |
|----------|-------------|
| Nextcloud | 文件、日历、通讯录等 |
| Radicale | CalDAV 和 CardDAV 服务器 |
| Baikal | 轻量级 CalDAV/CardDAV 服务器 |
| EteSync | 加密日历和通讯录同步 |

---

## 财务与记账

### 个人财务

| 软件 | 说明 |
|----------|-------------|
| Firefly III | 个人财务管理器 |
| Actual Budget | 带同步的预算管理 |
| GnuCash | 复式记账 |
| Homebank | 个人记账 |
| Beancount | 纯文本记账 |
| hledger | 纯文本记账 |

### 发票和商业

| 软件 | 说明 |
|----------|-------------|
| Invoice Ninja | 发票和账单 |
| Akaunting | 在线会计软件 |
| InvoicePlane | 发票应用 |
| Kill Bill | 账单和支付平台 |
| Bigcapital | 财务会计 |

### 加密货币

| 软件 | 说明 |
|----------|-------------|
| BTCPay Server | Bitcoin 支付处理器 |
| LNbits | Lightning Network 钱包系统 |
| Electrum Server | Bitcoin Electrum 服务器 |
| Monero Node | Monero 加密货币节点 |

---

## 自动化

### 家庭自动化

| 软件 | 说明 |
|----------|-------------|
| Home Assistant | 家庭自动化平台 |
| openHAB | 带规则引擎的家庭自动化 |
| Domoticz | 家庭自动化系统 |
| Node-RED | 基于流程的自动化工具 |

### 工作流自动化

| 软件 | 说明 |
|----------|-------------|
| n8n | 工作流自动化（Zapier 替代品） |
| Activepieces | 业务自动化 |
| Huginn | 构建代理为你执行操作 |
| Automatisch | 业务自动化（Zapier 替代品） |
| Windmill | 脚本和流程的开发者平台 |

### 下载自动化

| 软件 | 说明 |
|----------|-------------|
| yt-dlp | 视频下载器 |
| gallery-dl | 图库下载器 |
| aria2 | 多协议下载工具 |
| SABnzbd | Usenet 下载器 |
| Transmission | BitTorrent 客户端 |
| qBittorrent | 带 Web UI 的 BitTorrent 客户端 |

---

## 监控

### 基础设施监控

| 软件 | 说明 |
|----------|-------------|
| Prometheus | 指标收集和告警 |
| Grafana | 可视化和仪表盘 |
| Netdata | 实时性能监控 |
| Zabbix | 企业级监控方案 |
| LibreNMS | 网络监控 |
| Uptime Kuma | 可用性监控 |

### 日志管理

| 软件 | 说明 |
|----------|-------------|
| Graylog | 日志管理平台 |
| Loki | 日志聚合（类似 Prometheus 的日志版） |
| Elasticsearch + Kibana | 搜索和可视化 |
| SigNoz | OpenTelemetry 原生可观测性 |

### 可用性监控

| 软件 | 说明 |
|----------|-------------|
| Uptime Kuma | 精美的可用性监控 |
| Gatus | 健康仪表盘 |
| Statping | 状态页面和监控 |
| cState | 静态状态页面 |

---

## 备份

### 备份方案

| 软件 | 说明 |
|----------|-------------|
| Restic | 快速、安全的备份程序 |
| BorgBackup | 去重备份程序 |
| Duplicati | 加密备份到云存储 |
| Kopia | 跨平台备份工具 |
| UrBackup | 客户端/服务器备份系统 |
| Backrest | Restic 的 Web UI |

### 备份策略

| 策略 | 说明 | 用途 |
|----------|-------------|----------|
| 3-2-1 法则 | 3 份副本、2 种介质、1 份异地 | 通用最佳实践 |
| 祖-父-子 | 轮换备份方案 | 长期保留 |
| 增量备份 | 仅备份上次后变更的文件 | 节省存储 |
| 差异备份 | 备份上次全量后变更的文件 | 恢复更快 |

---

## 内容管理系统

### 传统 CMS

| 软件 | 说明 | 语言 |
|----------|-------------|----------|
| WordPress | 最流行的 CMS | PHP |
| Ghost | 发布平台 | Node.js |
| Strapi | Headless CMS | Node.js |
| Directus | Headless CMS | Node.js |
| KeystoneJS | Headless CMS | Node.js |
| Payload | Headless CMS | TypeScript |

### 静态站点生成器

| 软件 | 说明 |
|----------|-------------|
| Hugo | 快速的静态站点生成器 |
| Jekyll | 博客导向的静态站点生成器 |
| Gatsby | 基于 React 的静态站点生成器 |
| Next.js | 支持 SSG/SSR 的 React 框架 |
| Astro | 内容优先的 Web 框架 |
| Pelican | Python 静态站点生成器 |

### Wiki 平台

| 软件 | 说明 |
|----------|-------------|
| Wiki.js | 现代 Wiki 引擎 |
| BookStack | Wiki 和文档 |
| DokuWiki | 无需数据库的简单 Wiki |
| TiddlyWiki | 个人非线性笔记本 |
| Gollum | Git 驱动的 Wiki |

---

## 电商

### 在线商店平台

| 软件 | 说明 |
|----------|-------------|
| WooCommerce | WordPress 电商插件 |
| PrestaShop | 功能齐全的电商平台 |
| Magento Open Source | 企业级电商 |
| Saleor | GraphQL 优先的电商 |
| Medusa | Headless 电商 |
| Bagisto | 基于 Laravel 的电商 |
| Sylius | 基于 Symfony 的电商 |

### 库存管理

| 软件 | 说明 |
|----------|-------------|
| Inventree | 库存管理系统 |
| Part-DB | 电子元件数据库 |
| Snipe-IT | IT 资产管理 |

---

## 数据分析

### Web 分析

| 软件 | 说明 | 隐私保护 |
|----------|-------------|---------------|
| Plausible | 简单、隐私友好的分析 | 高 |
| Umami | 简单、快速、注重隐私 | 高 |
| Matomo | 功能齐全的分析（GA 替代品） | 中 |
| PostHog | 产品分析 | 中 |
| GoAccess | 实时 Web 日志分析器 | 高 |
| Shynet | 隐私友好的分析 | 高 |

### 商业智能

| 软件 | 说明 |
|----------|-------------|
| Metabase | 商业智能和分析 |
| Redash | 查询和可视化数据 |
| Apache Superset | 数据探索和可视化 |
| Grafana | 可观测性和数据可视化 |

### 对比

| 功能 | Plausible | Umami | Matomo |
|---------|-----------|-------|--------|
| 无 Cookie | 是 | 是 | 可选 |
| 符合 GDPR | 是 | 是 | 是 |
| 仪表盘 | 简洁 | 简洁 | 复杂 |
| 实时 | 是 | 是 | 是 |
| 目标追踪 | 是 | 是 | 是 |
| API | 是 | 是 | 是 |

---

## 书签与稍后阅读

### 书签管理器

| 软件 | 说明 |
|----------|-------------|
| Linkding | 快速、极简的书签管理器 |
| Shiori | 简单的书签管理器 |
| Grimoire | 带标签的书签管理器 |
| Wallabag | 稍后阅读应用 |
| Linkace | 带自动归档的书签存档 |

### RSS 阅读器

| 软件 | 说明 |
|----------|-------------|
| Miniflux | 极简 RSS 阅读器 |
| FreshRSS | 自托管 RSS 聚合器 |
| Tiny Tiny RSS | 功能丰富的 RSS 阅读器 |
| NewsBlur | 社交 RSS 阅读器 |
| CommaFeed | 受 Google Reader 启发的 RSS 阅读器 |

---

## 密码管理器

| 软件 | 说明 | 同步 | 共享 |
|----------|-------------|------|---------|
| Vaultwarden | Bitwarden 兼容服务器 | 是 | 是 |
| Passbolt | 团队密码管理器 | 是 | 是 |
| KeePassXC | 本地密码管理器 | 手动 | 否 |
| Padloc | 现代密码管理器 | 是 | 是 |
| Teampass | 协作密码管理器 | 是 | 是 |

### 对比

| 功能 | Vaultwarden | Passbolt | KeePassXC |
|---------|-------------|----------|-----------|
| Web UI | 是 | 是 | 否 |
| 浏览器扩展 | 是 | 是 | 是 |
| 移动应用 | 是 | 是 | 是 |
| 共享 | 是 | 是 | 否 |
| 2FA | 是 | 是 | 是 |
| 自托管 | 是 | 是 | 不适用 |
| 资源占用 | 低 | 中 | 不适用 |

---

## VPN

### VPN 服务器

| 软件 | 说明 | 协议 |
|----------|-------------|----------|
| WireGuard | 现代、快速的 VPN | WireGuard |
| OpenVPN | 传统 VPN | OpenVPN |
| Headscale | 自托管 Tailscale 控制服务器 | WireGuard |
| Netmaker | 基于 WireGuard 的网络平台 | WireGuard |
| Firezone | VPN 和防火墙 | WireGuard |
| Pritunl | 企业级 VPN 服务器 | OpenVPN/WireGuard |

### VPN 对比

| 功能 | WireGuard | OpenVPN | Headscale |
|---------|-----------|---------|-----------|
| 速度 | 快 | 中等 | 快 |
| 配置 | 简单 | 复杂 | 简单 |
| 移动支持 | 是 | 是 | 是 |
| 防火墙穿透 | 好 | 优秀 | 好 |
| 代码量 | 小 | 大 | 小 |

### 零信任网络

| 软件 | 说明 |
|----------|-------------|
| Tailscale | 基于 WireGuard 的 Mesh VPN |
| Netbird | 基于 WireGuard 的 Mesh 网络 |
| ZeroTier | 全球虚拟网络 |

---

## DNS

### DNS 服务器

| 软件 | 说明 |
|----------|-------------|
| Pi-hole | 用于广告拦截的 DNS 陷坑 |
| AdGuard Home | 全网广告拦截 |
| CoreDNS | Go 编写的 DNS 服务器 |
| Blocky | 带广告拦截的 DNS 代理 |
| Technitium DNS | 权威和递归 DNS |
| Unbound | 验证型 DNS 解析器 |
| BIND | 使用最广泛的 DNS 服务器 |

### 对比

| 功能 | Pi-hole | AdGuard Home | Blocky |
|---------|---------|--------------|--------|
| 广告拦截 | 是 | 是 | 是 |
| DNS over HTTPS | 是 | 是 | 是 |
| DNS over TLS | 是 | 是 | 是 |
| Web UI | 是 | 是 | 否 |
| DHCP 服务器 | 是 | 是 | 否 |
| 资源占用 | 低 | 低 | 极低 |

---

## 邮件

### 邮件服务器

| 软件 | 说明 |
|----------|-------------|
| Mailcow | Docker 化的邮件服务器套件 |
| Mailu | Docker 化的邮件服务器 |
| iRedMail | 即用型邮件服务器 |
| Maddy | 可组合的邮件服务器 |
| Stalwart | Rust 编写的现代邮件服务器 |

### 邮件客户端

| 软件 | 说明 |
|----------|-------------|
| Roundcube | 基于 Web 的邮件客户端 |
| SOGo | 带邮件的群件 |
| Cypht | 轻量级邮件客户端 |
| Snappymail | 现代 Web 邮件客户端 |

### 邮件安全

| 软件 | 说明 |
|----------|-------------|
| Rspamd | 垃圾邮件过滤系统 |
| Amavis | 邮件内容过滤器 |
| ClamAV | 邮件杀毒 |
| SpamAssassin | 垃圾邮件过滤 |

### 邮件对比

| 功能 | Mailcow | Mailu | iRedMail |
|---------|---------|-------|----------|
| Docker | 是 | 是 | 否 |
| Web UI | 是 | 是 | 是 |
| 垃圾邮件过滤 | Rspamd | Rspamd | Amavis |
| 日历 | 是 | 否 | 是 |
| 通讯录 | 是 | 否 | 是 |
| 安装难度 | 简单 | 简单 | 中等 |

---

## 选择自托管软件

### 决策因素

| 因素 | 需要考虑的问题 |
|--------|------------------|
| 资源需求 | 需要多少 RAM/CPU/存储？ |
| 维护 | 多久需要更新一次？ |
| 备份 | 备份和恢复有多容易？ |
| 社区 | 项目是否积极维护？ |
| 文档 | 是否有良好的文档？ |
| 安全 | 是否提供安全更新？ |
| 集成 | 是否能与其他工具配合？ |
| 许可证 | 许可证是否兼容你的用途？ |

### 最低服务器要求

| 软件类型 | RAM | CPU | 存储 |
|---------------|-----|-----|---------|
| 静态站点 | 256MB | 1 核 | 1GB |
| 博客/CMS | 512MB | 1 核 | 10GB |
| 文件同步 | 1GB | 2 核 | 50GB+ |
| 媒体服务器 | 2GB | 2 核 | 100GB+ |
| 邮件服务器 | 2GB | 2 核 | 20GB+ |
| 完整平台 | 4GB+ | 4 核 | 100GB+ |
