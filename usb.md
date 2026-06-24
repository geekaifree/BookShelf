# Ventoy：USB 启动工具教程

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
