# Raspberry Pi 完整资源指南

## 目录

1. [简介](#简介)
2. [设置与入门](#设置与入门)
3. [操作系统选择](#操作系统选择)
4. [GPIO 编程](#gpio-编程)
5. [传感器与组件](#传感器与组件)
6. [媒体中心项目](#媒体中心项目)
7. [网络附属存储](#网络附属存储)
8. [广告拦截与网络工具](#广告拦截与网络工具)
9. [VPN 与安全](#vpn-与安全)
10. [家庭自动化](#家庭自动化)
11. [配件](#配件)
12. [故障排除](#故障排除)
13. [性能优化](#性能优化)

---

## 简介

Raspberry Pi 是一系列小型、经济实惠的单板计算机，旨在推广计算机科学教育。自推出以来，它已广泛应用于从媒体中心到家庭自动化系统的各种项目。

### Raspberry Pi 型号

| 型号 | 内存 | CPU | USB | 以太网 | WiFi | 价格 |
|------|------|-----|-----|--------|------|------|
| Pi 5 | 4/8GB | 2.4GHz 四核 | 2x USB3, 2x USB2 | 千兆 | 是 | $60-80 |
| Pi 4 | 1/2/4/8GB | 1.5GHz 四核 | 2x USB3, 2x USB2 | 千兆 | 是 | $35-75 |
| Pi 3B+ | 1GB | 1.4GHz 四核 | 4x USB2 | 千兆 | 是 | $35 |
| Pi Zero 2 W | 512MB | 1GHz 四核 | 1x micro USB | 否 | 是 | $15 |
| Pi Zero W | 512MB | 1GHz 单核 | 1x micro USB | 否 | 是 | $10 |
| Pi Pico | 264KB | 133MHz 双核 | 无 | 否 | 否 | $4 |

### 常见用途

| 用途 | 难度 | Pi 型号 | 关键要求 |
|------|------|--------|----------|
| 桌面电脑 | 简单 | Pi 4/5 | 显示器、键盘、鼠标 |
| 媒体中心 | 简单 | Pi 4/5 | 电视、遥控器 |
| 复古游戏 | 中等 | Pi 4/5 | 控制器 |
| 家庭服务器 | 中等 | Pi 4/5 | 存储设备 |
| 广告拦截器 | 简单 | 任意型号 | 网络访问 |
| VPN 服务器 | 中等 | Pi 3/4 | 互联网访问 |
| 家庭自动化 | 中等 | Pi 3/4 | 智能设备 |
| 机器人 | 困难 | Pi 4/5 | 电机、传感器 |
| 气象站 | 中等 | Pi 3/4 | 传感器 |
| 安防摄像头 | 中等 | Pi 3/4 | 摄像头模块 |

---

## 设置与入门

### 所需组件

| 组件 | 用途 | 备注 |
|------|------|------|
| Raspberry Pi | 主板 | 根据项目选择 |
| 电源 | 供电 | Pi 4/5 需要 5V, 3A |
| MicroSD 卡 | 存储 | 建议 32GB 以上 |
| 外壳 | 保护 | 可选但建议使用 |
| 散热片 | 散热 | Pi 4/5 建议使用 |
| 风扇 | 主动散热 | 重度使用时可选 |
| HDMI 线 | 显示 | Pi 4/5 需要 Micro HDMI |
| 键盘/鼠标 | 输入 | USB 或蓝牙 |
| 以太网线 | 网络 | 使用 WiFi 时可选 |

### 初始设置步骤

1. **下载操作系统镜像**

```bash
# Download Raspberry Pi Imager
# https://www.raspberrypi.com/software/

# Or download directly
wget https://downloads.raspberrypi.com/raspios_arm64/images/raspios_arm64-2024-03-15/2024-03-15-raspios-bookworm-arm64.img.xz
```

2. **烧录 SD 卡**

```bash
# Using Raspberry Pi Imager (recommended)
# Select OS, select SD card, write

# Or using command line
sudo dd if=raspios.img of=/dev/sdX bs=4M status=progress
```

3. **配置 WiFi（无头设置）**

```bash
# Mount SD card boot partition
# Create file: wpa_supplicant.conf
country=US
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="YourNetworkName"
    psk="YourPassword"
}

# Create empty file: ssh (no extension)
touch /boot/ssh
```

4. **首次启动**

```bash
# Insert SD card, connect power
# Wait for boot (1-2 minutes)
# Connect via SSH
ssh pi@raspberrypi.local
# Default password: raspberry

# Change password immediately
passwd
```

### 基本配置

```bash
# Open configuration tool
sudo raspi-config

# Key settings:
# 1. System Options
#    - Password
#    - Hostname
#    - Boot options
# 2. Display Options
#    - Resolution
#    - Overscan
# 3. Interface Options
#    - SSH
#    - VNC
#    - SPI
#    - I2C
# 4. Localization Options
#    - Locale
#    - Timezone
#    - WiFi country
# 5. Advanced Options
#    - Expand filesystem
#    - Memory split
```

### 更新系统

```bash
# Update package list
sudo apt update

# Upgrade installed packages
sudo apt upgrade -y

# Full upgrade (including kernel)
sudo apt full-upgrade -y

# Reboot if needed
sudo reboot
```

---

## 操作系统选择

### 官方操作系统

| 操作系统 | 描述 | 适用场景 |
|----------|------|----------|
| Raspberry Pi OS | 基于 Debian 的官方系统 | 通用 |
| Raspberry Pi OS Lite | 无桌面环境 | 无头服务器 |
| Raspberry Pi OS Full | 包含推荐软件 | 初学者 |

### 第三方操作系统

| 操作系统 | 描述 | 适用场景 |
|----------|------|----------|
| Ubuntu Server | 完整的 Linux 服务器 | 服务器、开发 |
| Ubuntu Desktop | 完整桌面环境 | 桌面替代 |
| Kali Linux | 安全测试 | 渗透测试 |
| LibreELEC | 媒体中心 | Kodi 媒体中心 |
| OSMC | 媒体中心 | Kodi 媒体中心 |
| RetroPie | 复古游戏 | 游戏模拟 |
| Home Assistant OS | 家庭自动化 | 智能家居 |
| OctoPrint | 3D 打印机控制 | 3D 打印 |
| DietPi | 轻量级 | 最小化安装 |
| Manjaro ARM | 基于 Arch | 高级用户 |

### 操作系统对比

| 因素 | Pi OS | Ubuntu | DietPi | LibreELEC |
|------|-------|--------|--------|-----------|
| 体积 | 中等 | 较大 | 较小 | 较小 |
| 速度 | 快 | 中等 | 最快 | 快 |
| 支持 | 优秀 | 良好 | 良好 | 良好 |
| 桌面 | 是 | 是 | 可选 | 否 |
| 软件包 | 丰富 | 丰富 | 精选 | 有限 |
| 更新 | 定期 | 定期 | 定期 | 定期 |

### 安装不同操作系统

```bash
# Using Raspberry Pi Imager
1. Open Raspberry Pi Imager
2. Click "Choose OS"
3. Select from list or custom image
4. Select SD card
5. Click "Write"

# Using NOOBS
1. Format SD card as FAT32
2. Download NOOBS
3. Extract to SD card
4. Boot Pi and select OS
```

---

## GPIO 编程

### GPIO 引脚布局

```
Raspberry Pi GPIO Pinout (40-pin header):

     3V3  (1) (2)  5V
   GPIO2  (3) (4)  5V
   GPIO3  (5) (6)  GND
   GPIO4  (7) (8)  GPIO14
     GND  (9) (10) GPIO15
  GPIO17 (11) (12) GPIO18
  GPIO27 (13) (14) GND
  GPIO22 (15) (16) GPIO23
     3V3 (17) (18) GPIO24
  GPIO10 (19) (20) GND
   GPIO9 (21) (22) GPIO25
  GPIO11 (23) (24) GPIO8
     GND (25) (26) GPIO7
   GPIO0 (27) (28) GPIO1
   GPIO5 (29) (30) GND
   GPIO6 (31) (32) GPIO12
  GPIO13 (33) (34) GND
  GPIO19 (35) (36) GPIO16
  GPIO26 (37) (38) GPIO20
     GND (39) (40) GPIO21
```

### GPIO 模式

| 模式 | 描述 | 用途 |
|------|------|------|
| INPUT | 读取信号 | 按钮、传感器 |
| OUTPUT | 发送信号 | LED、电机 |
| PWM | 脉宽调制 | 舵机、亮度控制 |
| I2C | 串行通信 | 传感器、显示屏 |
| SPI | 串行通信 | ADC、显示屏 |
| UART | 串行通信 | GPS、串行设备 |

### Python GPIO 编程

**安装 GPIO 库：**

```bash
# RPi.GPIO (pre-installed on Pi OS)
pip install RPi.GPIO

# gpiozero (recommended for beginners)
pip install gpiozero
```

**使用 RPi.GPIO 控制 LED：**

```python
import RPi.GPIO as GPIO
import time

# Setup
LED_PIN = 18
GPIO.setmode(GPIO.BCM)
GPIO.setup(LED_PIN, GPIO.OUT)

# Blink LED
try:
    while True:
        GPIO.output(LED_PIN, GPIO.HIGH)
        time.sleep(1)
        GPIO.output(LED_PIN, GPIO.LOW)
        time.sleep(1)
except KeyboardInterrupt:
    GPIO.cleanup()
```

**使用 gpiozero 控制 LED：**

```python
from gpiozero import LED
from time import sleep

led = LED(18)

while True:
    led.on()
    sleep(1)
    led.off()
    sleep(1)
```

**按钮输入：**

```python
from gpiozero import Button, LED
from signal import pause

button = Button(2)
led = LED(18)

# LED follows button state
led.source = button

pause()
```

### I2C 通信

```python
import smbus

# Initialize I2C bus
bus = smbus.SMBus(1)  # 1 = /dev/i2c-1

# Read from device
DEVICE_ADDRESS = 0x48
data = bus.read_byte(DEVICE_ADDRESS)

# Write to device
bus.write_byte(DEVICE_ADDRESS, 0x01)

# Read word
value = bus.read_word_data(DEVICE_ADDRESS, 0x00)
```

### SPI 通信

```python
import spidev

# Initialize SPI
spi = spidev.SpiDev()
spi.open(0, 0)  # bus 0, device 0
spi.max_speed_hz = 1000000

# Read ADC (MCP3008)
def read_adc(channel):
    cmd = [1, (8 + channel) << 4, 0]
    response = spi.xfer2(cmd)
    value = ((response[1] & 3) << 8) + response[2]
    return value

# Read channel 0
value = read_adc(0)
print(f"ADC Value: {value}")
```

---

## 传感器与组件

### 常用传感器

| 传感器 | 测量参数 | 接口 | 库 |
|--------|----------|------|-----|
| DHT22 | 温度、湿度 | GPIO | Adafruit_DHT |
| BME280 | 温度、湿度、气压 | I2C | RPi.bme280 |
| DS18B20 | 温度 | 1-Wire | w1thermsensor |
| HC-SR04 | 距离 | GPIO | gpiozero |
| PIR | 运动检测 | GPIO | gpiozero |
| BH1750 | 光照强度 | I2C | smbus2 |
| MQ-2 | 气体检测 | GPIO/ADC | 自定义 |
| MPU6050 | 加速度计、陀螺仪 | I2C | mpu6050 |

### 传感器示例

**温度和湿度（DHT22）：**

```python
import Adafruit_DHT

DHT_SENSOR = Adafruit_DHT.DHT22
DHT_PIN = 4

humidity, temperature = Adafruit_DHT.read_retry(DHT_SENSOR, DHT_PIN)

if humidity is not None and temperature is not None:
    print(f"Temp: {temperature:.1f}°C")
    print(f"Humidity: {humidity:.1f}%")
else:
    print("Failed to read sensor")
```

**距离传感器（HC-SR04）：**

```python
from gpiozero import DistanceSensor
from time import sleep

sensor = DistanceSensor(echo=24, trigger=23)

while True:
    print(f"Distance: {sensor.distance * 100:.1f} cm")
    sleep(1)
```

**运动检测（PIR）：**

```python
from gpiozero import MotionSensor
from time import sleep

pir = MotionSensor(4)

pir.when_motion = print("Motion detected!")
pir.when_no_motion = print("No motion")

sleep(30)  # Run for 30 seconds
```

### 摄像头模块

```bash
# Enable camera
sudo raspi-config
# Interface Options > Camera > Enable

# Take photo
raspistill -o image.jpg

# Record video
raspivid -o video.h264 -t 10000  # 10 seconds
```

```python
# Using picamera2 (Python)
from picamera2 import Picamera2
from time import sleep

camera = Picamera2()
camera.start()
sleep(2)  # Camera warm-up
camera.capture_file("photo.jpg")
camera.stop()
```

### 显示选项

| 显示设备 | 接口 | 分辨率 | 用途 |
|----------|------|--------|------|
| HDMI 显示器 | HDMI | 最高 4K | 桌面 |
| 官方触摸屏 | DSI | 800x480 | 自助终端 |
| OLED 显示屏 | I2C | 128x64 | 状态显示 |
| LCD 16x2 | I2C/GPIO | 16 字符 x 2 行 | 简单输出 |
| 电子纸 | SPI | 多种 | 低功耗显示 |

---

## 媒体中心项目

### Kodi 媒体中心

**安装：**

```bash
# Option 1: LibreELEC (dedicated OS)
# Download from libreelec.tv and flash to SD card

# Option 2: Install Kodi on Pi OS
sudo apt update
sudo apt install kodi

# Launch Kodi
kodi
```

**Kodi 配置：**

| 设置 | 建议 |
|------|------|
| 视频输出 | 匹配电视分辨率 |
| 音频 | 根据设置选择 HDMI 或模拟 |
| 媒体库 | 添加媒体源 |
| 插件 | 安装实用插件 |
| 遥控器 | 配置 CEC 或应用 |

### 媒体服务器选项

| 服务器 | 功能 | 适用场景 |
|--------|------|----------|
| Plex | 流媒体、转码 | 远程访问 |
| Jellyfin | 开源、流媒体 | 自托管 |
| Emby | 流媒体、DVR | 媒体管理 |
| MiniDLNA | 简单 DLNA | 基本共享 |

**安装 Jellyfin：**

```bash
# Install dependencies
sudo apt install apt-transport-https

# Add repository
wget -O - https://repo.jellyfin.org/jellyfin_team.gpg.key | sudo apt-key add -
echo "deb [arch=$( dpkg --print-architecture )] https://repo.jellyfin.org/$( awk -F'=' '/^ID=/{ print $NF }' /etc/os-release ) $( awk -F'=' '/^VERSION_CODENAME=/{ print $NF }' /etc/os-release ) main" | sudo tee /etc/apt/sources.list.d/jellyfin.list

# Install Jellyfin
sudo apt update
sudo apt install jellyfin

# Start service
sudo systemctl start jellyfin
sudo systemctl enable jellyfin
```

### 流媒体设置

```
Media Center Architecture:

┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Storage   │────▶│ Raspberry Pi │────▶│     TV      │
│  (HDD/NAS)  │     │   (Kodi)    │     │   (HDMI)    │
└─────────────┘     └──────┬──────┘     └─────────────┘
                           │
                    ┌──────┴──────┐
                    │   Remote    │
                    │  (CEC/App)  │
                    └─────────────┘
```

---

## 网络附属存储

### NAS 设置

**硬件要求：**

| 组件 | 用途 | 建议 |
|------|------|------|
| Pi 4/5 | 主板 | 4GB+ 内存 |
| 外置硬盘 | 存储 | USB 3.0，带电源 |
| USB 集线器 | 多硬盘 | 带电源的集线器 |
| 外壳 | 保护 | 带风扇 |
| 以太网 | 网络 | 千兆连接 |

**软件安装：**

```bash
# Install Samba for Windows sharing
sudo apt install samba samba-common-bin

# Configure Samba
sudo nano /etc/samba/smb.conf

# Add share configuration
[share]
    comment=Pi Share
    path=/mnt/storage
    browseable=yes
    writeable=yes
    only guest=no
    create mask=0777
    directory mask=0777
    public=no

# Set Samba password
sudo smbpasswd -a pi

# Restart Samba
sudo systemctl restart smbd
```

**挂载外置硬盘：**

```bash
# Find drive
lsblk

# Create mount point
sudo mkdir /mnt/storage

# Mount drive
sudo mount /dev/sda1 /mnt/storage

# Auto-mount on boot
echo "/dev/sda1 /mnt/storage ext4 defaults 0 0" | sudo tee -a /etc/fstab
```

### OpenMediaVault

```bash
# Install OpenMediaVault
wget -O - https://github.com/OpenMediaVault-Plugin-Developers/installScript/raw/master/install | sudo bash

# Access web interface
# http://pi-ip-address
# Default: admin/openmediavault
```

---

## 广告拦截与网络工具

### Pi-hole

**安装：**

```bash
# One-line install
curl -sSL https://install.pi-hole.net | bash

# Or manual install
git clone --depth 1 https://github.com/pi-hole/pi-hole.git Pi-hole
cd "Pi-hole/automated install/"
sudo bash basic-install.sh
```

**配置：**

| 设置 | 建议 |
|------|------|
| 上游 DNS | Cloudflare (1.1.1.1) 或 Google (8.8.8.8) |
| 拦截 | 启用 |
| Web 界面 | 启用 |
| 日志记录 | 启用 |
| 隐私级别 | 根据偏好设置 |

**访问 Web 界面：**

```
URL: http://pi-ip-address/admin
Default password: (shown during install)
```

### 网络监控

| 工具 | 用途 | 安装命令 |
|------|------|----------|
| nmap | 网络扫描 | `sudo apt install nmap` |
| Wireshark | 数据包分析 | `sudo apt install wireshark` |
| iftop | 带宽监控 | `sudo apt install iftop` |
| vnstat | 流量统计 | `sudo apt install vnstat` |

---

## VPN 与安全

### WireGuard VPN

**安装：**

```bash
# Install WireGuard
sudo apt install wireguard

# Generate keys
wg genkey | tee privatekey | wg pubkey > publickey

# Configure interface
sudo nano /etc/wireguard/wg0.conf
```

**服务器配置：**

```ini
[Interface]
PrivateKey = <server_private_key>
Address = 10.0.0.1/24
ListenPort = 51820
PostUp = iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i wg0 -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
PublicKey = <client_public_key>
AllowedIPs = 10.0.0.2/32
```

**启动 WireGuard：**

```bash
sudo wg-quick up wg0
sudo systemctl enable wg-quick@wg0
```

### OpenVPN

```bash
# Install OpenVPN
sudo apt install openvpn easy-rsa

# Setup CA
make-cadir ~/openvpn-ca
cd ~/openvpn-ca
./easyrsa init-pki
./easyrsa build-ca
./easyrsa gen-req server nopass
./easyrsa sign-req server server
./easyrsa gen-dh

# Configure and start
sudo systemctl start openvpn@server
sudo systemctl enable openvpn@server
```

---

## 家庭自动化

### Home Assistant

**安装：**

```bash
# Install dependencies
sudo apt install -y apparmor cifs-utils curl dbus jq libglib2.0-bin     lsb-release network-manager socat

# Install Home Assistant OS
curl -Lo installer.sh https://raw.githubusercontent.com/home-assistant/supervised-installer/master/installer.sh
sudo bash installer.sh

# Or use Docker
docker run -d --name homeassistant --privileged --restart=unless-stopped     -v /home/pi/homeassistant:/config     -v /run/dbus:/run/dbus:ro     --network=host     ghcr.io/home-assistant/home-assistant:stable
```

**访问 Home Assistant：**

```
URL: http://pi-ip-address:8123
```

### Home Assistant 集成

| 集成 | 设备 | 协议 |
|------|------|------|
| Zigbee | 传感器、灯具 | Zigbee2MQTT |
| Z-Wave | 传感器、开关 | Z-Wave JS |
| WiFi | 各种设备 | 本地/云端 |
| Bluetooth | 追踪器、传感器 | BLE |
| MQTT | 自定义设备 | MQTT |

### MQTT 设置

```bash
# Install Mosquitto MQTT broker
sudo apt install mosquitto mosquitto-clients

# Configure
sudo nano /etc/mosquitto/mosquitto.conf

# Add:
listener 1883
allow_anonymous true

# Start service
sudo systemctl start mosquitto
sudo systemctl enable mosquitto
```

### 智能家居设备

| 设备类型 | 示例 | 协议 |
|----------|------|------|
| 灯具 | Philips Hue, IKEA | Zigbee, WiFi |
| 开关 | Sonoff, Shelly | WiFi |
| 传感器 | Aqara, Sonoff | Zigbee |
| 摄像头 | Reolink, Amcrest | RTSP |
| 恒温器 | Nest, Ecobee | WiFi |
| 门锁 | August, Yale | Z-Wave, WiFi |

---

## 配件

### 必备配件

| 配件 | 用途 | 建议 |
|------|------|------|
| 外壳 | 保护 | Flirc, Argon |
| 电源 | 供电 | 官方 RPi 电源 |
| SD 卡 | 存储 | Samsung EVO, SanDisk |
| 散热片 | 散热 | 铜、铝材质 |
| 风扇 | 主动散热 | Noctua 40mm |
| HDMI 线 | 显示 | Micro HDMI 转接器 |
| USB 集线器 | 扩展接口 | 带电源的 USB 3.0 |
| 摄像头 | 拍照/录像 | 官方摄像头模块 |
| 显示屏 | 输出 | 官方触摸屏 |

### HAT 扩展板

| HAT | 功能 | 用途 |
|-----|------|------|
| Sense HAT | 传感器、LED 矩阵 | 气象、实验 |
| PoE HAT | 以太网供电 | 整洁安装 |
| HiFiBerry | 音频输出 | 媒体中心 |
| Motor HAT | 电机控制 | 机器人 |
| Automation HAT | 工业 I/O | 家庭自动化 |
| GPS HAT | 定位 | 追踪 |

### 外壳与散热

| 外壳类型 | 特点 | 适用场景 |
|----------|------|----------|
| 基础款 | 简单保护 | 通用 |
| 风扇款 | 主动散热 | 高负载工作 |
| 被动散热 | 散热片设计 | 静音运行 |
| 工业款 | DIN 导轨安装 | 自动化 |
| 媒体款 | 红外接收器 | 媒体中心 |

---

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|------|------|----------|
| 无电源 | 电源不足 | 使用官方 3A 电源 |
| 无显示 | HDMI 问题 | 检查线缆、配置 |
| SD 卡速度慢 | 低质量卡 | 使用 Class 10/U3 |
| 过热 | 无散热 | 添加散热片/风扇 |
| WiFi 问题 | 干扰 | 更换信道、使用 5GHz |
| SSH 拒绝连接 | 未启用 | 通过 raspi-config 启用 |
| 启动失败 | SD 卡损坏 | 重新烧录系统 |
| USB 问题 | 功率不足 | 使用带电源的集线器 |

### 诊断命令

```bash
# Check temperature
vcgencmd measure_temp

# Check CPU frequency
vcgencmd measure_clock arm

# Check voltage
vcgencmd measure_volts

# Check memory
free -h

# Check disk space
df -h

# Check processes
top

# Check system logs
journalctl -xe

# Check hardware
lsusb
lspci
gpio readall
```

### SD 卡问题

| 问题 | 解决方案 |
|------|----------|
| 只读 | 重新挂载、检查卡 |
| 损坏 | 重新烧录、使用更好的卡 |
| 空间不足 | 扩展文件系统、清理日志 |
| 速度慢 | 更换更快的卡 |

---

## 性能优化

### 优化技巧

| 优化方法 | 操作 | 效果 |
|----------|------|------|
| 超频 | 编辑 config.txt | 速度提升 20-50% |
| USB 启动 | 从 SSD 启动 | 更快的 I/O |
| Swap | 优化交换文件 | 更好的内存管理 |
| 服务 | 禁用未使用的服务 | 减少内存占用 |
| GPU 内存 | 无头模式下减少 | 更多内存给 CPU |

### 超频

```bash
# Edit config.txt
sudo nano /boot/config.txt

# Add overclock settings (Pi 4)
over_voltage=6
arm_freq=2000
gpu_freq=700

# Monitor temperature
watch -n 1 vcgencmd measure_temp

# Stress test
sudo apt install stress
stress --cpu 4 --timeout 600
```

### SSD 启动

```bash
# Clone SD to SSD
sudo rpi-clone sda

# Update bootloader for USB boot
sudo raspi-config
# Advanced Options > Boot Order > USB Boot

# Update firmware
sudo rpi-eeprom-update -a
```

### 内存优化

```bash
# Check memory usage
free -h

# Disable unnecessary services
sudo systemctl disable bluetooth
sudo systemctl disable hciuart

# Reduce GPU memory (headless)
# Add to /boot/config.txt:
gpu_mem=16

# Optimize swap
sudo dphys-swapfile swapoff
sudo nano /etc/dphys-swapfile
# Set CONF_SWAPSIZE=100
sudo dphys-swapfile setup
sudo dphys-swapfile swapon
```

---

## 总结

Raspberry Pi 是一个功能强大的平台，适用于各种项目：

- **设置**：使用 Raspberry Pi OS 轻松完成初始配置
- **操作系统选择**：多种操作系统满足不同需求
- **GPIO**：使用 Python 编程控制硬件
- **传感器**：连接各种传感器和组件
- **媒体中心**：构建基于 Kodi 的娱乐系统
- **NAS**：使用外置硬盘创建网络存储
- **广告拦截**：使用 Pi-hole 实现全网广告拦截
- **VPN**：使用 WireGuard 实现安全远程访问
- **家庭自动化**：使用 Home Assistant 控制智能设备
- **配件**：通过 HAT 扩展板、外壳和散热方案增强功能

Raspberry Pi 社区为各种复杂度的项目提供了丰富的资源、教程和支持。
