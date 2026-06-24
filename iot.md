# ESPHome 教程：IoT 固件框架

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
