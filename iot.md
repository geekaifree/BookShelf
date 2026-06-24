# IoT 与硬件

> 本文档整合了以下源文件：arduino.md, esp32.md, esp.md, iot.md, pi.md

---

## 来源：arduino.md

## 简介

Arduino 是一个基于易用硬件和软件的开源电子平台。Arduino 开发板从传感器和开关读取输入，并将其转换为电机、灯光和显示器等输出。本教程涵盖 Arduino 生态系统的基础知识。

## 开发板对比

| 开发板 | 处理器 | Flash | 数字 I/O | 模拟输入 | 价格范围 |
|--------|--------|-------|----------|----------|----------|
| Uno | ATmega328P | 32 KB | 14 | 6 | $20-25 |
| Mega | ATmega2560 | 256 KB | 54 | 16 | $35-45 |
| Nano | ATmega328P | 32 KB | 14 | 6 | $15-20 |
| Due | SAM3X8E | 512 KB | 54 | 12 | $35-45 |
| Leonardo | ATmega32u4 | 32 KB | 14 | 12 | $20-25 |
| ESP32 | Xtensa LX6 | 4 MB | 34 | 18 | $5-15 |

## 开发环境

### Arduino IDE

Arduino IDE 是标准开发工具。

| 功能 | 描述 |
|------|------|
| 代码编辑器 | 语法高亮和自动格式化 |
| 开发板管理器 | 安装开发板支持包 |
| 库管理器 | 浏览和安装库 |
| 串口监视器 | 查看开发板输出 |
| 上传 | 编译并上传 sketch 到开发板 |

### Arduino CLI

```bash
# 安装 Arduino CLI
curl -fsSL https://raw.githubusercontent.com/arduino/arduino-cli/master/install.sh | sh

# 安装开发板核心
arduino-cli core install arduino:avr

# 编译 sketch
arduino-cli compile --fqbn arduino:uno MySketch

# 上传到开发板
arduino-cli upload -p /dev/ttyACM0 --fqbn arduino:uno MySketch
```

### Arduino Web Editor

基于浏览器的 IDE，地址为 create.arduino.cc，无需本地安装。

## 基本语法

### Sketch 结构

每个 Arduino 程序（sketch）有两个主要函数。

```cpp
// 开发板启动或复位时运行一次
void setup() {
  // 初始化引脚、串口、库
  pinMode(LED_BUILTIN, OUTPUT);
  Serial.begin(9600);
}

// setup() 完成后重复运行
void loop() {
  // 主程序逻辑
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}
```

### 数据类型

| 类型 | 大小 | 范围 | 使用场景 |
|------|------|------|----------|
| `bool` | 1 字节 | true/false | 标志、开关 |
| `int` | 2 字节 | -32768 到 32767 | 通用整数 |
| `long` | 4 字节 | -2.1B 到 2.1B | 大数值 |
| `float` | 4 字节 | 3.4E+/-38 | 小数 |
| `char` | 1 字节 | -128 到 127 | 字符 |
| `String` | 动态 | 可变 | 文本字符串 |
| `byte` | 1 字节 | 0 到 255 | 小数值 |
| `unsigned int` | 2 字节 | 0 到 65535 | 正整数 |

## 数字 I/O

### 数字输出

```cpp
void setup() {
  pinMode(13, OUTPUT);
}

void loop() {
  digitalWrite(13, HIGH);  // 打开
  delay(500);
  digitalWrite(13, LOW);   // 关闭
  delay(500);
}
```

### 数字输入

```cpp
void setup() {
  pinMode(2, INPUT_PULLUP);
  Serial.begin(9600);
}

void loop() {
  int buttonState = digitalRead(2);
  if (buttonState == LOW) {
    Serial.println("Button pressed");
  }
  delay(100);
}
```

## 模拟 I/O

### 模拟读取

```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  int sensorValue = analogRead(A0);
  float voltage = sensorValue * (5.0 / 1023.0);
  Serial.print("Voltage: ");
  Serial.println(voltage);
  delay(100);
}
```

### 模拟写入（PWM）

```cpp
void setup() {
  // analogWrite 不需要设置
}

void loop() {
  for (int brightness = 0; brightness <= 255; brightness++) {
    analogWrite(9, brightness);
    delay(10);
  }
  for (int brightness = 255; brightness >= 0; brightness--) {
    analogWrite(9, brightness);
    delay(10);
  }
}
```

