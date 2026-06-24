# Linux 优质软件：完整集合

Linux 最佳软件综合目录，按类别组织。从音频制作到系统管理，本指南涵盖你需要的一切。

## 目录

- [音频](#音频)
- [视频](#视频)
- [图形](#图形)
- [生产力](#生产力)
- [办公](#办公)
- [通信](#通信)
- [互联网](#互联网)
- [系统工具](#系统工具)
- [安全](#安全)
- [开发](#开发)
- [游戏](#游戏)
- [教育](#教育)
- [科学](#科学)
- [终端工具](#终端工具)

---

## 音频

### 音乐播放器

| 应用 | 类型 | 描述 | 安装 |
|-----|------|-------------|---------|
| Rhythmbox | GUI | GNOME 默认音乐播放器 | `apt install rhythmbox` |
| Clementine | GUI | 音乐播放器和管理器 | `apt install clementine` |
| Strawberry | GUI | 现代音乐播放器 | AppImage/Flatpak |
| Audacious | GUI | 轻量播放器 | `apt install audacious` |
| Lollypop | GUI | GNOME 音乐播放器 | `apt install lollypop` |
| DeaDBeeF | GUI | 模块化音乐播放器 | 下载 .deb |
| MPD + ncmpcpp | TUI | 音乐播放器守护进程 + 客户端 | `apt install mpd ncmpcpp` |
| cmus | TUI | 控制台音乐播放器 | `apt install cmus` |
| Spotify | GUI | 音乐流媒体（专有） | Snap/Flatpak |

### 音频编辑

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Audacity | 多轨音频编辑器 | `apt install audacity` |
| Ardour | 数字音频工作站 | `apt install ardour` |
| LMMS | 音乐制作 | `apt install lmms` |
| Mixxx | DJ 软件 | `apt install mixxx` |
| Hydrogen | 鼓机 | `apt install hydrogen` |
| Carla | 音频插件宿主 | `apt install carla` |
| Calf Studio Gear | 音频效果插件 | `apt install calf-plugins` |

### 音频工具

| 应用 | 描述 |
|-----|-------------|
| PulseAudio | 声音服务器 |
| PipeWire | 现代音频服务器 |
| JACK | 专业音频 |
| SoX | 命令行音频处理 |
| FFmpeg | 音频转换 |
| EasyEffects | 音频效果（PipeWire） |
| PulseEffects | 音频效果（PulseAudio） |

---

## 视频

### 视频播放器

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| VLC | 通用媒体播放器 | `apt install vlc` |
| mpv | 轻量强大的播放器 | `apt install mpv` |
| Celluloid | mpv 前端（GTK） | `apt install celluloid` |
| GNOME Videos | GNOME 视频播放器 | `apt install totem` |
| Haruna | mpv 前端（Qt） | Flatpak |
| Clapper | 现代视频播放器 | Flatpak |

### 视频编辑

| 应用 | 描述 | 类型 |
|------|-------------|------|
| DaVinci Resolve | 专业视频编辑器 | 专有/免费 |
| Kdenlive | 非线性视频编辑器 | 开源 |
| Shotcut | 跨平台视频编辑器 | 开源 |
| OpenShot | 初学者友好编辑器 | 开源 |
| Olive | 非线性编辑器 | 开源 |
| Pitivi | GNOME 视频编辑器 | 开源 |
| Flowblade | 多轨编辑器 | 开源 |
| LosslessCut | 无损视频剪切 | 开源 |

### 屏幕录制

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| OBS Studio | 录制和直播 | `apt install obs-studio` |
| SimpleScreenRecorder | 屏幕录制 | `apt install simplescreenrecorder` |
| Kazam | 屏幕截图 | `apt install kazam` |
| Green Recorder | 简单录制 | Flatpak |
| GPU Screen Recorder | GPU 加速 | Flatpak |

### 视频转换

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| HandBrake | 视频转码器 | Flatpak |
| FFmpeg | 命令行转换 | `apt install ffmpeg` |
| Shutter Encoder | 媒体转换器 | 下载 |
| WinFF | FFmpeg 前端 | `apt install winff` |

---

## 图形

### 图像编辑器

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| GIMP | 图像处理 | `apt install gimp` |
| Krita | 数字绘画 | `apt install krita` |
| Pinta | 简单图像编辑器 | `apt install pinta` |
| MyPaint | 绘画应用 | `apt install mypaint` |
| Photopea | 基于浏览器的编辑器 | Web 应用 |

### 矢量图形

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Inkscape | 矢量图形编辑器 | `apt install inkscape` |
| Penpot | 设计平台 | Web 应用 |
| Karbon | 矢量绘图 | `apt install karbon` |
| sK1 | 矢量图形 | 下载 |

### 3D 图形

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Blender | 3D 创作套件 | `apt install blender` |
| FreeCAD | 参数化 3D 建模 | `apt install freecad` |
| OpenSCAD | 基于脚本的建模 | `apt install openscad` |
| MeshLab | 网格处理 | `apt install meshlab` |
| MakeHuman | 人物模型创建 | 下载 |

### 照片管理

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| digiKam | 照片管理 | `apt install digikam` |
| Shotwell | GNOME 照片管理器 | `apt install shotwell` |
| Darktable | 照片工作流 | `apt install darktable` |
| RawTherapee | RAW 照片处理 | `apt install rawtherapee` |
| gThumb | 图像查看和编辑 | `apt install gthumb` |

### 截图工具

| 应用 | 描述 |
|-----|-------------|
| Flameshot | 功能丰富的截图工具 |
| GNOME Screenshot | 简单截图工具 |
| Shutter | 截图和编辑 |
| scrot | 命令行截图 |
| maim | 命令行截图 |

---

## 生产力

### 笔记

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Joplin | 带同步的笔记 | AppImage/Flatpak |
| Standard Notes | 加密笔记 | Flatpak |
| Logseq | 知识库 | AppImage |
| Trilium | 个人知识库 | 下载 |
| Zim | 桌面 Wiki | `apt install zim` |
| CherryTree | 分层笔记 | `apt install cherrytree` |
| Simplenote | 简单笔记 | Snap/Flatpak |
| Notion | 工作区（专有） | Web 应用 |
| Obsidian | 知识库（专有） | AppImage |

### 任务管理

| 应用 | 描述 | 类型 |
|------|-------------|------|
| GNOME Todo | 简单任务管理器 | `apt install gnome-todo` |
| Planner | 任务管理器 | Flatpak |
| Todoist | 任务管理器（专有） | 应用/Web |
| Vikunja | 自托管任务 | Docker |
| Taskwarrior | 命令行任务 | `apt install taskwarrior` |
| todo.txt | 纯文本任务 | Shell 脚本 |

### 思维导图

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Freeplane | 思维导图 | 下载 |
| Vym | 思维导图 | `apt install vym` |
| XMind | 思维导图（专有） | 下载 |
| Draw.io | 图表 | Snap/Web |

### 日历

| 应用 | 描述 |
|-----|-------------|
| GNOME Calendar | GNOME 日历应用 |
| Thunderbird | 邮件 + 日历 |
| Lightning | Thunderbird 日历扩展 |
| KOrganizer | KDE 日历 |
| Calcurse | 终端日历 |

---

## 办公

### 办公套件

| 套件 | 组件 | 安装 |
|-------|-----------|---------|
| LibreOffice | Writer、Calc、Impress、Draw | `apt install libreoffice` |
| OnlyOffice | Docs、Sheets、Presentation | Flatpak/Snap |
| Calligra | Words、Sheets、Stage | `apt install calligra` |
| FreeOffice | TextMaker、PlanMaker、Presentations | 下载 |
| WPS Office | Writer、Spreadsheet、Presentation | 下载 |

### 文档工具

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Evince | PDF 查看器（GNOME） | `apt install evince` |
| Okular | 文档查看器（KDE） | `apt install okular` |
| Zathura | 极简 PDF 查看器 | `apt install zathura` |
| Master PDF Editor | PDF 编辑器（专有） | 下载 |
| Xournal++ | PDF 标注 | Flatpak |
| Scribus | 桌面出版 | `apt install scribus` |
| Pandoc | 文档转换器 | `apt install pandoc` |
| Calibre | 电子书管理 | `apt install calibre` |

### 电子表格

| 应用 | 描述 |
|-----|-------------|
| LibreOffice Calc | 全功能电子表格 |
| Gnumeric | 轻量电子表格 |
| OnlyOffice Spreadsheet | 现代电子表格 |

---

## 通信

### 邮件客户端

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Thunderbird | 功能丰富的邮件 | `apt install thunderbird` |
| Geary | GNOME 邮件 | `apt install geary` |
| Evolution | GNOME PIM 套件 | `apt install evolution` |
| KMail | KDE 邮件 | `apt install kmail` |
| Mailspring | 现代邮件 | Snap/Flatpak |
| neomutt | 终端邮件 | `apt install neomutt` |
| aerc | 终端邮件 | 从源码构建 |
| Claws Mail | 轻量邮件 | `apt install claws-mail` |

### 聊天应用

| 应用 | 协议 | 安装 |
|-----|----------|---------|
| Signal | Signal 协议 | `apt install signal-desktop` |
| Telegram | Telegram | `apt install telegram-desktop` |
| Element | Matrix | Flatpak |
| Discord | Discord（专有） | `apt install discord` |
| Slack | Slack（专有） | Snap/Flatpak |
| Pidgin | 多协议 | `apt install pidgin` |
| HexChat | IRC | `apt install hexchat` |
| Weechat | IRC（终端） | `apt install weechat` |
| Fractal | Matrix（GNOME） | Flatpak |

### 视频会议

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Jitsi Meet | 视频会议 | Web 应用 |
| Zoom | 视频会议（专有） | 下载 |
| BigBlueButton | 虚拟教室 | Docker |
| Wire | 视频会议 | Flatpak |
| MiroTalk | 视频会议 | Docker |

---

## 互联网

### Web 浏览器

| 浏览器 | 引擎 | 安装 |
|---------|--------|---------|
| Firefox | Gecko | `apt install firefox` |
| Chromium | Blink | `apt install chromium-browser` |
| Brave | Blink | 仓库 |
| Vivaldi | Blink | 下载 |
| LibreWolf | Gecko | Flatpak |
| Falkon | WebKit | `apt install falkon` |
| Epiphany | WebKit（GNOME） | `apt install epiphany-browser` |
| qutebrowser | WebKit | `apt install qutebrowser` |

### 下载管理器

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Motrix | 下载管理器 | AppImage |
| Persepolis | 下载管理器 | `apt install persepolis` |
| aria2 | 命令行下载器 | `apt install aria2` |
| yt-dlp | 视频下载器 | `pip install yt-dlp` |
| wget | 命令行下载器 | `apt install wget` |
| curl | 数据传输工具 | `apt install curl` |

### Torrent 客户端

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Transmission | 简单 torrent 客户端 | `apt install transmission` |
| qBittorrent | 功能丰富的 torrent 客户端 | `apt install qbittorrent` |
| Deluge | 基于插件的 torrent 客户端 | `apt install deluge` |
| rTorrent | 终端 torrent 客户端 | `apt install rtorrent` |

### RSS 阅读器

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Newsboat | 终端 RSS 阅读器 | `apt install newsboat` |
| Liferea | GNOME RSS 阅读器 | `apt install liferea` |
| Akregator | KDE RSS 阅读器 | `apt install akregator` |
| Thunderbird | 邮件 + RSS | `apt install thunderbird` |
| Miniflux | 自托管 RSS | Docker |

### VPN 客户端

| 应用 | 协议 | 安装 |
|-----|----------|---------|
| WireGuard | WireGuard | `apt install wireguard` |
| OpenVPN | OpenVPN | `apt install openvpn` |
| NetworkManager | 多种 | 内置 |
| ProtonVPN | ProtonVPN | Flatpak |

---

## 系统工具

### 系统监控

| 应用 | 类型 | 安装 |
|-----|------|---------|
| htop | 终端 | `apt install htop` |
| btop | 终端 | 下载/Flatpak |
| glances | 终端 | `pip install glances` |
| bpytop | 终端 | `pip install bpytop` |
| GNOME System Monitor | GUI | `apt install gnome-system-monitor` |
| KSysGuard | GUI（KDE） | `apt install ksysguard` |
| nmon | 终端 | `apt install nmon` |
| iotop | 终端（磁盘 I/O） | `apt install iotop` |
| nethogs | 终端（网络） | `apt install nethogs` |

### 文件管理器

| 应用 | 类型 | 安装 |
|-----|------|---------|
| Nautilus | GUI（GNOME） | `apt install nautilus` |
| Dolphin | GUI（KDE） | `apt install dolphin` |
| Thunar | GUI（XFCE） | `apt install thunar` |
| PCManFM | GUI（LXDE） | `apt install pcmanfm` |
| ranger | 终端 | `apt install ranger` |
| lf | 终端 | 下载 |
| nnn | 终端 | `apt install nnn` |
| mc | 终端（Midnight Commander） | `apt install mc` |

### 分区工具

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| GParted | 分区编辑器 | `apt install gparted` |
| GNOME Disks | 磁盘工具 | `apt install gnome-disks` |
| fdisk | 命令行分区 | 内置 |
| parted | 命令行分区 | `apt install parted` |

### 备份工具

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Timeshift | 系统快照 | `apt install timeshift` |
| rsync | 文件同步 | `apt install rsync` |
| Borg | 去重备份 | `apt install borgbackup` |
| Restic | 快速备份 | `apt install restic` |
| Duplicati | 带加密的备份 | Flatpak |
| Deja Dup | GNOME 备份 | `apt install deja-dup` |
| Rclone | 云同步 | `apt install rclone` |

### 包管理器

| 管理器 | 格式 | 安装 |
|---------|--------|---------|
| apt | .deb | 内置（Debian/Ubuntu） |
| dnf | .rpm | 内置（Fedora） |
| pacman | .pkg | 内置（Arch） |
| Flatpak | Flatpak | `apt install flatpak` |
| Snap | Snap | `apt install snapd` |
| AppImage | AppImage | 直接运行 |
| Homebrew | Formulae | 安装脚本 |
| Nix | Nix packages | 安装脚本 |

---

## 安全

### 密码管理器

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| KeePassXC | 离线密码管理器 | `apt install keepassxc` |
| Bitwarden | 在线密码管理器 | Flatpak/Snap |
| pass | Unix 密码管理器 | `apt install pass` |
| gopass | 密码管理器 | 下载 |
| 1Password | 密码管理器（专有） | 下载 |

### 加密工具

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| GnuPG | 加密 | `apt install gnupg` |
| VeraCrypt | 磁盘加密 | 下载 |
| age | 文件加密 | 下载 |
| Cryptomator | 云加密 | Flatpak |
| LUKS | 磁盘加密 | 内置 |
| Tomb | 文件加密 | GitHub |

### 网络安全

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Wireshark | 网络分析器 | `apt install wireshark` |
| nmap | 网络扫描器 | `apt install nmap` |
| OWASP ZAP | Web 安全 | 下载 |
| Burp Suite | Web 安全（专有） | 下载 |
| ClamAV | 杀毒软件 | `apt install clamav` |
| rkhunter | Rootkit 检测 | `apt install rkhunter` |
| Lynis | 安全审计 | `apt install lynis` |

### 防火墙

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| UFW | 简单防火墙 | `apt install ufw` |
| firewalld | 动态防火墙 | `apt install firewalld` |
| iptables | 包过滤 | 内置 |
| nftables | 包过滤 | 内置 |

---

## 开发

### 代码编辑器和 IDE

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| VS Code | 代码编辑器 | Snap/Flatpak |
| VSCodium | 无遥测的 VS Code | 仓库 |
| Neovim | 终端编辑器 | `apt install neovim` |
| Vim | 终端编辑器 | `apt install vim` |
| Emacs | 可扩展编辑器 | `apt install emacs` |
| Sublime Text | 文本编辑器（专有） | 下载 |
| JetBrains IDEs | 语言专用 IDE | Toolbox |
| Zed | 快速编辑器 | 下载 |
| Lapce | 现代编辑器 | 下载 |
| Geany | 轻量 IDE | `apt install geany` |

### 版本控制

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Git | 版本控制 | `apt install git` |
| lazygit | 终端 Git UI | 下载 |
| tig | 文本模式 Git | `apt install tig` |
| GitKraken | Git GUI（专有） | 下载 |
| Sublime Merge | Git 客户端（专有） | 下载 |

### 容器

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Docker | 容器平台 | 仓库 |
| Podman | 无 root 容器 | `apt install podman` |
| Kubernetes | 容器编排 | 各种 |
| Distrobox | 基于容器的开发 | GitHub |
| Toolbox | 基于容器的开发 | 内置（Fedora） |

### 数据库

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| DBeaver | 通用数据库工具 | Flatpak |
| Beekeeper Studio | 数据库管理器 | Flatpak |
| SQLiteBrowser | SQLite GUI | `apt install sqlitebrowser` |
| pgAdmin | PostgreSQL 管理 | Docker |
| MySQL Workbench | MySQL GUI | 下载 |

### API 工具

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Insomnia | API 客户端 | Flatpak |
| Hoppscotch | API 测试 | Web 应用 |
| Bruno | API 客户端 | Flatpak |
| HTTPie | HTTP 客户端 | `pip install httpie` |
| Postman | API 平台（专有） | 下载 |

---

## 游戏

### 游戏引擎

| 引擎 | 语言 | 安装 |
|--------|----------|---------|
| Godot | GDScript/C# | Flatpak |
| Unity | C# | 下载 |
| Unreal Engine | C++ | 下载 |
| Bevy | Rust | Cargo |
| LÖVE | Lua | `apt install love` |
| Pygame | Python | `pip install pygame` |

### Linux 原生游戏

| 游戏 | 类型 | 安装 |
|------|-------|---------|
| 0 A.D. | RTS | `apt install 0ad` |
| SuperTuxKart | 赛车 | `apt install supertuxkart` |
| Minetest | 沙盒 | `apt install minetest` |
| OpenTTD | 模拟 | `apt install openttd` |
| Battle for Wesnoth | 策略 | `apt install wesnoth` |
| FreeCiv | 策略 | `apt install freeciv` |
| Xonotic | FPS | 下载 |
| Teeworlds | 平台射击 | `apt install teeworlds` |
| Hedgewars | 炮兵 | `apt install hedgewars` |
| The Dark Mod | 潜行 | 下载 |

### Steam 和 Proton

| 工具 | 描述 | 安装 |
|------|-------------|---------|
| Steam | 游戏平台 | `apt install steam` |
| Proton | Windows 游戏兼容 | Steam 内置 |
| Proton GE | 增强版 Proton | ProtonUp-Qt |
| Lutris | 游戏管理器 | Flatpak |
| Heroic | Epic/GOG 启动器 | Flatpak |
| Bottles | Windows 应用运行器 | Flatpak |
| Wine | Windows 兼容 | `apt install wine` |

### 模拟器

| 模拟器 | 平台 | 安装 |
|----------|----------|---------|
| RetroArch | 多系统 | Flatpak |
| Dolphin | GameCube/Wii | Flatpak |
| PCSX2 | PlayStation 2 | Flatpak |
| RPCS3 | PlayStation 3 | 下载 |
| Yuzu | Nintendo Switch | 下载 |
| mGBA | Game Boy Advance | `apt install mgba` |
| DeSmuME | Nintendo DS | `apt install desmume` |
| MAME | 街机 | `apt install mame` |

---

## 教育

### 学习平台

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Anki | 闪卡应用 | `apt install anki` |
| GCompris | 儿童活动 | `apt install gcompris-qt` |
| Marble | 虚拟地球 | `apt install marble` |
| Stellarium | 天文学 | `apt install stellarium` |
| KGeography | 地理学习 | `apt install kgeography` |
| Scratch | 可视化编程 | Snap/Web |

### 打字练习

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Klavaro | 打字练习 | `apt install klavaro` |
| TypingTest | 打字速度测试 | Web 应用 |
| gtypist | 打字练习 | `apt install gtypist` |
| keybr.com | 打字练习 | Web 应用 |

### 语言学习

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Anki | 间隔重复 | `apt install anki` |
| GoldenDict | 词典 | `apt install goldendict` |
| LibreLingo | 语言学习 | Web 应用 |

---

## 科学

### 科学计算

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| GNU Octave | MATLAB 替代 | `apt install octave` |
| R | 统计计算 | `apt install r-base` |
| Scilab | 数值计算 | 下载 |
| SageMath | 数学 | 下载 |
| Julia | 科学编程 | 下载 |
| Jupyter | 交互式笔记本 | `pip install jupyter` |
| Spyder | 科学 IDE | `pip install spyder` |

### 数据科学

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| RStudio | R IDE | 下载 |
| Orange | 数据挖掘 | Flatpak |
| KNIME | 数据分析 | 下载 |
| JupyterLab | 笔记本界面 | `pip install jupyterlab` |
| VS Code + Python | Python IDE | 扩展 |

### 天文学

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Stellarium | 天文馆 | `apt install stellarium` |
| KStars | 天文学 | `apt install kstars` |
| Celestia | 太空模拟 | `apt install celestia` |
| Siril | 天文摄影 | Flatpak |

### 化学

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| Avogadro | 分子编辑器 | `apt install avogadro` |
| GROMACS | 分子动力学 | `apt install gromacs` |
| Gabedit | 计算化学 | 下载 |

---

## 终端工具

### Shell

| Shell | 描述 | 安装 |
|-------|-------------|---------|
| Bash | 默认 shell | 内置 |
| Zsh | 扩展 shell | `apt install zsh` |
| Fish | 用户友好 shell | `apt install fish` |
| Nushell | 现代 shell | 下载 |
| Elvish | 表达性 shell | 下载 |

### 终端模拟器

| 应用 | 描述 | 安装 |
|-----|-------------|---------|
| GNOME Terminal | GNOME 默认终端 | 内置 |
| Konsole | KDE 终端 | `apt install konsole` |
| Alacritty | GPU 加速 | `apt install alacritty` |
| Kitty | GPU 加速 | `apt install kitty` |
| WezTerm | GPU 加速 | Flatpak |
| Terminator | 多终端 | `apt install terminator` |
| Tilix | 平铺终端 | `apt install tilix` |
| st | 简单终端 | 从源码构建 |

### 命令行工具

| 工具 | 描述 | 安装 |
|------|-------------|---------|
| exa/eza | 现代 ls | `apt install exa` |
| bat | 现代 cat | `apt install bat` |
| fd | 现代 find | `apt install fd-find` |
| ripgrep | 现代 grep | `apt install ripgrep` |
| fzf | 模糊查找 | `apt install fzf` |
| zoxide | 智能 cd | 安装脚本 |
| starship | 跨 shell 提示符 | 安装脚本 |
| tmux | 终端复用器 | `apt install tmux` |
| zellij | 现代终端复用器 | 下载 |
| jq | JSON 处理器 | `apt install jq` |
| yq | YAML 处理器 | 下载 |
| tldr | 简化 man 页面 | `apt install tldr` |
| cheat | 速查表 | 下载 |
| direnv | 每目录环境 | `apt install direnv` |

### 文件工具

| 工具 | 描述 | 安装 |
|------|-------------|---------|
| rsync | 文件同步 | `apt install rsync` |
| rclone | 云同步 | `apt install rclone` |
| mc | 文件管理器 | `apt install mc` |
| ranger | 文件管理器 | `apt install ranger` |
| tree | 目录树 | `apt install tree` |
| duf | 磁盘使用 | 下载 |
| dust | 磁盘使用 | 下载 |
| ncdu | 磁盘使用 | `apt install ncdu` |

---

## 安装指南

### 包管理器快速参考

| 发行版 | 包管理器 | 安装命令 |
|-------------|----------------|-----------------|
| Ubuntu/Debian | apt | `sudo apt install package` |
| Fedora | dnf | `sudo dnf install package` |
| Arch Linux | pacman | `sudo pacman -S package` |
| openSUSE | zypper | `sudo zypper install package` |

### 通用包

| 格式 | 安装 | 运行 |
|--------|---------|-----|
| Flatpak | `flatpak install package` | `flatpak run package` |
| Snap | `sudo snap install package` | 自动可用 |
| AppImage | `chmod +x file.AppImage` | `./file.AppImage` |

### 设置 Flatpak

```bash
# 安装 Flatpak
sudo apt install flatpak

# 添加 Flathub 仓库
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# 安装应用
flatpak install flathub com.spotify.Client

# 更新所有应用
flatpak update
```

---

## 总结

Linux 拥有令人难以置信的免费和开源软件生态系统。本目录涵盖了每个类别中最流行和维护良好的应用。

从发行版的包管理器开始安装大多数软件。对于不在仓库中的应用使用 Flatpak。需要时使用 Snap 或 AppImage 作为替代。Linux 桌面从未如此强大。
