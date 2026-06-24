# Arduino ESP32 教程：开发平台

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