## 常用组件

| 组件 | 连接方式 | 代码函数 |
|------|----------|----------|
| LED | 数字引脚 + 电阻 | `digitalWrite()` |
| 按钮 | 数字引脚 + 上拉电阻 | `digitalRead()` |
| 电位器 | 模拟引脚 | `analogRead()` |
| 舵机 | 数字引脚 + 电源 | `Servo.write(angle)` |
| 温度传感器（DHT） | 数字引脚 | `DHT.readTemperature()` |
| 超声波 | 两个数字引脚 | `pulseIn()` |
| LCD 显示屏 | I2C 或并行 | `LiquidCrystal_I2C` |

## 通信协议

| 协议 | 引脚 | 速度 | 使用场景 |
|------|------|------|----------|
| UART（串口） | TX、RX | 最高 115200 波特率 | PC 通信 |
| I2C | SDA、SCL | 100-400 kHz | 传感器、显示屏 |
| SPI | MOSI、MISO、SCK、CS | 最高 8 MHz | SD 卡、高速设备 |

### 串口通信

```cpp
void setup() {
  Serial.begin(9600);
}

void loop() {
  if (Serial.available() > 0) {
    char input = Serial.read();
    Serial.print("Received: ");
    Serial.println(input);
  }
}
```

### I2C 通信

```cpp
#include <Wire.h>

void setup() {
  Wire.begin();
  Serial.begin(9600);
}

void loop() {
  Wire.beginTransmission(0x68);  // 设备地址
  Wire.write(0x3B);              // 要读取的寄存器
  Wire.endTransmission(false);
  Wire.requestFrom(0x68, 6);     // 读取 6 字节

  while (Wire.available()) {
    byte data = Wire.read();
    Serial.println(data, HEX);
  }
  delay(500);
}
```

## 库

### 安装库

| 方法 | 步骤 |
|------|------|
| IDE 管理器 | Sketch > Include Library > Manage Libraries |
| CLI | `arduino-cli lib install "LibraryName"` |
| 手动 | 下载 ZIP > Sketch > Include Library > Add .ZIP |

### 常用库

| 库 | 用途 |
|----|------|
| Servo | 控制舵机 |
| Wire | I2C 通信 |
| SPI | SPI 通信 |
| WiFi | WiFi 连接（ESP 开发板） |
| EEPROM | 持久化存储 |
| LiquidCrystal | LCD 显示屏 |
| DHT | 温湿度传感器 |
| FastLED | 可寻址 LED 灯带 |

## 中断

无需轮询即可立即处理外部事件。

```cpp
volatile bool buttonPressed = false;

void buttonISR() {
  buttonPressed = true;
}

void setup() {
  pinMode(2, INPUT_PULLUP);
  attachInterrupt(digitalPinToInterrupt(2), buttonISR, FALLING);
  Serial.begin(9600);
}

void loop() {
  if (buttonPressed) {
    Serial.println("Interrupt triggered!");
    buttonPressed = false;
  }
}
```

## 定时器

| 定时器 | 分辨率 | 默认用途 |
|--------|--------|----------|
| Timer0 | 8 位 | `millis()`、`delay()` |
| Timer1 | 16 位 | Servo 库 |
| Timer2 | 8 位 | Tone 库 |

## 电源管理

| 技术 | 描述 | 节省 |
|------|------|------|
| 睡眠模式 | 降低 CPU 活动 | 最高 99% |
| 禁用 ADC | 关闭模拟转换器 | 约 0.5 mA |
| 禁用外设 | 关闭未使用的硬件 | 视情况而定 |
| 降低时钟频率 | 降低频率 | 成比例 |

## 故障排除

| 问题 | 解决方案 |
|------|----------|
| 上传失败 | 检查端口、开发板类型和数据线 |
| 无串口输出 | 验证波特率与 Serial.begin() 匹配 |
| 读数不稳定 | 添加电容进行噪声滤波 |
| 开发板未识别 | 安装 USB 驱动（CH340、FTDI） |
| 电源不足 | 为电机使用外部电源 |

## 总结

