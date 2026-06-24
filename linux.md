# Linux

> 本文档整合了以下源文件：linux.md

---

## 来源：linux.md

## 简介

本指南提供了一份精选的 Linux 必备软件列表，涵盖各种用途。基于 Awesome Linux Software 收藏，包括生产力、开发、媒体和系统管理方面的应用。

### Linux 桌面环境

| 环境 | 描述 | 资源占用 |
|------|------|----------|
| GNOME | 现代、用户友好 | 高 |
| KDE Plasma | 功能丰富、可定制 | 中高 |
| XFCE | 轻量、传统 | 低 |
| LXQt | 非常轻量 | 非常低 |
| Cinnamon | 传统布局 | 中 |
| MATE | GNOME 2 的延续 | 中低 |

### 选择发行版

| 发行版 | 最佳用途 | 基础 |
|--------|----------|------|
| Ubuntu | 初学者、通用 | Debian |
| Fedora | 最新软件 | 独立 |
| Linux Mint | Windows 迁移者 | Ubuntu |
| Arch Linux | 高级用户 | 独立 |
| Debian | 稳定性 | 独立 |
| openSUSE | 企业、桌面 | 独立 |

## Web 浏览器

### 浏览器选项

| 浏览器 | 引擎 | 特性 |
|--------|------|------|
| Firefox | Gecko | 隐私优先、扩展 |
| Chromium | Blink | 开源 Chrome |
| Brave | Blink | 内置广告拦截 |
| Vivaldi | Blink | 高度可定制 |
| Tor Browser | Gecko | 最大隐私 |
| Falkon | QtWebEngine | 轻量 |

### Firefox 配置

```bash
# 安装 Firefox
sudo apt install firefox

# 安装扩展
# uBlock Origin、Privacy Badger、HTTPS Everywhere
```

## 办公和生产力

### 办公套件

| 套件 | 格式支持 | 特性 |
|------|----------|------|
| LibreOffice | MS Office、ODF | 完整办公套件 |
| OnlyOffice | MS Office | 协作编辑 |
| WPS Office | MS Office | MS 兼容 UI |
| Calligra | ODF | KDE 集成 |

### 笔记应用

| 应用 | 特性 | 同步 |
|------|------|------|
| Joplin | Markdown、加密 | 云同步 |
| Simplenote | 极简 | 云同步 |
| Standard Notes | 加密 | 云同步 |
| Zim | Wiki 风格 | 本地 |
| CherryTree | 层级结构 | 本地 |

### 任务管理

| 应用 | 特性 |
|------|------|
| Todo.txt | 纯文本任务 |
| Planner | GNOME 任务 |
| Taskwarrior | 命令行任务 |
| Kanban boards | 可视化任务板 |

## 开发工具

### 代码编辑器

| 编辑器 | 类型 | 特性 |
|--------|------|------|
| VS Code | GUI | 扩展、调试 |
| Vim | 终端 | 模态编辑 |
| Neovim | 终端 | 现代 Vim |
| Emacs | 两者 | 可扩展 |
| Sublime Text | GUI | 快速、轻量 |

### IDE

| IDE | 语言重点 |
|-----|----------|
| IntelliJ IDEA | Java、Kotlin |
| PyCharm | Python |
| Eclipse | Java |
| Android Studio | Android |
| Qt Creator | C++、Qt |

### 版本控制

| 工具 | 用途 |
|------|------|
| Git | 分布式版本控制 |
| GitKraken | GUI Git 客户端 |
| Sublime Merge | 快速 Git GUI |
| lazygit | 终端 Git UI |

### 容器工具

| 工具 | 用途 |
|------|------|
| Docker | 容器运行时 |
| Podman | 无 root 容器 |
| Buildah | 容器构建 |
| Skopeo | 容器镜像管理 |
| distroless | 最小容器镜像 |

## 媒体应用

### 视频播放器

| 播放器 | 特性 |
|--------|------|
| VLC | 播放一切 |
| MPV | 轻量、可脚本化 |
| Celluloid | MPV 前端 |
| Haruna | 基于 Qt 的播放器 |

### 音频播放器

| 播放器 | 特性 |
|--------|------|
| Rhythmbox | GNOME 音乐播放器 |
| Clementine | 功能丰富 |
| Strawberry | Clementine 分支 |
| Audacious | 轻量 |
| DeaDBeeF | 模块化播放器 |

### 图片编辑器

| 编辑器 | 特性 |
|--------|------|
| GIMP | 全功能编辑器 |
| Krita | 数字绘画 |
| Inkscape | 矢量图形 |
| Darktable | RAW 照片处理 |
| Shotwell | 照片管理 |

### 视频编辑

| 编辑器 | 特性 |
|--------|------|
| Kdenlive | 非线性编辑器 |
| Shotcut | 跨平台 |
| OpenShot | 适合初学者 |
| DaVinci Resolve | 专业级 |
| Olive | 现代编辑器 |

## 系统工具

### 文件管理器

