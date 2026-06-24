# Awesome ESP 项目教程

## 简介

awesome-esp 仓库是 ESP8266 和 ESP32 微控制器的项目、工具和资源精选集合。这些经济实惠、支持 WiFi 的芯片广泛应用于物联网、家庭自动化和嵌入式系统项目。

| 平台 | 描述 |
|----------|-------------|
| ESP8266 | 低成本 WiFi 微控制器，GPIO 有限 |
| ESP32 | 更强大的版本，带蓝牙、更多 GPIO、双核 |
| ESP32-S2 | 单核，带 USB OTG 和更多 GPIO |
| ESP32-S3 | 双核，带 AI 加速和 USB |
| ESP32-C3 | 基于 RISC-V，低成本，BLE 支持 |

## 硬件概述

### ESP8266 开发板

| 开发板 | GPIO | Flash | WiFi | 价格 |
|-------|------|-------|------|-------|
| ESP-01 | 2 | 512KB-4MB | 是 | $2-3 |
| NodeMCU | 10 | 4MB | 是 | $4-6 |
| Wemos D1 Mini | 11 | 4MB | 是 | $3-5 |
| ESP-12E/F | 10 | 4MB | 是 | $2-4 |

### ESP32 开发板

| 开发板 | GPIO | Flash | WiFi | BLE | 价格 |
|-------|------|-------|------|-----|-------|
| ESP32-DevKitC | 34 | 4MB | 是 | 是 | $5-8 |
| ESP32-WROOM-32 | 34 | 4MB | 是 | 是 | $4-6 |
| ESP32-S3-DevKitC | 45 | 8MB | 是 | 是 | $8-12 |
| ESP32-C3-DevKitM | 22 | 4MB | 是 | 是 | $4-6 |
| TTGO T-Display | 20 | 4MB | 是 | 是 | $10-15 |

### 引脚对比

| 特性 | ESP8266 | ESP32 |
|---------|---------|-------|
| CPU | 单核 80MHz | 双核 240MHz |
| RAM | 80KB | 520KB |
| GPIO | 17 | 34 |
| ADC | 1 (10-bit) | 18 (12-bit) |
| PWM | 8 通道 | 16 通道 |
| SPI | 2 | 4 |
| I2C | 1 (软件) | 2 (硬件) |
| UART | 2 | 3 |
| 蓝牙 | 否 | 是（经典 + BLE） |

## 开发环境

### Arduino IDE

| 步骤 | 操作 |
|------|--------|
| 1 | 安装 Arduino IDE |
| 2 | 在偏好设置中添加 ESP 开发板 URL |
| 3 | 通过开发板管理器安装 ESP 开发板包 |
| 4 | 选择开发板和端口 |
| 5 | 上传草图 |

### PlatformIO

| 特性 | 描述 |
|---------|-------------|
| 多平台 | 支持 ESP8266 和 ESP32 |
| 库管理 | 自动依赖处理 |
| 构建系统 | 高级构建配置 |
| IDE 集成 | VS Code、CLion 等 |

### ESP-IDF

| 特性 | 描述 |
|---------|-------------|
| 官方 SDK | Espressif 的官方开发框架 |
| FreeRTOS | 实时操作系统支持 |
| 高级 | 完全控制硬件 |
| 组件 | 模块化组件系统 |

## 项目分类

### 家庭自动化

| 项目 | 描述 | 难度 |
|---------|-------------|------------|
| 智能开关 | 控制灯光和电器 | 初级 |
| 温度监控 | DHT22 传感器带 Web 显示 | 初级 |
| 智能恒温器 | 带定时的温度控制 | 中级 |
| 安防系统 | 运动传感器和告警 | 中级 |
| 智能门铃 | 摄像头和通知系统 | 高级 |

### 物联网传感器

| 项目 | 传感器 | 输出 |
|---------|---------|--------|
| 气象站 | BME280、雨量计 | Web 仪表板 |
| 空气质量监测 | MQ-135、PMS5003 | MQTT 数据 |
| 土壤湿度 | 电容传感器 | 灌溉控制 |
| 能源监测 | CT 钳、电压传感器 | 电力仪表板 |
| 水位 | 超声波传感器 | 告警系统 |

### 通信项目

| 项目 | 协议 | 描述 |
|---------|----------|-------------|
| MQTT 客户端 | MQTT | 物联网消息代理通信 |
| HTTP 服务器 | HTTP | 基于 Web 的控制界面 |
| WebSocket | WebSocket | 实时双向通信 |
| ESP-NOW | ESP-NOW | ESP 之间的点对点通信 |
| 蓝牙 | BLE | 移动设备通信 |

## 网络

### WiFi 配置

```cpp
#include <WiFi.h>

const char* ssid = "your_wifi_ssid";
const char* password = "your_wifi_password";

void setup() {
  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(1000);
  }
  // 已连接 - 打印 IP 地址
  Serial.println(WiFi.localIP());
}
```

### MQTT 通信

```cpp
#include <PubSubClient.h>

const char* mqtt_server = "broker.example.com";
WiFiClient espClient;
PubSubClient client(espClient);

void setup() {
  client.setServer(mqtt_server, 1883);
  client.connect("esp32-client");
  client.publish("sensors/temperature", "25.5");
}
```