Arduino 平台为嵌入式系统开发提供了便捷的入门途径。从 Uno 开发板和 Arduino IDE 开始，学习数字和模拟 I/O，然后扩展到通信协议、库和电源管理。丰富的扩展板、传感器和库生态系统使其适用于从简单 LED 闪烁到复杂物联网系统的各种项目。


---

## 来源：esp32.md

## 简介

Arduino ESP32 核心为 Espressif 的 ESP32 系列微控制器提供了熟悉的 Arduino 兼容 API。它支持 WiFi、蓝牙和高级外设功能，同时保持了 Arduino 开发框架的简洁性。

## 支持的开发板

| 开发板 | 芯片 | WiFi | BLE | Flash | PSRAM |
|--------|------|------|-----|-------|-------|
| ESP32-DevKitC | ESP32 | 是 | 是 | 4 MB | 可选 |
| ESP32-S3-DevKitC | ESP32-S3 | 是 | 是 | 8 MB | 8 MB |
| ESP32-C3-DevKitC | ESP32-C3 | 是 | 是 | 4 MB | 否 |
| ESP32-S2-Saola | ESP32-S2 | 是 | 否 | 4 MB | 可选 |
| XIAO ESP32-S3 | ESP32-S3 | 是 | 是 | 8 MB | 8 MB |

## 环境搭建

### Arduino IDE 安装

1. 打开 **File > Preferences**
2. 在 Board Manager URLs 中添加：
   ```
   https://espressif.github.io/arduino-esp32/package_esp32_index.json
   ```
3. 打开 **Tools > Board > Boards Manager**
4. 搜索 "esp32" 并安装 **esp32 by Espressif Systems**

### PlatformIO 安装

```ini
; platformio.ini
[env:esp32dev]
platform = espressif32
board = esp32dev
framework = arduino
monitor_speed = 115200
```

## GPIO 参考

### ESP32 引脚功能

| GPIO | ADC | DAC | Touch | PWM | 说明 |
|------|-----|-----|-------|-----|------|
| 0 | ADC2 | 否 | T1 | 是 | 启动按钮，避免使用 |
| 1 | 否 | 否 | 否 | 是 | TX0 串口 |
| 2 | ADC2 | 否 | T2 | 是 | 内置 LED |
| 3 | 否 | 否 | 否 | 是 | RX0 串口 |
| 4 | ADC2 | 否 | T0 | 是 | 推荐使用 |
| 5 | ADC2 | 否 | 否 | 是 | 推荐使用 |
| 12 | ADC2 | 否 | T5 | 是 | 启动敏感 |
| 13 | ADC2 | 否 | T4 | 是 | 推荐使用 |
| 14 | ADC2 | 否 | T6 | 是 | 推荐使用 |
| 15 | ADC2 | 否 | T3 | 是 | 推荐使用 |
| 25 | ADC2 | DAC1 | 否 | 是 | DAC 输出 |
| 26 | ADC2 | DAC2 | 否 | 是 | DAC 输出 |
| 27 | ADC2 | 否 | T7 | 是 | 推荐使用 |
| 32 | ADC1 | 否 | T9 | 是 | 推荐使用 |
| 33 | ADC1 | 否 | T8 | 是 | 推荐使用 |
| 34 | ADC1 | 否 | 否 | 否 | 仅输入 |
| 35 | ADC1 | 否 | 否 | 否 | 仅输入 |
| 36 | ADC1 | 否 | 否 | 否 | 仅输入（VP） |
| 39 | ADC1 | 否 | 否 | 否 | 仅输入（VN） |

## 基本 GPIO 操作

### 数字输入和输出

```cpp
#define LED_PIN 2
#define BUTTON_PIN 4

void setup() {
  Serial.begin(115200);
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
}

void loop() {
  if (digitalRead(BUTTON_PIN) == LOW) {
    digitalWrite(LED_PIN, HIGH);
  } else {
    digitalWrite(LED_PIN, LOW);
  }
  delay(10);
}
```

### 带校准的模拟读取

```cpp
#define SENSOR_PIN 34

void setup() {
  Serial.begin(115200);
  analogReadResolution(12);      // 0-4095 范围
  analogSetAttenuation(ADC_11db); // 0-3.3V 范围
}

void loop() {
  int raw = analogRead(SENSOR_PIN);
  float voltage = raw * 3.3 / 4095.0;
  Serial.printf("Raw: %d, Voltage: %.2fV\n", raw, voltage);
  delay(1000);
}
```

