# MicroPython 编程指南

## 简介

MicroPython 是 Python 3 的精简实现，针对在微控制器和受限环境中运行进行了优化。它将 Python 的易用性带入了硬件编程领域。

### 什么是 MicroPython？

MicroPython 是 Python 3 的完整重新实现，包含标准库的子集，并针对微控制器进行了优化。

| 特性 | 描述 |
|------|------|
| Python 语法 | 完整 Python 3 语法 |
| 交互式 REPL | 实时代码执行 |
| 硬件访问 | GPIO、I2C、SPI、UART |
| 紧凑 | 仅需 256KB flash |
| 可扩展 | C/C++ 集成 |

### 与其他方案的比较

| 特性 | MicroPython | CircuitPython | Arduino |
|------|------------|---------------|---------|
| 语言 | Python | Python | C/C++ |
| 易用性 | 高 | 高 | 中 |
| 性能 | 中 | 中 | 高 |
| 库 | 丰富 | Adafruit 为主 | 丰富 |
| 社区 | 大 | 大 | 非常大 |

## 支持的硬件

### 兼容开发板

| 开发板 | 特性 |
|--------|------|
| ESP32 | WiFi、蓝牙 |
| ESP8266 | WiFi |
| Raspberry Pi Pico | RP2040 |
| BBC micro:bit | 教育 |
| STM32 | 工业 |
| Pyboard | 官方开发板 |

### 开发板比较

| 开发板 | Flash | RAM | WiFi | 价格 |
|--------|-------|-----|------|------|
| ESP32 | 4MB | 520KB | 是 | $5 |
| ESP8266 | 4MB | 160KB | 是 | $3 |
| Pico | 2MB | 264KB | 否 | $4 |
| micro:bit | 256KB | 16KB | 否 | $15 |
| Pyboard | 1MB | 192KB | 否 | $40 |

## 安装

### 安装 MicroPython

```bash
# 从 micropython.org 下载固件
# 刷入开发板

# ESP32
esptool.py --chip esp32 --port /dev/ttyUSB0 erase_flash
esptool.py --chip esp32 --port /dev/ttyUSB0 write_flash -z 0x1000 firmware.bin

# Raspberry Pi Pico
# 连接时按住 BOOTSEL 按钮
# 复制 .uf2 文件到 RPI-RP2 驱动器
```

### 开发工具

| 工具 | 描述 |
|------|------|
| Thonny | 内置支持的 IDE |
| Mu | 简单编辑器 |
| VS Code | 配合 Pymakr 扩展 |
| rshell | 远程 shell |
| ampy | 文件传输 |

### Thonny 设置

1. 安装 Thonny
2. 选择 MicroPython 解释器
3. 选择开发板端口
4. 打开 REPL |

## 基本编程

### Hello World

```python
print("Hello, MicroPython!")
```

### 变量和数据类型

```python
# 数字
x = 42
y = 3.14

# 字符串
name = "MicroPython"

# 列表
items = [1, 2, 3, 4]

# 字典
config = {
    "wifi_ssid": "MyNetwork",
    "wifi_pass": "password"
}
```

### 控制流

```python
# If 语句
if temperature > 30:
    print("Hot!")
elif temperature > 20:
    print("Warm")
else:
    print("Cold")

# For 循环
for i in range(10):
    print(i)

# While 循环
while True:
    do_something()
```

### 函数

```python
def blink(led, times=3):
    for _ in range(times):
        led.on()
        time.sleep(0.5)
        led.off()
        time.sleep(0.5)
```

## 硬件访问

### GPIO 引脚

```python
from machine import Pin
import time

# 创建 LED 对象
led = Pin(2, Pin.OUT)

# 闪烁 LED
while True:
    led.on()
    time.sleep(1)
    led.off()
    time.sleep(1)
```

### 引脚模式

| 模式 | 描述 |
|------|------|
| Pin.OUT | 输出模式 |
| Pin.IN | 输入模式 |
| Pin.PULL_UP | 内部上拉 |
| Pin.PULL_DOWN | 内部下拉 |

### 读取输入

```python
from machine import Pin

# 创建按钮对象
button = Pin(0, Pin.IN, Pin.PULL_UP)

# 读取按钮状态
if button.value() == 0:
    print("Button pressed")
```

### PWM（脉宽调制）

```python
from machine import Pin, PWM
import time

# 创建 PWM 对象
pwm = PWM(Pin(2))
pwm.freq(1000)

# LED 渐变
while True:
    for duty in range(0, 1024):
        pwm.duty(duty)
        time.sleep(0.005)
```

## 传感器

### 温度传感器 (DHT11)

```python
import dht
from machine import Pin

sensor = dht.DHT11(Pin(4))
sensor.measure()

temp = sensor.temperature()
humidity = sensor.humidity()

print(f"Temperature: {temp}°C")
print(f"Humidity: {humidity}%")
```

