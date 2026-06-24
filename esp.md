# ESP 开发：ESP8266 和 ESP32 项目指南

使用 ESP8266 和 ESP32 微控制器构建项目的综合指南。这些经济实惠的 WiFi 芯片是无数 IoT 项目的骨干。

## 目录

- [入门](#入门)
- [Arduino IDE 设置](#arduino-ide-设置)
- [ESP 上的 MicroPython](#esp-上的-micropython)
- [传感器](#传感器)
- [执行器](#执行器)
- [WiFi 项目](#wifi-项目)
- [蓝牙项目](#蓝牙项目)
- [MQTT 和 IoT](#mqtt-和-iot)
- [家庭自动化](#家庭自动化)
- [可穿戴设备](#可穿戴设备)
- [IoT 项目创意](#iot-项目创意)
- [电源管理](#电源管理)

---

## 入门

### ESP8266 vs ESP32

| 特性 | ESP8266 | ESP32 |
|---------|---------|-------|
| CPU | 单核 80 MHz | 双核 240 MHz |
| RAM | 80 KB | 520 KB |
| WiFi | 2.4 GHz | 2.4 GHz |
| 蓝牙 | 无 | 有（BLE 和经典） |
| GPIO 引脚 | 17 | 34 |
| ADC 通道 | 1（10 位） | 18（12 位） |
| DAC | 无 | 2 通道 |
| PWM | 1 通道 | 16 通道 |
| 价格 | $2-4 | $3-8 |
| 最适合 | 简单 WiFi 项目 | 带蓝牙的复杂 IoT |

### 热门开发板

| 开发板 | 芯片 | 特性 | 最适合 |
|-------|------|----------|----------|
| NodeMCU V3 | ESP8266 | USB、面包板友好 | 初学者 |
| Wemos D1 Mini | ESP8266 | 紧凑、可堆叠扩展 | 小型项目 |
| ESP32 DevKit V1 | ESP32 | USB、多 GPIO | 通用 ESP32 项目 |
| ESP32-S3 | ESP32-S3 | USB OTG、AI 加速 | ML 和摄像头项目 |
| ESP32-C3 | ESP32-C3 | RISC-V、低成本 | 成本敏感项目 |
| ESP32-WROOM | ESP32 | 自定义 PCB 模块 | 生产设计 |
| TTGO T-Display | ESP32 | 内置 LCD 屏幕 | 可视化项目 |
| ESP32-CAM | ESP32 | 摄像头模块 | 视频项目 |
| XIAO ESP32C3 | ESP32-C3 | 超小尺寸 | 可穿戴设备 |

### 购买渠道

| 渠道 | 优点 | 缺点 |
|--------|------|------|
| AliExpress | 最低价格 | 长时间运输 |
| Amazon | 快速配送 | 价格较高 |
| DigiKey | 正品 | 最低订购量 |
| Mouser | 广泛选择 | 运费 |
| Banggood | 好价格 | 运费不定 |

---

## Arduino IDE 设置

### 安装步骤

| 步骤 | 操作 | 详情 |
|------|--------|---------|
| 1 | 安装 Arduino IDE | 从 arduino.cc 下载 |
| 2 | 打开偏好设置 | 文件 > 偏好设置 |
| 3 | 添加开发板 URL | 添加 ESP 开发板管理器 URL |
| 4 | 安装开发板 | 工具 > 开发板 > 开发板管理器 |
| 5 | 选择开发板 | 选择你的 ESP 开发板 |
| 6 | 安装库 | 项目 > 包含库 |

### 开发板管理器 URL

| 开发板 | URL |
|-------|-----|
| ESP8266 | http://arduino.esp8266.com/stable/package_esp8266com_index.json |
| ESP32 | https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json |

### 必备 Arduino 库

| 库 | 用途 |
|---------|---------|
| WiFi.h | WiFi 连接（ESP32） |
| ESP8266WiFi.h | WiFi 连接（ESP8266） |
| PubSubClient | MQTT 客户端 |
| ArduinoJson | JSON 解析和创建 |
| DHT sensor library | 温度和湿度 |
| Adafruit NeoPixel | RGB LED 控制 |
| ESPAsyncWebServer | 异步 Web 服务器 |
| AsyncTCP | ESP32 TCP 库 |
| Wire.h | I2C 通信 |
| SPI.h | SPI 通信 |

### 你的第一个程序

```cpp
// Blink LED on ESP32
#define LED_PIN 2

void setup() {
  Serial.begin(115200);
  pinMode(LED_PIN, OUTPUT);
  Serial.println("ESP32 Ready!");
}

void loop() {
  digitalWrite(LED_PIN, HIGH);
  delay(1000);
  digitalWrite(LED_PIN, LOW);
  delay(1000);
}
```

---

## ESP 上的 MicroPython

MicroPython 让你用 Python 而不是 C++ 来编程 ESP 开发板。

### 安装

| 步骤 | 操作 |
|------|--------|
| 1 | 为你的开发板下载 MicroPython 固件 |
| 2 | 安装 esptool：`pip install esptool` |
| 3 | 擦除闪存：`esptool.py --port /dev/ttyUSB0 erase_flash` |
| 4 | 刷入固件：`esptool.py --port /dev/ttyUSB0 write_flash -z 0x1000 firmware.bin` |
| 5 | 用串口终端或 Thonny IDE 连接 |

### MicroPython vs Arduino

| 特性 | MicroPython | Arduino (C++) |
|---------|-------------|---------------|
| 易用性 | 更简单，Python 语法 | 更复杂 |
| 速度 | 较慢 | 较快 |
| 内存使用 | 较高 | 较低 |
| 库支持 | 增长中 | 丰富 |
| REPL | 交互式 | 无 |
| 最适合 | 原型、教育 | 生产、性能 |

### 基本 MicroPython 示例

```python
# Blink LED
from machine import Pin
import time

led = Pin(2, Pin.OUT)

while True:
    led.on()
    time.sleep(1)
    led.off()
    time.sleep(1)
```

```python
# Connect to WiFi
import network

wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect('SSID', 'PASSWORD')

while not wlan.isconnected():
    pass

print('Connected:', wlan.ifconfig())
```

### Thonny IDE

| 特性 | 优势 |
|---------|---------|
| 内置 MicroPython 支持 | 无需配置 |
| 文件管理器 | 上传文件到 ESP |
| REPL 访问 | 交互式 Python Shell |
| 调试器 | 单步执行代码 |
| 跨平台 | Windows、Mac、Linux |

---

## 传感器

### 温度和湿度

| 传感器 | 接口 | 范围 | 精度 | 价格 |
|--------|-----------|-------|----------|-------|
| DHT11 | 数字 | 0-50C、20-80% | +-2C、+-5% | $1 |
| DHT22 | 数字 | -40-80C、0-100% | +-0.5C、+-2% | $3 |
| BME280 | I2C/SPI | -40-85C、0-100% | +-1C、+-3% | $3 |
| DS18B20 | 1-Wire | -55-125C | +-0.5C | $2 |
| SHT31 | I2C | -40-125C | +-0.3C | $5 |

### 运动和距离

| 传感器 | 类型 | 范围 | 用例 |
|--------|------|-------|----------|
| HC-SR04 | 超声波 | 2-400 cm | 距离测量 |
| PIR (HC-SR501) | 红外 | 3-7 m | 运动检测 |
| VL53L0X | 飞行时间 | 5-200 cm | 精确距离 |
| MPU6050 | 加速度计/陀螺仪 | - | 运动/方向 |
| ADXL345 | 加速度计 | - | 振动/倾斜 |

### 环境

| 传感器 | 测量 | 接口 | 备注 |
|--------|----------|-----------|-------|
| MQ-2 | 气体/烟雾 | 模拟 | 可燃气体 |
| MQ-135 | 空气质量 | 模拟 | CO2、NH3、苯 |
| BH1750 | 光照水平 | I2C | 勒克斯测量 |
| BMP280 | 气压/温度 | I2C/SPI | 气象站 |
| Soil Moisture | 土壤水分 | 模拟 | 植物监测 |
| Rain Sensor | 雨水检测 | 数字/模拟 | 气象站 |

### 完整传感器接线指南

| 传感器 | VCC | GND | 数据引脚 |
|--------|-----|-----|-------------|
| DHT22 | 3.3V | GND | GPIO4 |
| HC-SR04 | 5V | GND | Trig: GPIO5、Echo: GPIO18 |
| BME280 | 3.3V | GND | SDA: GPIO21、SCL: GPIO22 |
| DS18B20 | 3.3V | GND | GPIO4（带 4.7k 上拉） |
| PIR | 5V | GND | GPIO13 |

---

## 执行器

### 电机

| 电机类型 | 驱动 | 用例 |
|-----------|--------|----------|
| 直流电机 | L298N、TB6612 | 轮子、风扇 |
| 舵机 | 直接 PWM | 转向、机械臂 |
| 步进电机 | A4988、DRV8825 | 精确定位 |
| 无刷电机 | ESC | 无人机、高速 |

### 显示屏

| 显示屏 | 接口 | 分辨率 | 最适合 |
|---------|-----------|------------|----------|
| SSD1306 OLED | I2C | 128x64 | 简单文本/图形 |
| ST7789 LCD | SPI | 240x240 | 彩色图形 |
| ILI9341 LCD | SPI | 240x320 | 大彩屏 |
| E-Paper | SPI | 各种 | 低功耗显示 |
| TM1637 | 数字 | 4 位 | 仅数字 |
| MAX7219 | SPI | 8x8 矩阵 | LED 矩阵 |

### 输出设备

| 设备 | 接口 | 用例 |
|--------|-----------|----------|
| WS2812B (NeoPixel) | 数字 | RGB LED 灯带 |
| 蜂鸣器 | PWM/GPIO | 声音提醒 |
| 继电器模块 | GPIO | 开关交流设备 |
| 扬声器 (I2S) | I2S | 音频播放 |

---

## WiFi 项目

### 基本 WiFi 操作

| 操作 | 代码方式 |
|-----------|---------------|
| 扫描网络 | `WiFi.scanNetworks()` |
| 连接 AP | `WiFi.begin(ssid, password)` |
| 创建 AP | `WiFi.softAP(ssid, password)` |
| 获取 IP 地址 | `WiFi.localIP()` |
| HTTP 客户端 | `HTTPClient` 类 |
| Web 服务器 | `WebServer` 或 `AsyncWebServer` |

### Web 服务器示例项目

| 组件 | 描述 |
|-----------|-------------|
| 目的 | 通过 Web 界面控制 GPIO 引脚 |
| 硬件 | ESP32 + LED + 电阻 |
| 软件 | AsyncWebServer 库 |
| 功能 | 切换 LED、读取传感器数据、响应式 UI |

### WiFi 项目创意

| 项目 | 描述 | 难度 |
|---------|-------------|------------|
| 气象站 | 在网页上显示传感器数据 | 初学者 |
| 遥控车 | 通过 Web 界面控制电机 | 中级 |
| WiFi 扫描器 | 检测并显示附近网络 | 初学者 |
| 智能门铃 | 按下按钮时发送通知 | 中级 |
| 文件服务器 | 通过 WiFi 从 SD 卡提供文件 | 中级 |
| OTA 更新器 | 通过 WiFi 更新固件 | 中级 |

---

## 蓝牙项目

### BLE（低功耗蓝牙）

| 组件 | 描述 |
|-----------|-------------|
| BLE 服务器 | 广播服务和特征 |
| BLE 客户端 | 连接并读写服务器 |
| BLE 扫描器 | 发现附近的 BLE 设备 |
| BLE 信标 | 无需连接即可广播数据 |

### 蓝牙项目创意

| 项目 | 描述 | 难度 |
|---------|-------------|------------|
| BLE 信标 | 广播位置信息 | 初学者 |
| 蓝牙音箱 | 通过经典蓝牙流式传输音频 | 高级 |
| BLE 传感器节点 | 将传感器数据发送到手机 | 初学者 |
| 接近锁 | 手机靠近时解锁 | 中级 |
| BLE 网状网络 | 控制多个设备 | 高级 |
| BLE HID 设备 | 模拟键盘或鼠标 | 中级 |

---

## MQTT 和 IoT

### MQTT 基础

| 概念 | 描述 |
|---------|-------------|
| 代理 | 路由消息的服务器（Mosquitto、HiveMQ） |
| 发布者 | 向主题发送消息 |
| 订阅者 | 从主题接收消息 |
| 主题 | 命名的消息通道（如 home/temperature） |
| QoS | 服务质量（0、1 或 2） |
| Retain | 代理为新订阅者保存最后一条消息 |

### 热门 MQTT 代理

| 代理 | 类型 | 最适合 |
|--------|------|----------|
| Mosquitto | 自托管 | 家庭自动化 |
| HiveMQ Cloud | 云 | 生产 IoT |
| Adafruit IO | 云 | 初学者、爱好者 |
| AWS IoT Core | 云 | 企业 IoT |
| ThingsBoard | 自托管/云 | IoT 平台 |

### MQTT 连接示例

```cpp
#include <WiFi.h>
#include <PubSubClient.h>

const char* mqtt_server = "192.168.1.100";
WiFiClient espClient;
PubSubClient client(espClient);

void setup() {
  WiFi.begin("SSID", "PASSWORD");
  client.setServer(mqtt_server, 1883);
  client.setCallback(callback);
}

void callback(char* topic, byte* payload, unsigned int length) {
  // Handle incoming messages
}

void loop() {
  if (!client.connected()) {
    client.connect("ESP32Client");
    client.subscribe("home/command");
  }
  client.loop();
  client.publish("home/temperature", "23.5");
  delay(5000);
}
```

### MQTT 主题设计

| 模式 | 示例 | 用例 |
|---------|---------|----------|
| 位置/设备/传感器 | home/livingroom/temp | 家庭自动化 |
| 设备/状态 | esp32/light/state | 设备状态 |
| 命令/设备 | cmd/light/on | 远程控制 |
| 警报/设备 | alert/smoke/alarm | 通知 |

---

## 家庭自动化

### 平台集成

| 平台 | 协议 | ESP 支持 |
|----------|----------|-------------|
| Home Assistant | MQTT、REST、ESPHome | 优秀 |
| OpenHAB | MQTT、REST | 良好 |
| Tasmota | MQTT、Web | 优秀 |
| ESPHome | 原生 | 优秀 |
| Node-RED | MQTT | 优秀 |

### ESPHome

ESPHome 是将 ESP 设备与 Home Assistant 集成的最简单方式。

| 特性 | 描述 |
|---------|-------------|
| YAML 配置 | 无需编码 |
| 自动发现 | 自动 Home Assistant 集成 |
| OTA 更新 | 无线更新固件 |
| 深度睡眠 | 内置电源管理 |
| 广泛传感器支持 | 100+ 组件 |

### 家庭自动化项目

| 项目 | 组件 | 难度 |
|---------|------------|------------|
| 智能灯 | ESP32 + 继电器 + LED 灯泡 | 初学者 |
| 温度监控 | ESP32 + DHT22 | 初学者 |
| 门窗传感器 | ESP8266 + 磁簧开关 | 初学者 |
| 智能插座 | ESP32 + 继电器 + 电流传感器 | 中级 |
| 车库门 | ESP32 + 继电器 + 限位开关 | 中级 |
| 灌溉系统 | ESP32 + 电磁阀 + 土壤传感器 | 中级 |
| 安防系统 | ESP32 + PIR + 门窗传感器 + 蜂鸣器 | 高级 |
| 智能镜子 | ESP32 + 显示屏 + 传感器 | 高级 |

---

## 可穿戴设备

### 可穿戴硬件

| 开发板 | 尺寸 | 电池 | 最适合 |
|-------|------|---------|----------|
| ESP32-C3 Mini | 极小 | 外接 | 自定义可穿戴 |
| XIAO ESP32C3 | 小 | LiPo | 紧凑项目 |
| ESP32-S3 Mini | 小 | 外接 | 摄像头可穿戴 |
| TTGO T-Watch | 手表形态 | 内置 | 手腕项目 |
| Wemos D1 Mini | 小 | 外接 | 简单可穿戴 |

### 可穿戴项目创意

| 项目 | 组件 | 描述 |
|---------|------------|-------------|
| 计步器 | ESP32 + MPU6050 | 跟踪每日步数 |
| 心率监测 | ESP32 + MAX30102 | 监测脉搏 |
| GPS 追踪 | ESP32 + NEO-6M | 跟踪位置 |
| 跌倒检测 | ESP32 + MPU6050 | 跌倒时报警 |
| 智能徽章 | ESP32-C3 + E-Paper | 显示信息 |
| 睡眠监测 | ESP32 + MPU6050 | 跟踪睡眠质量 |

---

## IoT 项目创意

### 初学者项目

| 项目 | 传感器/组件 | 描述 |
|---------|-------------------|-------------|
| 气象站 | BME280、OLED | 显示温度、湿度、气压 |
| 植物监测 | 土壤湿度、LDR | 监测植物健康 |
| 邮件通知 | 按钮、WiFi | 按下按钮时发送邮件 |
| LED 控制器 | WS2812B、WiFi | 从手机控制 RGB LED |
| 超声波尺 | HC-SR04、OLED | 测量距离 |

### 中级项目

| 项目 | 组件 | 描述 |
|---------|------------|-------------|
| 空气质量监测 | MQ-135、BME280、OLED | 跟踪空气质量指标 |
| 智能锁 | 键盘、舵机、WiFi | 远程控制锁 |
| 能源监测 | CT 传感器、ESP32 | 跟踪电力消耗 |
| 宠物喂食器 | 舵机、RTC、WiFi | 定时喂食 |
| MQTT 仪表板 | 多个传感器 | 集中监控系统 |

### 高级项目

| 项目 | 组件 | 描述 |
|---------|------------|-------------|
| 机器人车 | ESP32、电机、摄像头 | 遥控机器人 |
| 无人机控制器 | ESP32、MPU6050、ESC | 自定义飞行控制器 |
| 网状网络 | 多个 ESP32 | 分布式传感器网络 |
| 边缘 AI | ESP32-S3、摄像头 | 设备端物体检测 |
| 太阳能监测 | ESP32、INA219、太阳能板 | 跟踪太阳能板输出 |

---

## 电源管理

### 功耗

| 模式 | ESP8266 | ESP32 | 描述 |
|------|---------|-------|-------------|
| 活跃（WiFi TX） | 170 mA | 240 mA | 传输数据 |
| 活跃（WiFi 空闲） | 60 mA | 80 mA | 已连接未传输 |
| 轻度睡眠 | 0.5 mA | 0.8 mA | CPU 暂停、WiFi 已连接 |
| 深度睡眠 | 10 uA | 10 uA | 仅 RTC 活跃 |
| 休眠 | 5 uA | 5 uA | 最低功耗 |

### 深度睡眠配置

```cpp
#define uS_TO_S_FACTOR 1000000
#define TIME_TO_SLEEP  300  // 5 minutes

void setup() {
  // Read sensor, send data
  esp_sleep_enable_timer_wakeup(TIME_TO_SLEEP * uS_TO_S_FACTOR);
  esp_deep_sleep_start();
}

void loop() {
  // Never reached in deep sleep
}
```

### 节能技巧

| 技术 | 节省 | 权衡 |
|-----------|---------|-----------|
| 读取间深度睡眠 | 99% | 无响应性 |
| 降低 WiFi 发射功率 | 20-50% | 范围缩短 |
| 使用 BLE 代替 WiFi | 50-80% | 吞吐量降低 |
| 不需要时禁用蓝牙 | 10-20% | 无 |
| 降低 CPU 频率 | 20-30% | 处理变慢 |
| 使用高效传感器 | 不定 | 可能更贵 |

### 电池寿命估算

| 电池 | 深度睡眠（5 分钟唤醒） | 轻度睡眠 | 始终开启 |
|---------|------------------------|-------------|-----------|
| 1000 mAh LiPo | ~30 天 | ~20 小时 | ~4 小时 |
| 2000 mAh LiPo | ~60 天 | ~40 小时 | ~8 小时 |
| 18650 (3000 mAh) | ~90 天 | ~60 小时 | ~12 小时 |
| 10000 mAh USB | ~1 年 | ~200 小时 | ~40 小时 |

### 太阳能供电

| 组件 | 用途 | 备注 |
|-----------|---------|-------|
| 太阳能板 (5V/1W) | 充电 | 需要直射阳光 |
| TP4056 模块 | 充电控制器 | 防止过充 |
| LiPo 电池 (1000+ mAh) | 储能 | 阴天缓冲 |
| 稳压器 | 稳定 3.3V | AMS1117 或类似 |
| 深度睡眠 | 最小化消耗 | 唤醒传输数据 |

---

## 最佳实践

### 代码组织

| 实践 | 描述 |
|----------|-------------|
| 使用 config.h | 分离 WiFi 凭据和设置 |
| 实现 OTA | 启用无线固件更新 |
| 处理错误 | 检查 WiFi 和 MQTT 连接状态 |
| 看门狗定时器 | 挂起时重置 |
| 串口日志 | 调试输出用于排错 |

### 硬件技巧

| 技巧 | 原因 |
|-----|--------|
| 使用去耦电容 | 防止电压尖峰 |
| 添加上拉电阻 | 稳定 I2C 通信 |
| 使用电平转换器 | 3.3V/5V 兼容 |
| 添加复位按钮 | 方便调试 |
| 使用合适电源 | USB 可能供电不足 |

---

## 总结

ESP8266 和 ESP32 是多功能微控制器，让 IoT 对每个人都触手可及。从简单的气象站和 LED 控制器开始，然后逐步过渡到涉及网状网络和边缘 AI 的更复杂系统。

Arduino IDE 提供最简单的入门方式，而 MicroPython 非常适合快速原型开发。ESPHome 是家庭自动化集成的最佳选择。通过适当的电源管理，这些设备可以使用电池运行数月。