### PWM 输出（LED 调光）

```cpp
#define LED_PIN 2

void setup() {
  ledcSetup(0, 5000, 8);       // 通道 0，5kHz，8 位分辨率
  ledcAttachPin(LED_PIN, 0);
}

void loop() {
  for (int duty = 0; duty <= 255; duty++) {
    ledcWrite(0, duty);
    delay(10);
  }
  for (int duty = 255; duty >= 0; duty--) {
    ledcWrite(0, duty);
    delay(10);
  }
}
```

## WiFi

### Station 模式（连接网络）

```cpp
#include <WiFi.h>

const char* ssid = "MyNetwork";
const char* password = "MyPassword";

void setup() {
  Serial.begin(115200);
  WiFi.begin(ssid, password);

  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }

  Serial.println("\nConnected!");
  Serial.print("IP Address: ");
  Serial.println(WiFi.localIP());
}
```

### 热点模式（Access Point）

```cpp
#include <WiFi.h>

void setup() {
  Serial.begin(115200);
  WiFi.softAP("ESP32-AP", "password123");
  Serial.print("AP IP: ");
  Serial.println(WiFi.softAPIP());
}
```

### WiFi 模式

| 模式 | 常量 | 用途 |
|------|------|------|
| Station | `WIFI_STA` | 连接到现有路由器 |
| Access Point | `WIFI_AP` | 创建自己的网络 |
| Station + AP | `WIFI_AP_STA` | 同时使用两种模式 |

## HTTP 客户端

### GET 请求

```cpp
#include <WiFi.h>
#include <HTTPClient.h>

HTTPClient http;
http.begin("https://api.example.com/data");
int httpCode = http.GET();

if (httpCode == 200) {
  String payload = http.getString();
  Serial.println(payload);
}
http.end();
```

### POST 请求

```cpp
#include <WiFi.h>
#include <HTTPClient.h>

HTTPClient http;
http.begin("https://api.example.com/submit");
http.addHeader("Content-Type", "application/json");

String json = "{\"temperature\": 25.5, \"humidity\": 60}";
int httpCode = http.POST(json);
Serial.printf("Response: %d\n", httpCode);
http.end();
```

## Web 服务器

```cpp
#include <WiFi.h>
#include <WebServer.h>

WebServer server(80);

void handleRoot() {
  server.send(200, "text/plain", "Hello from ESP32!");
}

void handleNotFound() {
  server.send(404, "text/plain", "Not Found");
}

void setup() {
  WiFi.begin("SSID", "PASSWORD");
  while (WiFi.status() != WL_CONNECTED) delay(500);

  server.on("/", handleRoot);
  server.onNotFound(handleNotFound);
  server.begin();
}

void loop() {
  server.handleClient();
}
```

## 经典蓝牙（Bluetooth Classic）

```cpp
#include "BluetoothSerial.h"

BluetoothSerial SerialBT;

void setup() {
  Serial.begin(115200);
  SerialBT.begin("ESP32-BT");
  Serial.println("Bluetooth started. Pair with 'ESP32-BT'");
}

void loop() {
  if (SerialBT.available()) {
    char c = SerialBT.read();
    Serial.write(c);
  }
  if (Serial.available()) {
    char c = Serial.read();
    SerialBT.write(c);
  }
}
```

## BLE（低功耗蓝牙）

```cpp
#include <BLEDevice.h>
#include <BLEServer.h>
#include <BLEUtils.h>
#include <BLE2902.h>

#define SERVICE_UUID "12345678-1234-1234-1234-123456789abc"
#define CHAR_UUID    "abcdefab-1234-1234-1234-abcdefabcdef"

BLECharacteristic *pCharacteristic;

void setup() {
  BLEDevice::init("ESP32-BLE");
  BLEServer *pServer = BLEDevice::createServer();
  BLEService *pService = pServer->createService(SERVICE_UUID);

  pCharacteristic = pService->createCharacteristic(
    CHAR_UUID,
    BLECharacteristic::PROPERTY_READ |
    BLECharacteristic::PROPERTY_WRITE
  );

  pCharacteristic->setValue("Hello BLE");
  pService->start();

  BLEAdvertising *pAdvertising = BLEDevice::getAdvertising();
  pAdvertising->addServiceUUID(SERVICE_UUID);
  pAdvertising->start();
```