### 超声波传感器

```python
from machine import Pin, time_pulse_us
import time

trigger = Pin(5, Pin.OUT)
echo = Pin(4, Pin.IN)

def measure_distance():
    trigger.value(0)
    time.sleep_us(2)
    trigger.value(1)
    time.sleep_us(10)
    trigger.value(0)
    
    duration = time_pulse_us(echo, 1)
    distance = (duration * 0.0343) / 2
    return distance
```

### I2C 设备

```python
from machine import I2C, Pin

# 创建 I2C 对象
i2c = I2C(scl=Pin(22), sda=Pin(21))

# 扫描设备
devices = i2c.scan()
print(devices)
```

## 通信

### WiFi 连接

```python
import network
import time

wlan = network.WLAN(network.STA_IF)
wlan.active(True)
wlan.connect("SSID", "password")

while not wlan.isconnected():
    time.sleep(1)

print("Connected!")
print(wlan.ifconfig())
```

### HTTP 请求

```python
import urequests

# GET 请求
response = urequests.get("http://httpbin.org/get")
print(response.json())

# POST 请求
data = {"key": "value"}
response = urequests.post("http://httpbin.org/post", json=data)
print(response.json())
```

### MQTT

```python
from umqtt.simple import MQTTClient

client = MQTTClient("esp32", "broker.example.com")
client.connect()

# 发布
client.publish(b"topic", b"message")

# 订阅
client.set_callback(callback)
client.subscribe(b"topic")
```

### 蓝牙 (ESP32)

```python
import bluetooth

ble = bluetooth.BLE()
ble.active(True)
```

## 文件系统

### 文件操作

```python
# 写入文件
with open("data.txt", "w") as f:
    f.write("Hello, World!")

# 读取文件
with open("data.txt", "r") as f:
    content = f.read()
    print(content)
```

### 文件系统操作

```python
import os

# 列出文件
os.listdir()

# 创建目录
os.mkdir("data")

# 删除文件
os.remove("data.txt")

# 检查文件是否存在
os.stat("data.txt")
```

## 显示

### OLED 显示屏 (SSD1306)

```python
from machine import I2C, Pin
from ssd1306 import SSD1306_I2C

i2c = I2C(scl=Pin(22), sda=Pin(21))
oled = SSD1306_I2C(128, 64, i2c)

oled.fill(0)
oled.text("Hello!", 0, 0)
oled.show()
```

### LCD 显示屏

```python
from machine import I2C, Pin
from lcd_api import LcdApi
from pico_i2c_lcd import I2cLcd

i2c = I2C(0, sda=Pin(0), scl=Pin(1), freq=400000)
lcd = I2cLcd(i2c, 0x27, 2, 16)

lcd.putstr("Hello, World!")
```

## 定时器和中断

### 硬件定时器

```python
from machine import Timer

timer = Timer(0)
timer.init(period=1000, mode=Timer.PERIODIC, callback=lambda t: print("Tick"))
```

### 中断

```python
from machine import Pin

button = Pin(0, Pin.IN, Pin.PULL_UP)

def callback(pin):
    print("Button pressed!")

button.irq(trigger=Pin.IRQ_FALLING, handler=callback)
```

## 电源管理

### 深度睡眠

```python
import machine

# 睡眠 10 秒
machine.deepsleep(10000)
```

### 唤醒源

| 源 | 描述 |
|----|------|
| Timer | 定时唤醒 |
| Pin | 引脚状态唤醒 |
| Touchpad | 触摸唤醒 |

## 库

### 标准库

| 库 | 用途 |
|----|------|
| `machine` | 硬件控制 |
| `network` | WiFi、蓝牙 |
| `time` | 时间函数 |
| `os` | 文件系统 |
| `json` | JSON 解析 |
| `socket` | 网络套接字 |

### 第三方库

| 库 | 用途 |
|----|------|
| `umqtt` | MQTT 客户端 |
| `urequests` | HTTP 请求 |
| `ssd1306` | OLED 显示屏 |
| `dht` | 温度传感器 |
| `onewire` | 1-Wire 协议 |

## 故障排除

### 常见问题

| 问题 | 解决方案 |
|------|----------|
| 内存不足 | 减少变量，使用 gc |
| WiFi 连接失败 | 检查 SSID/密码 |
| 导入错误 | 安装库 |
| REPL 无响应 | 重置开发板 |

### 内存管理

```python
import gc

# 检查内存
gc.mem_free()

# 垃圾回收
gc.collect()
```

## 总结

| 概念 | 描述 |
|------|------|
| GPIO | 控制引脚 |
| 传感器 | 读取传感器数据 |
| WiFi | 连接网络 |
| MQTT | IoT 消息传递 |
| REPL | 交互式编程 |
| 文件 | 存储数据 |
