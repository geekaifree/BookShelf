# Awesome Home Assistant 教程：智能家居搭建

## 简介

Home Assistant 是一个开源家庭自动化平台，以本地控制和隐私为先。本教程涵盖了 awesome-home-assistant 社区的核心资源、集成和最佳实践，用于构建全面的智能家居系统。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| CPU | 双核 ARM | 四核 x86_64 |
| 内存 | 2 GB | 4 GB |
| 存储 | 32 GB SSD | 128 GB SSD |
| 网络 | WiFi | 优先有线网络 |
| 电源 | 稳定 5V（树莓派） | UPS 保护 |

## 安装方式

| 方式 | 平台 | 难度 | 插件支持 |
|------|------|------|---------|
| HAOS | 专用硬件 | 简单 | 完全支持 |
| Container | 任意操作系统上的 Docker | 中等 | 手动管理 |
| Core | Python venv | 困难 | 手动管理 |
| Supervised | Debian Linux | 中等 | 完全支持 |

### Docker 安装

```yaml
version: '3.8'
services:
  homeassistant:
    image: ghcr.io/home-assistant/home-assistant:stable
    volumes:
      - ./config:/config
      - /etc/localtime:/etc/localtime:ro
    restart: unless-stopped
    network_mode: host
    privileged: true
```

## 核心集成

### Hub 集成

| 集成 | 协议 | 支持的设备 |
|------|------|-----------|
| Zigbee (ZHA) | Zigbee | 传感器、开关、灯 |
| Z-Wave JS | Z-Wave | 门锁、恒温器、传感器 |
| MQTT | MQTT | 自定义 IoT 设备 |
| ESPHome | WiFi | ESP32/ESP8266 设备 |
| Matter | Matter/Thread | 新智能家居标准 |
| Thread | Thread | 低功耗网状网络设备 |

### 热门设备集成

| 品牌 | 类别 | 本地控制 |
|------|------|---------|
| Philips Hue | 照明 | 是（通过桥接） |
| Shelly | 开关、继电器 | 是（直接） |
| Sonoff | 开关、传感器 | 是（通过 ESPHome） |
| Tuya | 各种 | 取决于设备 |
| Xiaomi | 传感器、扫地机器人 | 部分 |
| TP-Link | 开关、灯泡 | 是 |
| Sonos | 音频 | 是 |
| Chromecast | 媒体 | 是 |
| Apple HomeKit | 各种 | 是（通过桥接） |

## 自动化基础

### 自动化结构

| 组件 | 说明 | 必需 |
|------|------|------|
| Trigger（触发器） | 启动自动化的内容 | 是 |
| Condition（条件） | 执行前的额外检查 | 否 |
| Action（操作） | 触发时执行的操作 | 是 |

### 触发器类型

| 触发器 | 示例 | 说明 |
|--------|------|------|
| State（状态） | 灯亮起 | 设备状态变化 |
| Time（时间） | 07:00 | 特定时间 |
| Sun（日出日落） | 日落 - 30 分钟 | 太阳事件 |
| Numeric State（数值状态） | 温度超过 25 | 阈值跨越 |
| Zone（区域） | 进入家庭区域 | 地理围栏 |
| MQTT | 接收到主题 | MQTT 消息 |
| Webhook | 外部调用 | HTTP 请求 |
| Device（设备） | 检测到运动 | 设备特定事件 |

### 自动化示例

```yaml
automation:
  - alias: "Turn on porch light at sunset"
    trigger:
      platform: sun
      event: sunset
      offset: "-00:30:00"
    condition:
      condition: state
      entity_id: binary_sensor.someone_home
      state: "on"
    action:
      service: light.turn_on
      target:
        entity_id: light.porch
      data:
        brightness_pct: 80
```

## 仪表板（Lovelace）

### 卡片类型

| 卡片 | 用途 | 最佳场景 |
|------|------|---------|
| Entities | 实体列表 | 快速状态概览 |
| Picture Elements | 带叠加层的图片 | 平面图视图 |
| History Graph | 时间序列图表 | 传感器趋势 |
| Map | 地理视图 | 设备位置 |
| Media Control | 播放控制 | 娱乐 |
| Thermostat | 气候控制 | 温度设置 |
| Weather Forecast | 天气显示 | 室外条件 |
| Gauge | 单值显示 | 指标监控 |
| Button | 单个操作 | 快速控制 |

### 仪表板策略

| 策略 | 布局 | 用途 |
|------|------|------|
| 按房间 | 每个房间一个标签 | 基于房间的控制 |
| 按功能 | 每个功能一个标签 | 照明、气候、安防 |
| 概览 | 单页 | 小型配置 |
| 平面图 | Picture Elements | 可视化导航 |

## ESPHome 设备示例

### 温湿度传感器

```yaml
esphome:
  name: bedroom-sensor

sensor:
  - platform: dht
    pin: GPIO4
    model: DHT22
    temperature:
      name: "Bedroom Temperature"
    humidity:
      name: "Bedroom Humidity"
    update_interval: 60s
```

### 智能继电器开关