| 管理器 | 特性 |
|--------|------|
| Nautilus | GNOME 默认 |
| Dolphin | KDE 默认 |
| Thunar | XFCE 默认 |
| PCManFM | 轻量 |
| Ranger | 基于终端 |
| Midnight Commander | 基于终端 |

### 终端模拟器

| 模拟器 | 特性 |
|--------|------|
| GNOME Terminal | GNOME 默认 |
| Konsole | KDE 终端 |
| Alacritty | GPU 加速 |
| Kitty | GPU 加速、功能丰富 |
| Tilix | 平铺终端 |
| Terminator | 平铺、分屏 |

### 系统监控

| 工具 | 特性 |
|------|------|
| htop | 进程查看器 |
| btop | 现代进程查看器 |
| glances | 系统概览 |
| nmon | 性能监控 |
| iotop | I/O 监控 |

## 网络工具

### 网络管理器

| 工具 | 特性 |
|------|------|
| NetworkManager | GUI 和 CLI |
| systemd-networkd | Systemd 网络 |
| ConnMan | 轻量管理器 |
| Wicd | 无线管理器 |

### SSH 客户端

| 客户端 | 特性 |
|--------|------|
| OpenSSH | 标准 SSH |
| Mosh | 移动 shell |
| Termius | GUI SSH 客户端 |
| Remmina | 远程桌面 |

### VPN 客户端

| 客户端 | 协议 |
|--------|------|
| WireGuard | WireGuard |
| OpenVPN | OpenVPN |
| NetworkManager VPN | 多种 |
| Mullvad VPN | WireGuard、OpenVPN |

## 安全工具

### 防火墙

| 工具 | 界面 |
|------|------|
| ufw | 命令行 |
| firewalld | D-Bus 接口 |
| iptables | 底层 |
| nftables | 现代 iptables |

### 杀毒软件

| 工具 | 特性 |
|------|------|
| ClamAV | 开源扫描器 |
| rkhunter | Rootkit 检测 |
| chkrootkit | Rootkit 检测 |
| Lynis | 安全审计 |

### 密码管理器

| 管理器 | 特性 |
|--------|------|
| KeePassXC | 本地存储 |
| Bitwarden | 云同步 |
| pass | Unix 密码管理器 |
| gopass | 多存储 pass |

## 通讯

### 邮件客户端

| 客户端 | 特性 |
|--------|------|
| Thunderbird | 功能丰富 |
| Geary | GNOME 邮件 |
| KMail | KDE 邮件 |
| Neomutt | 终端邮件 |
| aerc | 终端邮件 |

### 聊天应用

| 应用 | 协议 |
|------|------|
| Signal | Signal 协议 |
| Element | Matrix |
| Telegram | Telegram 协议 |
| HexChat | IRC |
| Discord | Discord（非官方） |

### 视频会议

| 应用 | 特性 |
|------|------|
| Jitsi Meet | 可自托管 |
| Zoom | 跨平台 |
| Google Meet | 基于浏览器 |
| BigBlueButton | 教育导向 |

## 包管理

### 包管理器

| 管理器 | 发行版 |
|--------|--------|
| apt | Debian、Ubuntu |
| dnf | Fedora |
| pacman | Arch Linux |
| zypper | openSUSE |
| flatpak | 通用 |
| snap | 通用 |
| AppImage | 通用 |

### Flatpak 使用

```bash
# 安装 Flatpak
sudo apt install flatpak

# 添加 Flathub 仓库
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# 安装应用
flatpak install flathub com.visualstudio.code

# 更新应用
flatpak update
```

### Snap 使用

```bash
# 安装 Snap
sudo apt install snapd

# 安装应用
sudo snap install code --classic

# 列出已安装的 snap
snap list

# 刷新 snap
sudo snap refresh
```

## 备份方案

### 备份工具

| 工具 | 类型 | 特性 |
|------|------|------|
| rsync | 同步 | 增量、高效 |
| Timeshift | 系统快照 | BTRFS、RSYNC |
| Borgbackup | 去重 | 加密、压缩 |
| Duplicati | 云备份 | 多目标 |
| Restic | 快速备份 | 加密、去重 |

### 备份策略

```bash
# 使用 rsync
rsync -av --delete /home/ /backup/home/

# 使用 Timeshift
sudo timeshift --create --comments "Before update"
```

## 开发语言

### 语言安装

| 语言 | 安装 |
|------|------|
| Python | `sudo apt install python3` |
| Node.js | `sudo apt install nodejs` |
| Rust | `curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs \| sh` |
| Go | 从 golang.org 下载 |
| Java | `sudo apt install default-jdk` |

### 版本管理器

| 管理器 | 语言 |
|--------|------|
| pyenv | Python |
| nvm | Node.js |
| rbenv | Ruby |
| sdkman | Java、Kotlin |

## 总结

| 类别 | 推荐 |
|------|------|
| 浏览器 | Firefox、Chromium |
| 办公 | LibreOffice |
| 编辑器 | VS Code、Vim |
| 媒体 | VLC、GIMP |
| 终端 | Alacritty、Kitty |
| 文件管理器 | Dolphin、Nautilus |


---