## 深度睡眠

```cpp
#define uS_TO_S 1000000

void setup() {
  Serial.begin(115200);
  Serial.println("Waking up...");

  // 在此处执行传感器读取或任务

  Serial.println("Going to sleep...");
  esp_deep_sleep(60 * uS_TO_S); // 休眠 60 秒
}

void loop() {
  // 深度睡眠模式下永远不会执行
}
```

### 睡眠模式对比

| 睡眠模式 | 唤醒源 | 功耗 | RAM 保留 |
|---------|--------|------|---------|
| Active（活跃） | N/A | ~80 mA | 全部 |
| Modem Sleep（调制解调器睡眠） | 定时器 | ~20 mA | 全部 |
| Light Sleep（轻度睡眠） | 定时器, GPIO | ~0.8 mA | 全部 |
| Deep Sleep（深度睡眠） | 定时器, GPIO, Touch | ~10 uA | 仅 RTC |

## OTA（空中更新）

```cpp
#include <ArduinoOTA.h>

void setup() {
  ArduinoOTA.setHostname("esp32-device");
  ArduinoOTA.setPassword("otapassword");

  ArduinoOTA.onStart([]() {
    Serial.println("OTA Update Starting");
  });

  ArduinoOTA.onEnd([]() {
    Serial.println("\nOTA Update Complete");
  });

  ArduinoOTA.begin();
}

void loop() {
  ArduinoOTA.handle();
}
```

## 内存类型

| 内存类型 | ESP32 大小 | 用途 |
|---------|-----------|------|
| Flash | 4 MB | 程序存储 |
| SRAM | 520 KB | 变量和堆 |
| PSRAM | 0-8 MB | 扩展堆内存 |
| RTC SRAM | 8 KB | 深度睡眠数据保留 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 掉电复位 | 电源供应不足 | 使用更好的 USB 线或外部电源 |
| Panic handler | 代码崩溃或异常 | 检查串口监视器输出 |
| WiFi 无法连接 | 凭据错误或信号弱 | 验证 SSID 和密码，靠近路由器 |
| GPIO 不工作 | 启动引脚冲突 | 避免使用 GPIO 0、2 和 12 |
| ADC 不准确 | 非线性响应 | 使用 ESP32 ADC 校准 API |

## 总结

Arduino ESP32 平台为 ESP32 微控制器提供了全面的开发环境。其对 WiFi、蓝牙和众多外设的支持，使其适用于从简单传感器节点到复杂联网设备的各种 IoT 和嵌入式应用。


---

## 来源：esp.md

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


---

## 来源：iot.md

## 简介

ESPHome 是一个通过 YAML 配置文件控制 ESP32 和 ESP8266 微控制器的系统。它与 Home Assistant 深度集成，提供了一种声明式的 IoT 固件开发方式，无需编写 C++ 代码。

## 支持的硬件

| 芯片 | RAM | Flash | WiFi | 蓝牙 | 价格范围 |
|------|-----|-------|------|------|---------|
| ESP32 | 520 KB | 4 MB | 是 | 是 | $3-5 |
| ESP32-S2 | 320 KB | 4 MB | 是 | 否 | $2-4 |
| ESP32-S3 | 512 KB | 4-16 MB | 是 | 是 | $3-6 |
| ESP32-C3 | 400 KB | 4 MB | 是 | 是 | $2-3 |
| ESP8266 | 80 KB | 4 MB | 是 | 否 | $1-3 |

## 安装

### Python 安装

```bash
pip install esphome
```

### Docker 安装

```bash
docker pull ghcr.io/esphome/esphome:latest
docker run --rm -p 6052:6052 -v ./config:/config \
  ghcr.io/esphome/esphome:latest
```

### Dashboard 模式

```bash
esphome dashboard config/
```

在 `http://localhost:6052` 访问 Web 控制面板，以可视化方式管理设备。

## 配置结构

### 最小配置

