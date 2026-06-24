# Arduino：Arduino 平台入门

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
