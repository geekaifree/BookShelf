# Raspberry Pi：完整入门教程

## 简介

Raspberry Pi 是一系列小型、经济实惠的单板计算机，专为教育、原型开发和嵌入式项目设计。本教程涵盖硬件设置、操作系统安装、GPIO 编程和常见项目模式。

## Raspberry Pi 型号

| 型号 | CPU | 内存 | 价格 | 最佳用途 |
|------|-----|------|------|---------|
| Pi 5 | BCM2712, 2.4GHz | 4/8 GB | $60-80 | 桌面、媒体、AI |
| Pi 4 | BCM2711, 1.8GHz | 1/2/4/8 GB | $35-75 | 通用计算 |
| Pi Zero 2 W | BCM2710A1, 1GHz | 512 MB | $15 | IoT、嵌入式 |
| Pi Zero W | BCM2835, 1GHz | 512 MB | $10 | 最小化 IoT |
| Pi Pico | RP2040, 133MHz | 264 KB | $4 | 微控制器 |

## 必备硬件

| 组件 | 用途 | 推荐 |
|------|------|------|
| 电源 | 5V USB-C（Pi 4/5）或 Micro-USB（Zero） | 官方 Raspberry Pi 电源 |
| microSD 卡 | 启动和存储 | 32 GB Class 10，A2 等级 |
| 外壳 | 保护和散热 | Pi 5 用主动散热外壳 |
| HDMI 线 | 显示输出 | Micro-HDMI 转 HDMI（Pi 4/5） |
| 键盘/鼠标 | 输入 | USB 或蓝牙 |
| 散热片 | 热管理 | 大多数外壳附带 |
| 风扇 | 主动散热 | Pi 5 推荐使用 |

## 操作系统安装

### Raspberry Pi Imager（推荐）

1. 从 raspberrypi.com 下载 Raspberry Pi Imager。
2. 将 microSD 卡插入电脑。
3. 打开 Imager 并选择操作系统。
4. 选择 SD 卡。
5. 点击"Write"并等待完成。

### 支持的操作系统

| 操作系统 | 桌面 | 用例 |
|----------|------|------|
| Raspberry Pi OS（桌面版） | 有 | 通用、教育 |
| Raspberry Pi OS（Lite） | 无 | 无头服务器、IoT |
| Ubuntu Server | 无 | 服务器应用 |
| Ubuntu Desktop | 有 | 完整 Linux 桌面 |
| LibreELEC | 无 | Kodi 媒体中心 |
| OctoPrint | 无 | 3D 打印机管理 |
| Home Assistant | 无 | 智能家居自动化 |
| RetroPie | 无 | 复古游戏 |
| Kali Linux | 有 | 安全测试 |

### 无头设置

首次启动无需显示器：

| 文件 | 位置 | 用途 |
|------|------|------|
| ssh | 启动分区（空文件） | 启用 SSH |
| wpa_supplicant.conf | 启动分区 | Wi-Fi 配置 |
| userconf.txt | 启动分区 | 默认用户密码 |

### SSH 连接

```bash
ssh pi@raspberrypi.local
# 默认密码：raspberry（请立即更改）
```

## 系统配置

### raspi-config

| 选项 | 用途 |
|------|------|
| System Options | 主机名、密码、启动行为 |
| Display Options | 分辨率、过扫描 |
| Interface Options | SSH、VNC、SPI、I2C、GPIO |
| Performance Options | 超频、GPU 内存 |
| Localisation | 区域设置、时区、键盘 |

### 常用命令

| 命令 | 用途 |
|------|------|
| sudo apt update | 更新软件包列表 |
| sudo apt upgrade | 升级已安装的软件包 |
| sudo raspi-config | 系统配置工具 |
| vcgencmd measure_temp | 检查 CPU 温度 |
| free -h | 检查内存使用 |
| df -h | 检查磁盘使用 |
| hostname -I | 获取 IP 地址 |

## GPIO（通用输入/输出）

### GPIO 引脚布局

| 引脚 | 功能 | GPIO 编号 |
|------|------|----------|
| 1 | 3.3V 电源 | - |
| 2 | 5V 电源 | - |
| 3 | SDA（I2C） | GPIO 2 |
| 4 | 5V 电源 | - |
| 5 | SCL（I2C） | GPIO 3 |
| 6 | 接地 | - |
| 7 | GPIO | GPIO 4 |
| 8 | TX（UART） | GPIO 14 |
| 9 | 接地 | - |
| 10 | RX（UART） | GPIO 15 |

### GPIO 模式

