# USB 工具

> 本文档整合了以下源文件：boot.md, usb.md

---

## 来源：boot.md

## 简介

Rufus 是一款免费开源工具，用于格式化和创建可启动 USB 闪存驱动器。它广泛用于安装操作系统、刷写固件以及从可移动介质运行底层工具。

## 目录

1. [入门指南](#入门指南)
2. [界面概览](#界面概览)
3. [创建可启动 USB](#创建可启动-usb)
4. [启动模式](#启动模式)
5. [分区方案](#分区方案)
6. [文件系统选项](#文件系统选项)
7. [高级选项](#高级选项)
8. [常见用例](#常见用例)
9. [故障排除](#故障排除)

## 入门指南

### 系统要求

| 要求 | 详情 |
|------|------|
| 操作系统 | Windows 8 或更高版本 |
| 架构 | x86, x64, ARM64 |
| 磁盘空间 | Rufus 本身仅需 1 MB |
| USB 驱动器 | 建议最少 8 GB |
| 权限 | 需要管理员权限 |

### 下载与验证

| 步骤 | 操作 |
|------|------|
| 1 | 访问 https://rufus.ie |
| 2 | 下载最新的便携版或安装版 |
| 3 | 可选验证 SHA-256 哈希值 |
| 4 | 以管理员权限运行可执行文件 |

### 支持的 ISO 来源

| 来源类型 | 示例 |
|----------|------|
| Linux 发行版 | Ubuntu, Fedora, Debian, Arch |
| Windows | Windows 10, Windows 11 |
| 救援工具 | Hiren's Boot, SystemRescue |
| 固件 | BIOS 更新, memtest86 |
| 杀毒软件 | Kaspersky Rescue Disk |

## 界面概览

### 主面板元素

| 元素 | 位置 | 用途 |
|------|------|------|
| 设备下拉菜单 | 顶部 | 选择目标 USB 驱动器 |
| SELECT 按钮 | 启动选项 | 选择 ISO 或光盘镜像 |
| 分区方案 | 中部 | MBR 或 GPT 选择 |
| 目标系统 | 中部 | BIOS 或 UEFI 目标 |
| 文件系统 | 中部 | FAT32, NTFS, exFAT |
| START 按钮 | 底部 | 开始创建过程 |

### 状态栏信息

| 指示器 | 含义 |
|--------|------|
| Ready | 等待输入 |
| Writing | 数据正在写入 USB |
| Validating | 正在验证写入数据 |
| Complete | 过程成功完成 |

## 创建可启动 USB

### 分步流程

| 步骤 | 操作 | 详情 |
|------|------|------|
| 1 | 插入 USB 驱动器 | 使用 USB 3.0 以获得更快的速度 |
| 2 | 启动 Rufus | 以管理员身份运行 |
| 3 | 选择设备 | 从下拉菜单中选择正确的 USB |
| 4 | 点击 SELECT | 浏览并选择 ISO 文件 |
| 5 | 配置选项 | 分区方案、文件系统 |
| 6 | 点击 START | 开始过程 |
| 7 | 确认覆盖 | 接受数据销毁警告 |
| 8 | 等待完成 | 不要移除 USB |

### 按操作系统推荐设置

| 操作系统 | 分区方案 | 目标系统 | 文件系统 |
|----------|----------|----------|----------|
| Windows 11 | GPT | UEFI (non-CSM) | NTFS |
| Windows 10 | GPT | UEFI (non-CSM) | NTFS |
| Ubuntu 24.04 | GPT | UEFI (non-CSM) | FAT32 |
| Fedora 40 | GPT | UEFI (non-CSM) | FAT32 |
| Debian 12 | GPT | UEFI (non-CSM) | FAT32 |

## 启动模式

### BIOS 与 UEFI

| 特性 | Legacy BIOS | UEFI |
|------|-------------|------|
| 启动速度 | 较慢 | 较快 |
| 驱动器大小限制 | 2 TB | 9.4 ZB |
| 安全启动 | 否 | 是 |
| 图形界面 | 文本模式 | 图形界面 |
| 分区表 | MBR | GPT |
| 现代硬件 | 很少支持 | 标准支持 |

### UEFI 兼容性

| 设置 | 何时使用 |
|------|----------|
| UEFI (non-CSM) | 现代系统，默认选择 |
| UEFI (CSM) | 兼容模式 |
| BIOS | 仅限旧硬件 |

## 分区方案

### MBR 与 GPT

| 特性 | MBR | GPT |
|------|-----|-----|
| 最大分区数 | 4 个主分区 | 128 个 |
| 最大磁盘大小 | 2 TB | 9.4 ZB |
| 启动模式 | BIOS | UEFI |
| 冗余 | 无 | 有，备份头 |
| 兼容性 | 所有系统 | 现代系统 |

### 选择指南

| 场景 | 推荐方案 |
|------|----------|
| 在现代 PC 上安装 | GPT |
| 在旧 PC 上安装 | MBR |
| 与 Linux 双启动 | GPT |
| 仅 BIOS 系统 | MBR |
| Windows 11 要求 | GPT |

## 文件系统选项

### 对比表

| 文件系统 | 最大文件大小 | 最大卷大小 | 可启动 | Windows | Linux | macOS |
|----------|-------------|-----------|--------|---------|-------|-------|
| FAT32 | 4 GB | 8 TB | 是 | 是 | 是 | 是 |
| NTFS | 16 EB | 256 TB | 是 | 是 | 有限 | 有限 |
| exFAT | 16 EB | 128 PB | 有限 | 是 | 是 | 是 |
| ext2/3/4 | 不等 | 不等 | 是 | 否 | 是 | 否 |

### 各文件系统适用场景

| 文件系统 | 最佳用途 |
|----------|----------|
| FAT32 | Linux ISO, UEFI 兼容性 |
| NTFS | Windows ISO, 大文件 |
| exFAT | 跨平台数据驱动器 |

## 高级选项

### 簇大小

| 簇大小 | 最佳用途 |
|--------|----------|
| 512 字节 | 大量小文件 |
| 4096 字节 | 默认，通用 |
| 16 KB | 大型媒体文件 |
| 64 KB | 超大文件 |

### 其他设置

| 设置 | 说明 | 默认值 |
|------|------|--------|
| 快速格式化 | 快速擦除，不检查坏扇区 | 启用 |
| 创建扩展标签 | 长卷标 | 启用 |
| 为旧 BIOS 添加修复 | 旧启动兼容性 | 禁用 |
| 使用 Rufus MBR | 自定义启动代码 | 禁用 |
| 检测 USB 硬盘 | 显示非可移动驱动器 | 禁用 |

### Windows 专用选项

| 选项 | 说明 |
|------|------|
| 移除 TPM 要求 | 绕过 Windows 11 TPM 检查 |
| 移除安全启动要求 | 绕过安全启动检查 |
| 移除 4 GB 内存要求 | 绕过内存要求 |
| 禁用数据收集 | 跳过隐私问题 |
| 创建本地账户 | 跳过 Microsoft 账户要求 |

## 常见用例

### 从 USB 安装 Windows

| 步骤 | 设置 |
|------|------|
| 1 | 从 Microsoft 下载 Windows ISO |
| 2 | 选择 GPT 分区方案 |
| 3 | 选择 UEFI (non-CSM) 目标 |
| 4 | 选择 NTFS 文件系统 |
| 5 | 如需要启用 Windows 专用绕过选项 |
| 6 | 点击 START |

### 从 USB 安装 Linux

| 步骤 | 设置 |
|------|------|
| 1 | 从发行版网站下载 Linux ISO |
| 2 | 选择 GPT 分区方案 |
| 3 | 选择 UEFI (non-CSM) 目标 |
| 4 | 选择 FAT32 文件系统 |
| 5 | 点击 START |

### 创建多启动 USB

| 工具 | 用途 |
|------|------|
| Ventoy | 在一个驱动器上加载多个 ISO |
| Rufus | 写入单个 ISO |

### 刷写 BIOS 固件

| 步骤 | 操作 |
|------|------|
| 1 | 从制造商下载 BIOS 更新 ISO |
| 2 | 为旧系统选择 MBR 方案 |
| 3 | 选择 FAT32 文件系统 |
| 4 | 写入 USB |
| 5 | 从 USB 启动以刷写固件 |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| USB 未检测到 | 未被识别为可移动设备 | 启用"检测 USB 硬盘" |
| 启动失败 | 分区方案错误 | 匹配 BIOS/UEFI 固件类型 |
| 大文件错误 | FAT32 文件大小限制 | 改用 NTFS |
| 写入速度慢 | USB 2.0 驱动器 | 使用 USB 3.0 驱动器和端口 |
| 写入时出错 | 驱动器写保护 | 检查物理锁定开关 |
| ISO 未识别 | 下载损坏 | 重新下载并验证哈希值 |

### 性能提示

| 提示 | 影响 |
|------|------|
| 使用 USB 3.0+ 驱动器 | 写入速度快 5-10 倍 |
| 关闭其他应用程序 | 防止 I/O 冲突 |
| 临时禁用杀毒软件 | 减少写入中断 |
| 使用前置 USB 端口 | 更好的信号质量 |

### 日志与诊断

| 操作 | 方法 |
|------|------|
| 查看日志 | 点击底部日志区域 |
| 保存日志 | 右键日志，保存 |
| 检查 USB 健康 | 使用 CrystalDiskInfo |
| 验证写入数据 | 使用内置哈希检查 |

## 总结

Rufus 提供了一种可靠快速的方式来创建可启动 USB 驱动器，用于操作系统安装和系统恢复。它对 BIOS 和 UEFI 启动模式、多种分区方案以及 Windows 专用绕过选项的支持，使其成为系统管理员和高级用户的通用工具。


---

## 来源：usb.md

## 简介

Ventoy 是一个用于创建可启动 USB 驱动器的开源工具。与传统工具不同，Ventoy 直接将 ISO 文件复制到 USB 驱动器，无需解压。你可以存储多个 ISO 文件，并从菜单中启动任意一个。本教程涵盖设置、配置和高级用法。

## Ventoy 与传统工具对比

| 功能 | Ventoy | Rufus | Etcher |
|------|--------|-------|--------|
| 多 ISO | 是（无限制） | 每次一个 | 每次一个 |
| 需要重新格式化 | 否 | 是 | 是 |
| ISO 解压 | 无需 | 直接写入 | 直接写入 |
| 启动菜单 | 内置 | 无 | 无 |
| BIOS/UEFI | 两者都支持 | 两者都支持 | 仅 UEFI |
| 持久化 | 支持 | 手动 | 否 |
| 安全启动 | 支持 | 无 | 无 |

## 系统要求

| 组件 | 要求 |
|------|------|
| USB 驱动器 | 最低 8 GB（推荐 32+ GB） |
| 操作系统（宿主） | Windows、Linux、macOS |
| 启动目标 | BIOS 和 UEFI 系统 |
| 文件系统 | exFAT（默认）、NTFS、FAT32 |

## 安装

### Windows

1. 从 GitHub releases 下载 Ventoy。
2. 运行 Ventoy2Disk.exe。
3. 选择 USB 驱动器。
4. 点击"Install"。

### Linux

```bash
# 下载并解压
tar -xf ventoy-*.tar.gz
cd ventoy-*

# 安装到 USB（将 /dev/sdX 替换为你的设备）
sudo ./Ventoy2Disk.sh -i /dev/sdX
```

### 更新 Ventoy

```bash
# 更新且不丢失 ISO 文件
sudo ./Ventoy2Disk.sh -u /dev/sdX
```

## 使用

### 添加 ISO 文件

| 步骤 | 操作 |
|------|------|
| 1 | 在 USB 驱动器上安装 Ventoy |
| 2 | 挂载 USB 驱动器（Ventoy 分区） |
| 3 | 将 ISO 文件直接复制到根目录或任意文件夹 |
| 4 | 安全弹出 |
| 5 | 从 USB 启动 |

### 支持的文件格式

| 格式 | 扩展名 | 备注 |
|------|--------|------|
| ISO | .iso | 标准磁盘映像 |
| WIM | .wim | Windows 映像 |
| VHD(x) | .vhd、.vhdx | 虚拟硬盘 |
| EFI | .efi | EFI 启动文件 |
| IMG | .img | 原始磁盘映像 |

### 已测试的操作系统

| 类别 | 示例 |
|------|------|
| Windows | 7、8、10、11、Server |
| Ubuntu | 所有版本 |
| Debian | 所有版本 |
| Fedora | 所有版本 |
| CentOS/RHEL | 7、8、9 |
| Arch Linux | 滚动发布 |
| Kali Linux | 所有版本 |
| 救援 | SystemRescue、GParted |
| macOS | 有限支持 |

## 配置

### ventoy.json

在 Ventoy 分区上创建 `ventoy/ventoy.json` 进行自定义设置。

```json
{
  "theme": {
    "file": "/ventoy/theme/ventoy/theme.txt",
    "gfxmode": "1920x1080"
  },
  "boot": {
    "default_entry": 0,
    "timeout": 10
  }
}
```

### 主题自定义

| 设置 | 选项 |
|------|------|
| gfxmode | 分辨率：1024x768、1920x1080 |
| theme file | 自定义 theme.txt，包含颜色和字体 |
| wallpaper | JPG 或 PNG 背景图片 |
| fonts | 自定义字体文件 |

## 菜单选项

| 选项 | 按键 | 描述 |
|------|------|------|
| Boot | Enter | 启动选中的 ISO |
| Boot (memdisk) | F1 | 将 ISO 加载到内存 |
| Boot (grub2) | F2 | 使用 GRUB2 链式加载 |
| Boot (wimboot) | F3 | 启动 WIM 文件 |
| Check ISO | F4 | 验证 ISO 完整性 |
| Memory test | F5 | 运行 memtest86+ |
| Info | F6 | 显示系统信息 |
| Reboot | Ctrl+Alt+Del | 重启系统 |

## 持久化

持久化可以在 Live Linux 系统重启后保存更改。

### 创建持久化

| 步骤 | 操作 |
|------|------|
| 1 | 创建持久化文件 |
| 2 | 正确命名（如 persistence.dat） |
| 3 | 放置在 ventoy 目录中 |
| 4 | 在 ventoy.json 中配置持久化映射 |

### 持久化配置

```json
{
  "persistence": [
    {
      "image": "/ubuntu-22.04.iso",
      "backend": "/persistence/ubuntu.dat",
      "type": "casper-rw"
    }
  ]
}
```

## 安全启动

| 步骤 | 操作 |
|------|------|
| 1 | 安装支持安全启动的 Ventoy |
| 2 | 首次启动时注册 MOK 密钥 |
| 3 | 从 UEFI 菜单选择"Enroll MOK" |
| 4 | 重启后 Ventoy 将在安全启动启用的情况下工作 |

## Ventoy Plugson

一个用于生成 ventoy.json 配置的图形工具。

| 功能 | 描述 |
|------|------|
| Auto install | 静默 Windows 安装 |
| Persistence | 为 Linux ISO 配置持久化 |
| Theme | 可视化主题自定义 |
| Menu alias | ISO 条目的自定义名称 |
| File path | 控制启动文件选择 |

## 磁盘布局

| 分区 | 大小 | 格式 | 用途 |
|------|------|------|------|
| Ventoy | ~32 MB | FAT32 | 启动文件和 EFI |
| Main | 剩余空间 | exFAT | ISO 存储 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| USB 未检测到 | BIOS 设置 | 启用 USB 启动，检查启动顺序 |
| ISO 无法启动 | 不兼容的 ISO | 检查兼容性列表 |
| 启动缓慢 | USB 2.0 端口 | 使用 USB 3.0 端口 |
| 安全启动失败 | MOK 未注册 | 在 UEFI 中注册 MOK 密钥 |
| 文件不可见 | 分区错误 | 检查是否复制到 Ventoy 分区 |
| 黑屏 | 显卡问题 | 尝试不同的启动模式（grub2/memdisk） |

## 命令行使用

### Linux CLI

```bash
# 安装 Ventoy
sudo ./Ventoy2Disk.sh -i /dev/sdX

# 更新 Ventoy
sudo ./Ventoy2Disk.sh -u /dev/sdX

# 安装支持安全启动的版本
sudo ./Ventoy2Disk.sh -i -s /dev/sdX

# 显示 USB 上的 Ventoy 版本
sudo ./Ventoy2Disk.sh -l /dev/sdX
```

## 最佳实践

| 实践 | 原因 |
|------|------|
| 使用 exFAT | 支持大文件（>4GB） |
| 标记你的驱动器 | 在 BIOS 中便于识别 |
| 保持 ISO 有序 | 使用文件夹分类 |
| 定期更新 | 获取最新的 bug 修复和兼容性 |
| 部署前测试 | 在目标硬件上验证启动 |
| 备份 ISO | 在电脑上保留副本 |

## 总结

Ventoy 通过消除为每个 ISO 重新格式化的需求，简化了创建可启动 USB 驱动器的过程。它能够容纳多个操作系统、支持 BIOS 和 UEFI、以及持久化存储功能，使其成为系统管理员、IT 专业人员和经常安装或测试操作系统的用户的必备工具。


---