```yaml
esphome:
  name: garage-door

switch:
  - platform: gpio
    name: "Garage Door"
    pin: GPIO5
    icon: "mdi:garage"
```

## 推荐硬件

### 控制器

| 设备 | 协议 | 价格 | 范围 |
|------|------|------|------|
| Sonoff Zigbee 3.0 Dongle Plus | Zigbee | $15 | 30m |
| Zooz ZST39 Z-Wave Stick | Z-Wave | $35 | 30m |
| Raspberry Pi 4 | 所有（通过 USB） | $45 | N/A |
| Home Assistant Yellow | Zigbee + Thread | $120 | 内置 |
| Home Assistant Green | 所有（通过 USB） | $90 | N/A |

### 传感器

| 传感器 | 协议 | 用途 | 价格 |
|--------|------|------|------|
| Aqara Motion P1 | Zigbee | 运动检测 | $20 |
| Aqara Door Sensor | Zigbee | 门窗开关 | $15 |
| Sonoff SNZB-02 | Zigbee | 温湿度 | $10 |
| Shelly H&T | WiFi | 温湿度 | $20 |
| Aqara Water Leak | Zigbee | 水浸检测 | $15 |

### 开关和灯

| 设备 | 协议 | 类型 | 价格 |
|------|------|------|------|
| Shelly Plus 1 | WiFi | 继电器 | $13 |
| Shelly Plus 2PM | WiFi | 双继电器 + 功率 | $20 |
| Sonoff Mini R4 | WiFi | 继电器 | $10 |
| IKEA TRADFRI | Zigbee | 灯泡和遥控器 | $10-30 |
| Inovelli Blue | Zigbee | 智能开关 | $30 |

## 能源管理

### 能源仪表板设置

| 组件 | 必需 | 用途 |
|------|------|------|
| 电网传感器 | 是 | 测量电网消耗 |
| 太阳能传感器 | 可选 | 测量太阳能发电 |
| 电池传感器 | 可选 | 追踪电池储能 |
| 独立电表 | 可选 | 按设备追踪 |

### 能源监控硬件

| 设备 | 测量内容 | 协议 |
|------|---------|------|
| Shelly EM | 全屋 | WiFi |
| Emporia Vue | 电路级 | WiFi |
| CT 钳 | 电流 | 模拟/ESPHome |
| Shelly Plug S | 每个插座 | WiFi |

## 语音助手

| 选项 | 本地 | 云 | 隐私 |
|------|------|-----|------|
| Assist (HA) | 是 | 否 | 高 |
| Alexa | 否 | 是 | 低 |
| Google Home | 否 | 是 | 低 |
| Wyoming | 是 | 否 | 高 |
| ESP32 S3 Box | 是 | 否 | 高 |

### Assist 管道设置

1. 安装 Whisper 用于语音转文字
2. 安装 Piper 用于文字转语音
3. 在设置中配置 Assist 管道
4. 设置语音卫星（ESP32 或手机）

## 通知

### 通知渠道

| 渠道 | 方法 | 用途 |
|------|------|------|
| 移动应用 | 推送通知 | 个人提醒 |
| 持久通知 | 仪表板通知 | 应用内提醒 |
| 邮件 | SMTP | 详细报告 |
| Telegram | Bot API | 群组通知 |
| Discord | Webhook | 社区提醒 |
| ntfy | HTTP | 简单推送 |

### 通知自动化示例

```yaml
automation:
  - alias: "Notify on water leak"
    trigger:
      platform: state
      entity_id: binary_sensor.water_leak
      to: "on"
    action:
      service: notify.mobile_app
      data:
        title: "Water Leak Detected!"
        message: "Water leak sensor triggered in basement"
        data:
          priority: high
```

## 安全建议

| 措施 | 实现方式 |
|------|---------|
| HTTPS | 使用 SSL 的反向代理 |
| VPN | WireGuard 或 Tailscale 用于远程访问 |
| MFA | 在用户设置中启用 TOTP |
| 更新 | 保持 HA 和插件最新 |
| 密钥 | 使用 secrets.yaml 存储凭据 |
| 网络 | 将 IoT 隔离在独立 VLAN |

## 备份策略

| 组件 | 方法 | 频率 |
|------|------|------|
| HA 配置 | 内置快照 | 每周 |
| 数据库 | Recorder 备份 | 每日 |
| 插件 | 包含在快照中 | 每周 |
| ESPHome 配置 | Git 仓库 | 更改时 |
| 自动化 | Git 仓库 | 更改时 |

## 实用社区资源

| 资源 | 类型 | URL |
|------|------|-----|
| 社区论坛 | 讨论 | community.home-assistant.io |
| Blueprints Exchange | 共享自动化 | 社区论坛 |
| HACS | 自定义组件 | hacs.xyz |
| ESPHome 文档 | 设备配置 | esphome.io |
| HA Discord | 实时聊天 | Discord 服务器 |

## 总结

Home Assistant 提供了一个强大的、以隐私为先的家庭自动化平台。结合合适的硬件、集成和来自 awesome-home-assistant 的社区资源，它能够实现全面的智能家居控制，支持本地处理和广泛的自定义选项。