| 模式 | 描述 | 用例 |
|------|------|------|
| IN | 输入模式 | 读取传感器、按钮 |
| OUT | 输出模式 | LED、继电器 |
| ALT0-5 | 交替功能 | SPI、I2C、PWM、UART |

### Python GPIO 编程

安装库：

```bash
sudo apt install python3-gpiozero
```

### LED 控制示例

| 组件 | 引脚 |
|------|------|
| LED 阳极（+） | GPIO 17（Pin 11） |
| LED 阴极（-） | 接地（Pin 9） |
| 电阻 | 330 欧姆串联 |

```python
from gpiozero import LED
from time import sleep

led = LED(17)
while True:
    led.on()
    sleep(1)
    led.off()
    sleep(1)
```

### 按钮输入示例

```python
from gpiozero import Button
from signal import pause

button = Button(2)
button.when_pressed = lambda: print("Pressed!")
button.when_released = lambda: print("Released!")
pause()
```

## 通信协议

| 协议 | 引脚 | 速度 | 用例 |
|------|------|------|------|
| I2C | SDA、SCL | 100-400 kHz | 传感器、显示器 |
| SPI | MOSI、MISO、SCLK、CE | 最高 125 MHz | 高速外设 |
| UART | TX、RX | 115200+ 波特率 | 串口通信 |
| 1-Wire | 1 根数据线 | 16.3 kbit/s | 温度传感器 |
| PWM | 任意 GPIO | 可变 | 电机控制、LED |

### I2C 设置

```bash
sudo raspi-config  # 在 Interface Options 中启用 I2C
sudo apt install i2c-tools
i2cdetect -y 1     # 扫描 I2C 设备
```

## 常见项目

| 项目 | 组件 | 难度 |
|------|------|------|
| LED 闪烁 | LED、电阻 | 入门 |
| 温度监控 | DHT22 传感器 | 入门 |
| 运动检测 | PIR 传感器 | 入门 |
| 摄像头系统 | Pi Camera Module | 中级 |
| 气象站 | 多个传感器 | 中级 |
| 媒体中心 | LibreELEC、HDMI | 入门 |
| 网络广告拦截 | Pi-hole | 入门 |
| 家庭自动化 | Home Assistant | 中级 |
| 遥控车 | 电机、H 桥 | 高级 |
| AI 物体检测 | Coral USB Accelerator | 高级 |

## 摄像头模块

| 功能 | Camera Module 3 | Camera Module 3 Wide |
|------|-----------------|---------------------|
| 分辨率 | 12 MP | 12 MP |
| 视场角 | 66 度 | 120 度 |
| 自动对焦 | 是 | 是 |
| 视频 | 1080p50、720p100 | 1080p50、720p100 |
| 价格 | $25 | $35 |

### 摄像头命令

| 命令 | 用途 |
|------|------|
| libcamera-hello | 预览摄像头画面 |
| libcamera-still -o photo.jpg | 拍照 |
| libcamera-vid -o video.h264 -t 10000 | 录制 10 秒视频 |
| libcamera-still -t 0 --timelapse 5000 | 每 5 秒延时摄影 |

## 网络

| 服务 | 设置 |
|------|------|
| SSH | 在 raspi-config 中启用或创建 ssh 文件 |
| VNC | 在 raspi-config 中启用，安装 RealVNC |
| Samba | sudo apt install samba 用于文件共享 |
| Pi-hole | curl -sSL https://install.pi-hole.net \| bash |
| VPN | 安装 WireGuard 或 OpenVPN |

## 性能优化

| 建议 | 详情 |
|------|------|
| 使用高速 SD 卡 | A2 等级卡提供更好的 I/O |
| 启用超频 | 通过 raspi-config（仅 Pi 4/5） |
| 使用 SSD | USB 3.0 启动提供更快的存储 |
| 添加散热 | 散热片 + 风扇用于持续负载 |
| 减少 GPU 内存 | 无头模式设置 gpu_mem=16 |
| 禁用未使用的服务 | 释放内存和 CPU 周期 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无显示 | HDMI 端口错误 | 使用 HDMI0（最靠近 USB-C 的） |
| 低电压警告 | 电源不足 | 使用官方 5V/3A 电源 |
| 过热 | 无散热 | 添加散热片和风扇 |
| Wi-Fi 不工作 | 国家代码错误 | 在 raspi-config 中设置 |
| SD 卡损坏 | 不安全关机 | 使用只读根分区或 UPS |

## 总结

Raspberry Pi 是一个多功能平台，适用于学习编程、电子和计算。从简单的 LED 项目到复杂的 IoT 系统，它提供了一个经济实惠且文档完善的生态系统。理解 GPIO、通信协议和操作系统，将为你打开数千个项目的大门。
