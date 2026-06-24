# macOS 应用程序完全指南

## 目录

1. [简介](#简介)
2. [编辑器与 IDE](#编辑器与-ide)
3. [终端与命令行](#终端与命令行)
4. [浏览器](#浏览器)
5. [设计工具](#设计工具)
6. [效率工具](#效率工具)
7. [实用工具](#实用工具)
8. [安全](#安全)
9. [通讯](#通讯)
10. [媒体](#媒体)
11. [开发工具](#开发工具)
12. [文件管理](#文件管理)
13. [系统工具](#系统工具)

---

## 简介

macOS 拥有丰富的应用程序生态系统，能满足各种需求。本指南涵盖了从开发工具到效率软件等各类别中最优秀的应用程序。

### 应用来源

| 来源 | 说明 | 可信度 |
|------|------|--------|
| Mac App Store | Apple 官方商店 | 高 |
| 开发者网站 | 直接下载 | 不定 |
| Homebrew | 包管理器 | 高 |
| Setapp | 订阅服务 | 高 |
| GitHub | 开源项目 | 不定 |

### 安装应用程序

**Mac App Store：**

```
1. 打开 App Store 应用
2. 搜索应用程序
3. 点击 "获取" 或价格按钮
4. 使用 Apple ID 验证
5. 等待下载和安装完成
```

**Homebrew：**

```bash
# Install Homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install applications
brew install --cask visual-studio-code
brew install --cask google-chrome
brew install --cask iterm2

# Search for applications
brew search <app-name>

# List installed
brew list --cask
```

---

## 编辑器与 IDE

### 文本编辑器

| 编辑器 | 价格 | 特点 | 适用场景 |
|--------|------|------|----------|
| Visual Studio Code | 免费 | 扩展、终端、调试 | 通用开发 |
| Sublime Text | $99 | 快速、轻量 | 快速编辑 |
| BBEdit | $49.99 | 文本处理、grep | 文本操作 |
| Nova | $99 | 原生、快速 | Mac 原生开发 |
| Atom | 免费 | 可定制、插件丰富 | 个性化定制 |
| Vim | 免费 | 模态编辑、终端 | 终端编辑 |
| Emacs | 免费 | 可扩展、功能强大 | 高级用户 |

### IDE（集成开发环境）

| IDE | 价格 | 语言 | 特点 |
|-----|------|------|------|
| Xcode | 免费 | Swift, Obj-C | iOS/macOS 开发 |
| IntelliJ IDEA | $149/年 | Java, Kotlin | 企业级 Java |
| PyCharm | $89/年 | Python | Python 开发 |
| WebStorm | $59/年 | JavaScript | Web 开发 |
| CLion | $89/年 | C/C++ | 系统编程 |
| Android Studio | 免费 | Kotlin, Java | Android 开发 |
| Visual Studio | 免费 | C#, .NET | .NET 开发 |

### VS Code 扩展

| 扩展 | 用途 |
|------|------|
| Python | Python 支持 |
| ESLint | JavaScript 代码检查 |
| Prettier | 代码格式化 |
| GitLens | Git 集成 |
| Remote SSH | 远程开发 |
| Docker | 容器支持 |
| Thunder Client | API 测试 |
| Live Server | 本地开发服务器 |

### 代码编辑器对比

| 特性 | VS Code | Sublime Text | Nova |
|------|---------|--------------|------|
| 价格 | 免费 | $99 | $99 |
| 速度 | 快 | 非常快 | 快 |
| 扩展 | 丰富 | 有限 | 良好 |
| 终端 | 内置 | 插件 | 内置 |
| Git | 内置 | 插件 | 内置 |
| 调试 | 内置 | 插件 | 内置 |
| Mac 原生 | 否 | 否 | 是 |

---

## 终端与命令行

### 终端模拟器

| 终端 | 价格 | 特点 | 适用场景 |
|------|------|------|----------|
| iTerm2 | 免费 | 分屏、搜索、配置文件 | 高级用户 |
| Alacritty | 免费 | GPU 加速、快速 | 追求速度 |
| Kitty | 免费 | GPU、图片、连字 | 现代功能 |
| Warp | 免费 | AI、代码块、现代化 | 现代工作流 |
| Hyper | 免费 | 基于 Electron、可定制 | 个性化定制 |
| Terminal.app | 免费 | 内置、简洁 | 基础使用 |

### iTerm2 功能

| 功能 | 说明 |
|------|------|
| 分屏 | 一个窗口中显示多个终端 |
| 搜索 | 在终端输出中查找文本 |
| 自动补全 | 命令建议 |
| 配置文件 | 不同的配置方案 |
| 触发器 | 自动化操作 |
| 广播 | 同时发送到多个面板 |
| 热键 | 快速访问 |
| 复制模式 | 选择和复制文本 |

### Shell 选项

| Shell | 特点 | 安装方式 |
|-------|------|----------|
| zsh | macOS 默认，支持插件 | 预装 |
| bash | 经典，广泛使用 | 预装 |
| fish | 用户友好，自动建议 | `brew install fish` |
| nushell | 结构化数据 | `brew install nushell` |

### Oh My Zsh

```bash
# Install Oh My Zsh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# Popular plugins
plugins=(
    git
    docker
    kubectl
    zsh-autosuggestions
    zsh-syntax-highlighting
    z
)

# Popular themes
ZSH_THEME="powerlevel10k/powerlevel10k"
```

### CLI 工具

| 工具 | 用途 | 安装方式 |
|------|------|----------|
| Homebrew | 包管理器 | `/bin/bash -c "$(curl..."` |
| git | 版本控制 | `xcode-select --install` |
| wget | 文件下载 | `brew install wget` |
| curl | HTTP 请求 | 预装 |
| jq | JSON 处理 | `brew install jq` |
| tree | 目录列表 | `brew install tree` |
| htop | 进程查看器 | `brew install htop` |
| ripgrep | 快速搜索 | `brew install ripgrep` |
| fd | 快速查找 | `brew install fd` |
| bat | 带语法高亮的 cat | `brew install bat` |
| exa | ls 替代品 | `brew install exa` |

---

## 浏览器

### 浏览器对比

| 浏览器 | 引擎 | 价格 | 特点 |
|--------|------|------|------|
| Safari | WebKit | 免费 | 原生、高效、Apple 生态集成 |
| Chrome | Blink | 免费 | 扩展丰富、Google 服务 |
| Firefox | Gecko | 免费 | 注重隐私、可定制 |
| Arc | Blink | 免费 | 现代 UI、工作区 |
| Brave | Blink | 免费 | 隐私保护、广告拦截 |
| Edge | Blink | 免费 | Microsoft 服务 |
| Vivaldi | Blink | 免费 | 高度定制、面向高级用户 |
| Orion | WebKit | 免费 | 原生、支持 Firefox/Chrome 扩展 |

### Safari 功能

| 功能 | 说明 |
|------|------|
| 阅读模式 | 无干扰阅读 |
| 标签页组 | 整理标签页 |
| 隐私报告 | 追踪器拦截统计 |
| 钥匙串 | 密码管理 |
| 接力 | 在其他设备上继续 |
| AirPlay | 投放到 Apple TV |
| Apple Pay | 安全支付 |

### Chrome 扩展

| 扩展 | 用途 |
|------|------|
| uBlock Origin | 广告拦截 |
| LastPass/1Password | 密码管理 |
| React DevTools | React 调试 |
| Wappalyzer | 技术检测 |
| JSON Viewer | JSON 格式化 |
| Momentum | 新标签页仪表盘 |
| Dark Reader | 全局深色模式 |

### Firefox 附加组件

| 附加组件 | 用途 |
|----------|------|
| uBlock Origin | 广告拦截 |
| Privacy Badger | 追踪器拦截 |
| Bitwarden | 密码管理 |
| Tree Style Tab | 垂直标签页 |
| Multi-Account Containers | 隔离会话 |

---

## 设计工具

### 图形设计

| 工具 | 价格 | 用途 | 适用场景 |
|------|------|------|----------|
| Figma | 免费/高级版 | UI/UX 设计 | Web、应用设计 |
| Sketch | $99/年 | UI 设计 | Mac 原生设计 |
| Adobe Creative Cloud | $54.99/月 | 全套工具 | 专业设计 |
| Affinity Designer | $69.99 | 矢量图形 | Illustrator 替代品 |
| Affinity Photo | $69.99 | 图片编辑 | Photoshop 替代品 |
| Canva | 免费/高级版 | 快速设计 | 非专业设计人员 |
| GIMP | 免费 | 图片编辑 | 开源方案 |

### 设计工具对比

| 特性 | Figma | Sketch | Adobe XD |
|------|-------|--------|----------|
| 价格 | 免费版 | $99/年 | 免费版 |
| 平台 | Web、Mac、Win | 仅 Mac | Mac、Win |
| 协作 | 实时 | 通过插件 | 实时 |
| 原型设计 | 内置 | 通过插件 | 内置 |
| 组件 | 支持 | 支持 | 支持 |
| 开发交付 | 内置 | 通过插件 | 内置 |

### 图标与素材工具

| 工具 | 价格 | 用途 |
|------|------|------|
| SF Symbols | 免费 | Apple 图标库 |
| Iconify | 免费 | 图标库 |
| Noun Project | 免费/高级版 | 图标集合 |
| Lottie | 免费 | 动画 |
| Figma Community | 免费 | 设计素材 |

### 颜色工具

| 工具 | 价格 | 用途 |
|------|------|------|
| Coolors | 免费/高级版 | 调色板 |
| Adobe Color | 免费 | 色轮 |
| Sip | $9.99 | 取色器 |
| ColorSlurp | 免费 | 取色器 |
| Realtime Colors | 免费 | 颜色预览 |

---

## 效率工具

### 任务管理

| 工具 | 价格 | 特点 | 适用场景 |
|------|------|------|----------|
| Things 3 | $49.99 | 界面美观、GTD | 个人任务 |
| Todoist | 免费/高级版 | 跨平台 | 团队任务 |
| OmniFocus | $49.99 | 功能强大、GTD | 高级用户 |
| TickTick | 免费/高级版 | 一站式 | 混合使用 |
| Apple Reminders | 免费 | 内置、简洁 | 基础任务 |
| Notion | 免费/高级版 | 一站式工作空间 | 团队协作 |

### 笔记工具

| 工具 | 价格 | 特点 | 适用场景 |
|------|------|------|----------|
| Apple Notes | 免费 | 内置、简洁 | 快速笔记 |
| Obsidian | 免费 | Markdown、双向链接 | 知识管理 |
| Notion | 免费/高级版 | 一站式 | 团队、项目 |
| Bear | $14.99/年 | 界面美观、Markdown | 写作者 |
| Craft | 免费/高级版 | 原生、美观 | 文档 |
| DEVONthink | $99 | 功能强大、AI | 研究 |
| Evernote | 免费/高级版 | 跨平台 | 老用户 |

### 日历

| 工具 | 价格 | 特点 |
|------|------|------|
| Apple Calendar | 免费 | 内置、iCloud 同步 |
| Fantastical | $49.99/年 | 自然语言、界面美观 |
| BusyCal | $49.99 | 功能强大、可定制 |
| Google Calendar | 免费 | 跨平台 |
| Calendly | 免费/高级版 | 日程安排 |

### 邮件

| 工具 | 价格 | 特点 |
|------|------|------|
| Apple Mail | 免费 | 内置、简洁 |
| Spark | 免费/高级版 | 智能收件箱、团队 |
| Airmail | $9.99 | 可定制 |
| Outlook | 免费/高级版 | Microsoft 集成 |
| Thunderbird | 免费 | 开源 |
| Mimestream | $49.99/年 | 原生 Gmail |

---

## 实用工具

### 文件工具

| 工具 | 价格 | 用途 |
|------|------|------|
| CleanMyMac X | $34.95 | 清理、维护 |
| DaisyDisk | $9.99 | 磁盘空间分析 |
| The Unarchiver | 免费 | 解压缩 |
| Keka | 免费 | 压缩 |
| AppCleaner | 免费 | 应用卸载 |
| OnyX | 免费 | 系统维护 |

### 剪贴板管理

| 工具 | 价格 | 特点 |
|------|------|------|
| Paste | $3.99/月 | 界面美观、可视化 |
| Alfred | 免费/高级版 | 剪贴板 + 启动器 |
| Maccy | 免费 | 轻量 |
| CopyClip | 免费 | 简洁 |
| Flycut | 免费 | 面向开发者 |

### 窗口管理

| 工具 | 价格 | 特点 |
|------|------|------|
| Rectangle | 免费 | 键盘快捷键 |
| Magnet | $7.99 | 拖放操作 |
| Moom | $10.99 | 自定义布局 |
| Amethyst | 免费 | 平铺管理器 |
| BetterSnapTool | $2.99 | 吸附区域 |

### 启动器

| 工具 | 价格 | 特点 |
|------|------|------|
| Alfred | 免费/高级版 | 功能强大、工作流 |
| Raycast | 免费/高级版 | 现代、快速 |
| Spotlight | 免费 | 内置、简洁 |
| LaunchBar | $29 | 快速、智能学习 |

---

## 安全

### 密码管理

| 工具 | 价格 | 特点 |
|------|------|------|
| 1Password | $2.99/月 | 家庭、团队 |
| Bitwarden | 免费/高级版 | 开源 |
| LastPass | 免费/高级版 | 跨平台 |
| Apple Keychain | 免费 | 内置、简洁 |
| KeePassXC | 免费 | 本地存储 |

### VPN

| 工具 | 价格 | 特点 |
|------|------|------|
| Mullvad | $5/月 | 注重隐私 |
| ProtonVPN | 免费/高级版 | 总部在瑞士 |
| WireGuard | 免费 | 开源协议 |
| ExpressVPN | $8.32/月 | 速度快、节点多 |
| NordVPN | $3.29/月 | 网络庞大 |

### 杀毒软件

| 工具 | 价格 | 特点 |
|------|------|------|
| Malwarebytes | 免费/高级版 | 恶意软件清除 |
| ClamXAV | $29.99/年 | 病毒扫描 |
| Avast | 免费/高级版 | 实时保护 |
| Bitdefender | $29.99/年 | 全面保护 |

### 防火墙

| 工具 | 价格 | 特点 |
|------|------|------|
| Little Snitch | $45 | 网络监控 |
| LuLu | 免费 | 开源 |
| Radio Silence | $9 | 简单拦截 |
| Hands Off! | $49 | 应用控制 |

---

## 通讯

### 即时通讯

| 工具 | 价格 | 特点 |
|------|------|------|
| Messages | 免费 | iMessage、短信 |
| Slack | 免费/高级版 | 团队沟通 |
| Discord | 免费 | 社区、游戏 |
| Telegram | 免费 | 隐私、频道 |
| Signal | 免费 | 注重隐私 |
| WhatsApp | 免费 | 跨平台 |

### 视频会议

| 工具 | 价格 | 特点 |
|------|------|------|
| FaceTime | 免费 | Apple 生态 |
| Zoom | 免费/高级版 | 广泛使用 |
| Google Meet | 免费 | Google 集成 |
| Microsoft Teams | 免费/高级版 | Office 集成 |
| Webex | 免费/高级版 | 企业级 |

### 邮件客户端

| 工具 | 价格 | 特点 |
|------|------|------|
| Apple Mail | 免费 | 内置 |
| Spark | 免费/高级版 | 智能收件箱 |
| Airmail | $9.99 | 可定制 |
| Outlook | 免费/高级版 | Microsoft |
| Thunderbird | 免费 | 开源 |

---

## 媒体

### 视频播放器

| 工具 | 价格 | 特点 |
|------|------|------|
| IINA | 免费 | 现代、原生 |
| VLC | 免费 | 支持所有格式 |
| Infuse | 免费/高级版 | 界面美观、元数据 |
| Movist Pro | $7.99 | 高级功能 |
| mpv | 免费 | 命令行 |

### 音频播放器

| 工具 | 价格 | 特点 |
|------|------|------|
| Apple Music | 免费/高级版 | Apple 生态 |
| Spotify | 免费/高级版 | 音乐流媒体 |
| VOX | 免费/高级版 | Hi-Res 音频 |
| Swinsian | $24.95 | 音乐库 |
| Audirvana | $49.99 | 发烧级 |

### 图片查看器

| 工具 | 价格 | 特点 |
|------|------|------|
| Preview | 免费 | 内置 |
| XnView MP | 免费 | 多格式支持 |
| qView | 免费 | 轻量 |
| ApolloOne | 免费/高级版 | 快速浏览 |
| Lyn | $19.99 | 专业级 |

### 屏幕录制

| 工具 | 价格 | 特点 |
|------|------|------|
| QuickTime | 免费 | 内置 |
| OBS Studio | 免费 | 专业级 |
| ScreenFlow | $129 | 视频编辑 |
| Kap | 免费 | GIF 录制 |
| Cleanshot X | $29 | 截图 + 录制 |

---

## 开发工具

### 版本控制

| 工具 | 价格 | 特点 |
|------|------|------|
| Git | 免费 | 命令行 |
| GitHub Desktop | 免费 | GitHub 图形界面 |
| Sourcetree | 免费 | Git 图形界面 |
| Tower | $69/年 | 专业 Git |
| GitKraken | 免费/高级版 | 可视化 Git |
| Sublime Merge | $99 | 快速 Git 图形界面 |

### API 开发

| 工具 | 价格 | 特点 |
|------|------|------|
| Postman | 免费/高级版 | API 测试 |
| Insomnia | 免费/高级版 | REST、GraphQL |
| Paw | $49.99 | 原生 HTTP 客户端 |
| HTTPie | 免费 | 命令行 |
| curl | 免费 | 命令行 |

### 数据库工具

| 工具 | 价格 | 特点 |
|------|------|------|
| TablePlus | $89 | 多数据库支持 |
| DBeaver | 免费 | 通用数据库 |
| Sequel Pro | 免费 | MySQL |
| pgAdmin | 免费 | PostgreSQL |
| MongoDB Compass | 免费 | MongoDB |
| Redis Insight | 免费 | Redis |

### 容器

| 工具 | 价格 | 特点 |
|------|------|------|
| Docker Desktop | 免费/高级版 | 容器 |
| OrbStack | 免费/高级版 | 快速容器 |
| Podman | 免费 | 无 root 容器 |
| Kubernetes | 免费 | 容器编排 |

### 虚拟化

| 工具 | 价格 | 特点 |
|------|------|------|
| UTM | 免费 | 虚拟机 |
| Parallels | $99.99/年 | Mac 上运行 Windows |
| VirtualBox | 免费 | 开源 |
| VMware Fusion | $149 | 专业级 |

---

## 文件管理

### 文件管理器

| 工具 | 价格 | 特点 |
|------|------|------|
| Finder | 免费 | 内置 |
| Path Finder | $29.95 | 功能强大的替代品 |
| ForkLift | $29.95 | 双面板、FTP |
| Commander One | 免费/高级版 | 双面板 |
| Transmit | $45 | FTP 客户端 |
| Cyberduck | 免费 | FTP、云存储 |

### 云存储

| 工具 | 价格 | 存储空间 | 特点 |
|------|------|----------|------|
| iCloud | 免费/$0.99+ | 5GB-12TB | Apple 生态集成 |
| Dropbox | 免费/$9.99+ | 2GB-3TB | 跨平台 |
| Google Drive | 免费/$1.99+ | 15GB-2TB | Google 服务 |
| OneDrive | 免费/$1.99+ | 5GB-6TB | Microsoft |
| Syncthing | 免费 | 无限制 | 自托管 |

### 备份工具

| 工具 | 价格 | 特点 |
|------|------|------|
| Time Machine | 免费 | 内置备份 |
| Carbon Copy Cloner | $49.99 | 可启动备份 |
| SuperDuper! | $27.95 | 克隆和备份 |
| Arq | $49.99 | 云备份 |
| Restic | 免费 | 开源 |

---

## 系统工具

### 监控

| 工具 | 价格 | 特点 |
|------|------|------|
| Activity Monitor | 免费 | 内置 |
| iStat Menus | $9.99 | 菜单栏统计 |
| Stats | 免费 | 开源统计 |
| htop | 免费 | 终端进程查看器 |
| btop | 免费 | 终端系统监控 |

### 维护

| 工具 | 价格 | 特点 |
|------|------|------|
| OnyX | 免费 | 系统维护 |
| CleanMyMac X | $34.95 | 清理、优化 |
| AppCleaner | 免费 | 应用卸载 |
| KnockKnock | 免费 | 持久化软件检测 |
| BlockBlock | 免费 | 持久化保护 |

### 系统信息

| 工具 | 价格 | 特点 |
|------|------|------|
| System Information | 免费 | 内置 |
| Mactracker | 免费 | Apple 硬件信息 |
| coconutBattery | 免费 | 电池健康 |
| DriveDx | $19.99 | 磁盘健康 |
| EtreCheck | 免费/高级版 | 系统诊断 |

### 个性化定制

| 工具 | 价格 | 特点 |
|------|------|------|
| BetterTouchTool | $9 | 手势、窗口管理 |
| Bartender | $16 | 菜单栏整理 |
| Dozer | 免费 | 菜单栏隐藏 |
| Hidden Bar | 免费 | 菜单栏隐藏 |
| uBar | $30 | Dock 替代品 |

---

## 总结

macOS 拥有满足各种需求的应用程序：

- **编辑器**：VS Code、Sublime Text、Xcode 用于开发
- **终端**：iTerm2、Alacritty 用于命令行操作
- **浏览器**：Safari、Chrome、Firefox 用于网页浏览
- **设计**：Figma、Sketch、Affinity 用于创意工作
- **效率工具**：Things、Obsidian、Notion 用于组织管理
- **实用工具**：Alfred、Rectangle、CleanMyMac 用于系统增强
- **安全**：1Password、Little Snitch、VPN 用于安全防护
- **通讯**：Slack、Zoom、Spark 用于消息沟通
- **媒体**：IINA、VLC、Spotify 用于娱乐
- **开发工具**：Docker、Postman、TablePlus 用于编程开发
- **文件管理**：Finder 替代品、云存储
- **系统工具**：监控、维护、个性化定制

macOS 生态系统为专业人士和普通用户都提供了高质量的应用程序。大多数应用程序都提供免费试用，让您可以找到最适合自己工作流程的工具。