```yaml
esphome:
  name: living-room-sensor
  platform: ESP32
  board: esp32dev

wifi:
  ssid: "MyNetwork"
  password: "mypassword"

api:
  encryption:
    key: "your-encryption-key"

ota:
  password: "your-ota-password"

logger:
```

### 配置块

| 配置块 | 用途 | 必需 |
|--------|------|------|
| `esphome` | 设备名称和平台 | 是 |
| `wifi` | WiFi 网络凭据 | 是 |
| `api` | Home Assistant API 连接 | 可选 |
| `ota` | 空中更新支持 | 推荐 |
| `logger` | 串口日志输出 | 推荐 |
| `web_server` | 内置 Web 管理界面 | 可选 |
| `bluetooth_proxy` | Home Assistant BLE 代理 | 可选 |

## 组件参考

### 传感器平台

| 平台 | 传感器类型 | 接口 |
|------|-----------|------|
| `dht` | 温湿度 | 1-Wire |
| `dallas` | DS18B20 温度 | 1-Wire |
| `bme280` | 温度/湿度/气压 | I2C 或 SPI |
| `bh1750` | 光照强度（lux） | I2C |
| `hcsr501` | 运动检测 | GPIO |
| `adc` | 模拟电压读数 | ADC 引脚 |
| `ultrasonic` | 距离测量 | GPIO trigger/echo |

### 二进制传感器平台

| 平台 | 类型 | 用途 |
|------|------|------|
| `gpio` | 数字输入 | 门窗磁性开关 |
| `status` | 设备在线状态 | 连接监控 |
| `template` | 计算布尔值 | 由其他传感器派生 |
| `homeassistant` | Home Assistant 状态 | 跨设备逻辑 |
| `mqtt_subscribe` | MQTT 消息 | 远程状态监控 |

### 输出平台

| 平台 | 类型 | 用途 |
|------|------|------|
| `gpio` | 数字开/关 | 继电器控制、LED 切换 |
| `ledc` | PWM 信号 | LED 调光、电机调速 |
| `dac` | 模拟电压 | 电压输出 |
| `pca9685` | 16 通道 PWM | 舵机或 LED 控制 |

### 显示平台

| 平台 | 显示类型 | 接口 |
|------|---------|------|
| `ssd1306` | OLED 128x64 | I2C |
| `st7789v` | 彩色 TFT | SPI |
| `lcd_pcf8574` | 字符 LCD 16x2/20x4 | I2C |
| `nextion` | 触摸屏 TFT | UART |

## GPIO 引脚参考（ESP32）

| 引脚 | ADC | PWM | 输入 | 输出 | 说明 |
|------|-----|-----|------|------|------|
| GPIO0 | 否 | 是 | 是 | 是 | 启动按钮，避免使用 |
| GPIO2 | 否 | 是 | 是 | 是 | 多数开发板的内置 LED |
| GPIO4 | 是 | 是 | 是 | 是 | 安全使用 |
| GPIO5 | 否 | 是 | 是 | 是 | 安全使用 |
| GPIO13 | 是 | 是 | 是 | 是 | 安全使用 |
| GPIO14 | 是 | 是 | 是 | 是 | 安全使用 |
| GPIO25 | 是 | 是 | 是 | 是 | DAC1 输出 |
| GPIO26 | 是 | 是 | 是 | 是 | DAC2 输出 |
| GPIO27 | 是 | 是 | 是 | 是 | 安全使用 |
| GPIO32 | 是 | 是 | 是 | 是 | ADC1，安全使用 |
| GPIO33 | 是 | 是 | 是 | 是 | ADC1，安全使用 |
| GPIO34 | 是 | 否 | 是 | 否 | 仅输入 |
| GPIO35 | 是 | 否 | 是 | 否 | 仅输入 |
| GPIO36 | 是 | 否 | 是 | 否 | 仅输入（VP） |
| GPIO39 | 是 | 否 | 是 | 否 | 仅输入（VN） |

## 传感器配置示例

### DHT22 温湿度传感器

```yaml
sensor:
  - platform: dht
    model: DHT22
    pin: GPIO4
    temperature:
      name: "Room Temperature"
      filters:
        - offset: -1.5
    humidity:
      name: "Room Humidity"
    update_interval: 30s
```

### Dallas DS18B20 防水传感器