### OTA 更新

| 方式 | 描述 |
|--------|-------------|
| ArduinoOTA | 通过网络进行空中更新 |
| HTTP OTA | 从 Web 服务器下载固件 |
| MQTT OTA | 通过 MQTT 消息触发更新 |

## 传感器和模块

### 常用传感器

| 传感器 | 测量 | 接口 | 价格 |
|--------|----------|-----------|-------|
| DHT22 | 温度、湿度 | Digital | $3-5 |
| BME280 | 温度、湿度、气压 | I2C/SPI | $5-10 |
| DS18B20 | 温度 | 1-Wire | $2-4 |
| HC-SR04 | 距离 | Digital | $2-3 |
| PIR | 运动 | Digital | $2-3 |
| BH1750 | 光照 | I2C | $2-4 |
| MPU6050 | 加速度计、陀螺仪 | I2C | $3-5 |
| GPS (NEO-6M) | 位置 | UART | $5-10 |

### 常用模块

| 模块 | 功能 | 接口 |
|--------|----------|-----------|
| 继电器 | 开关大功率设备 | Digital |
| OLED 显示屏 | 小屏幕显示 | I2C |
| SD 卡 | 数据记录存储 | SPI |
| RF 433MHz | 无线通信 | Digital |
| LoRa | 远距离通信 | SPI |
| GPS | 位置追踪 | UART |
| Camera (OV2640) | 图像采集 | DVP |

## 显示项目

### OLED 显示屏

| 显示屏 | 尺寸 | 接口 | 库 |
|---------|------|-----------|---------|
| SSD1306 | 0.96" 128x64 | I2C | Adafruit_SSD1306 |
| SH1106 | 1.3" 128x64 | I2C | U8g2 |
| SSD1351 | 1.5" 128x128 | SPI | Adafruit_SSD1351 |

### TFT 显示屏

| 显示屏 | 尺寸 | 接口 | 库 |
|---------|------|-----------|---------|
| ILI9341 | 2.8" 320x240 | SPI | TFT_eSPI |
| ST7789 | 1.3" 240x240 | SPI | TFT_eSPI |
| ILI9488 | 3.5" 480x320 | SPI | TFT_eSPI |

## 电源管理

### 省电模式

| 模式 | ESP8266 | ESP32 | 唤醒源 |
|------|---------|-------|-------------|
| Active | 全速运行 | 全速运行 | N/A |
| Modem Sleep | CPU 开启，WiFi 关闭 | CPU 开启，WiFi 关闭 | 定时器 |
| Light Sleep | CPU 暂停 | CPU 暂停 | 定时器、GPIO |
| Deep Sleep | 最低功耗 | 最低功耗 | 定时器、GPIO、ULP |
| Hibernation | N/A | 最低功耗 | RTC GPIO、ULP |

### 电池项目

| 项目 | 电池 | 续航 |
|---------|---------|---------|
| 气象站 | 18650 锂电池 | 1-6 个月 |
| 远程传感器 | CR2032 纽扣电池 | 1-3 个月 |
| 太阳能传感器 | LiPo + 太阳能板 | 持续 |
| 便携设备 | LiPo 电池 | 数小时到数天 |

## 库

### 基础库

| 库 | 用途 |
|---------|---------|
| WiFi | WiFi 连接 |
| PubSubClient | MQTT 客户端 |
| AsyncWebServer | 异步 Web 服务器 |
| ArduinoJson | JSON 解析和创建 |
| FastLED | LED 灯带控制 |
| Adafruit_Sensor | 统一传感器接口 |
| Blynk | 物联网平台集成 |
| ESPAsyncWebServer | 异步 HTTP 服务器 |

### 库安装

| 方式 | 描述 |
|--------|-------------|
| Arduino Library Manager | 内置库搜索和安装 |
| PlatformIO | 自动依赖解析 |
| Git clone | 从仓库手动安装 |

## 学习资源

### 文档

| 资源 | 描述 |
|----------|-------------|
| ESP-IDF docs | Espressif 官方文档 |
| Arduino ESP32 | ESP32 的 Arduino 核心 |
| Random Nerd Tutorials | 分步项目指南 |
| Instructables | 社区项目说明 |

### 按难度分类的项目想法

| 难度 | 项目 |
|-----------|----------|
| 初级 | LED 闪烁、WiFi 扫描器、温度显示 |
| 中级 | Web 服务器、MQTT 客户端、传感器仪表板 |
| 高级 | 摄像头流媒体、Mesh 组网、OTA 更新 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 硬件 | 推荐新项目使用 ESP32，因 BLE 和更多 GPIO |
| 开发 | 初学者用 Arduino IDE，高级用户用 PlatformIO |
| 网络 | WiFi、MQTT 和 HTTP 是常见通信方式 |
| 传感器 | 广泛的经济实惠传感器可用 |
| 电源 | Deep Sleep 模式显著延长电池寿命 |
| 社区 | 大型社区，拥有丰富的库和教程 |