```yaml
dallas:
  - pin: GPIO5

sensor:
  - platform: dallas
    address: 0x1234567890ABCDEF
    name: "Water Temperature"
```

### BH1750 环境光传感器

```yaml
sensor:
  - platform: bh1750
    address: 0x23
    name: "Light Level"
    update_interval: 10s
    unit_of_measurement: "lx"
```

## 开关和继电器控制

```yaml
switch:
  - platform: gpio
    name: "Living Room Light"
    pin: GPIO18
    inverted: false
    restore_mode: RESTORE_DEFAULT_OFF

  - platform: template
    name: "Auto Mode"
    optimistic: yes
    turn_on_action:
      - switch.turn_on: relay_1
    turn_off_action:
      - switch.turn_off: relay_1
```

## 设备端自动化

```yaml
automation:
  - id: temp_high_fan_on
    trigger:
      platform: numeric_state
      sensor_id: temperature_sensor
      above: 28.0
    action:
      - switch.turn_on: fan_switch

  - id: motion_light
    trigger:
      platform: state
      binary_sensor_id: motion_sensor
      to: "on"
    action:
      - light.turn_on: room_light
        brightness: 80%
      - delay: 5min
      - light.turn_off: room_light
```

### 触发器类型

| 触发器 | 用途 | 示例 |
|--------|------|------|
| `numeric_state` | 温度、湿度阈值 | 高于 28 度 |
| `state` | 二进制传感器变化 | 检测到运动 |
| `time` | 基于计划的操作 | 上午 8:00 |
| `interval` | 定期操作 | 每 10 分钟 |
| `gpio` | 引脚状态变化 | 按钮按下 |
| `shutdown` | 设备关机 | 保存状态 |

## 深度睡眠（电池设备）

```yaml
deep_sleep:
  run_duration: 30s
  sleep_duration: 10min
  wakeup_pin: GPIO33
  wakeup_pin_mode: KEEP_AWAKE
```

| 模式 | 功耗 | 唤醒时间 | 用途 |
|------|------|---------|------|
| 活跃 | ~80 mA | 即时 | 常开传感器 |
| 轻度睡眠 | ~10 mA | 快速 | 频繁唤醒的电池设备 |
| 深度睡眠 | ~10 uA | 完全重启 | 太阳能或纽扣电池传感器 |

## OTA 更新

```yaml
ota:
  platform: esphome
  password: "my-ota-password"
  safe_mode: true
```

| 方法 | 要求 | 速度 |
|------|------|------|
| USB | 物理接入开发板 | 快 |
| OTA | 与设备在同一网络 | 中等 |
| Dashboard | ESPHome Web 界面 | 中等 |

## 数据过滤器

| 过滤器 | 用途 | 示例 |
|--------|------|------|
| `offset` | 校准调整 | `- 1.5` |
| `multiply` | 缩放因子 | `* 1.1` |
| `median` | 降噪 | 5 个读数的窗口 |
| `sliding_window_moving_average` | 平滑处理 | 10 个读数的窗口 |
| `throttle` | 速率限制 | `60s` |
| `debounce` | 消抖 | `5s` |
| `lambda` | 自定义转换 | 任意表达式 |

## 密钥管理

```yaml
# secrets.yaml（永远不要提交到版本控制）
wifi_ssid: "MyNetwork"
wifi_password: "securepassword"
ota_password: "otapassword"
api_key: "base64encodedkey"
```

```yaml
# device.yaml
wifi:
  ssid: !secret wifi_ssid
  password: !secret wifi_password
```

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 无法连接 WiFi | 凭据错误 | 验证 SSID 和密码 |
| 编译错误 | 无效的 YAML 语法 | 检查缩进 |
| 传感器无数据 | GPIO 引脚错误 | 验证引脚号 |
| OTA 更新失败 | 网络连接问题 | 改用 USB 上传 |
| 功耗过高 | 未配置睡眠 | 添加 deep_sleep 组件 |

## 总结

ESPHome 提供了一个声明式框架，用于创建无需编程的 IoT 固件。其基于 YAML 的配置、丰富的组件库和与 Home Assistant 的无缝集成，使其成为智能家居传感器和自动化项目的理想选择。


---

## 来源：pi.md

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


---
