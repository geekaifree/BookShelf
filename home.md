# Home Assistant - 完整指南

## 目录

- [简介](#简介)
- [安装方式](#安装方式)
- [初始设置](#初始设置)
- [集成](#集成)
- [自动化](#自动化)
- [仪表盘](#仪表盘)
- [设备和实体](#设备和实体)
- [ESPHome](#esphome)
- [Zigbee](#zigbee)
- [Z-Wave](#z-wave)
- [语音控制](#语音控制)
- [能源监控](#能源监控)
- [技巧和最佳实践](#技巧和最佳实践)

---

## 简介

Home Assistant 是一个开源家庭自动化平台，将本地控制和隐私放在首位。它支持数千种设备和服务。

### 主要功能

| 功能 | 说明 |
|---------|-------------|
| 本地控制 | 无需互联网即可工作 |
| 隐私 | 数据留在家中 |
| 自动化 | 强大的自动化引擎 |
| 集成 | 2000+ 设备集成 |
| 仪表盘 | 可定制的 UI |
| 语音控制 | Assist 语音助手 |
| 移动应用 | iOS 和 Android 应用 |
| 社区 | 庞大、活跃的社区 |

### 要求

| 要求 | 最低 | 推荐 |
|-------------|---------|-------------|
| RAM | 2GB | 4GB |
| 存储 | 32GB | 64GB+ |
| CPU | 2 核 | 4 核 |
| 网络 | 有线 | 有线 |

---

## 安装方式

### 对比

| 方式 | 说明 | 优点 | 缺点 |
|--------|-------------|------|------|
| HAOS | 完整操作系统 | 最简单、功能完整 | 需要专用硬件 |
| 容器 | Docker 容器 | 灵活、轻量 | 无插件、手动更新 |
| Core | Python 安装 | 完全控制 | 配置复杂 |
| Supervised | 在现有系统上运行 HAOS | 现有系统上使用插件 | 复杂、要求严格 |

### Home Assistant OS (HAOS)

**支持的硬件：**

| 设备 | 备注 |
|--------|-------|
| Raspberry Pi 4 | 流行、实惠 |
| Raspberry Pi 5 | 性能更好 |
| Intel NUC | 性能强、可靠 |
| Odroid | 性能好 |
| 通用 x86-64 | 任何 PC |
| 虚拟机 | Proxmox、VirtualBox、VMware |

**在 Raspberry Pi 上安装：**

1. 从 home-assistant.io 下载 HAOS 镜像
2. 使用 Balena Etcher 刷入 SD 卡
3. 将 SD 卡插入 Pi
4. 连接网线和电源
5. 访问 `http://homeassistant.local:8123`

**在 Docker 中安装：**

    docker run -d \
      --name homeassistant \
      --privileged \
      --restart unless-stopped \
      -v /path/to/config:/config \
      -v /run/dbus:/run/dbus:ro \
      --network=host \
      ghcr.io/home-assistant/home-assistant:stable

### Docker Compose

    version: '3'

    services:
      homeassistant:
        image: ghcr.io/home-assistant/home-assistant:stable
        container_name: homeassistant
        privileged: true
        restart: unless-stopped
        volumes:
          - ./config:/config
          - /run/dbus:/run/dbus:ro
        network_mode: host
        environment:
          - TZ=UTC

---

## 初始设置

### 首次启动

1. 访问 `http://homeassistant.local:8123`
2. 创建管理员账户
3. 设置家庭位置
4. 配置单位（公制/英制）
5. 允许自动发现设备

### 基本设置

| 设置 | 位置 | 用途 |
|---------|----------|---------|
| 家庭位置 | 设置 > 区域 | 天气、日出日落 |
| 时区 | 设置 > 系统 | 正确时间 |
| 货币 | 设置 > 系统 | 能源监控 |
| 语言 | 设置 > 系统 | 界面语言 |
| 单位 | 设置 > 系统 | 公制或英制 |

### 创建区域

按物理位置组织设备：

| 区域 | 示例设备 |
|------|-----------------|
| 客厅 | 灯、电视、温控器 |
| 卧室 | 灯、风扇、窗帘 |
| 厨房 | 灯、电器 |
| 卫生间 | 灯、风扇、湿度传感器 |
| 车库 | 门、灯、摄像头 |
| 花园 | 喷灌器、灯、传感器 |

---

## 集成

集成将 Home Assistant 连接到设备和服务。

### 常用集成

| 集成 | 设备/服务 |
|-------------|------------------|
| Philips Hue | Hue 灯和桥接器 |
| Google Home | Google 音箱、显示器 |
| Amazon Alexa | Echo 设备 |
| Shelly | Shelly 继电器和传感器 |
| Tuya | Tuya/Smart Life 设备 |
| Xiaomi | 小米智能设备 |
| Sonoff | Sonoff 设备 |
| MQTT | MQTT 设备 |
| Zigbee (ZHA) | Zigbee 设备 |
| Z-Wave | Z-Wave 设备 |
| ESPHome | ESPHome 设备 |

### 添加集成

1. 进入设置 > 设备与服务
2. 点击"添加集成"
3. 搜索集成
4. 按向导操作

### 集成类型

| 类型 | 说明 | 示例 |
|------|-------------|---------|
| 本地 | 直接连接 | Shelly、ESPHome |
| 云 | 通过云服务 | Google、Alexa |
| 集线器 | 通过集线器/网关 | Hue、SmartThings |
| 协议 | 直接协议 | MQTT、Zigbee |

### MQTT 集成

MQTT 是物联网中流行的消息协议。

    # configuration.yaml
    mqtt:
      broker: 192.168.1.100
      port: 1883
      username: mqtt_user
      password: mqtt_password

**MQTT 代理选项：**

| 代理 | 说明 |
|--------|-------------|
| Mosquitto | 最流行、轻量 |
| EMQX | 企业功能 |
| HiveMQ | 云选项 |
| 内置 | HA 自带代理 |

---

## 自动化

自动化根据条件触发操作。

### 自动化结构

    automation:
      - alias: "Turn on lights at sunset"
        trigger:
          - platform: sun
            event: sunset
            offset: "-00:30:00"
        condition:
          - condition: state
            entity_id: person.me
            state: home
        action:
          - service: light.turn_on
            target:
              entity_id: light.living_room
            data:
              brightness: 255

### 触发器

| 触发器类型 | 说明 | 示例 |
|--------------|-------------|---------|
| State | 实体状态变化 | 灯亮了 |
| Time | 特定时间 | 上午 7:00 |
| Sun | 日出/日落 | 日落 |
| Device | 设备事件 | 门打开 |
| Numeric | 数值阈值 | 温度 > 25C |
| Zone | 进入/离开区域 | 到家 |
| Webhook | HTTP 请求 | 外部触发 |
| MQTT | MQTT 消息 | 传感器数据 |
| Template | 模板条件 | 复杂逻辑 |

### 条件

| 条件 | 说明 |
|-----------|-------------|
| State | 实体处于某状态 |
| Time | 时间在某范围内 |
| Sun | 太阳在地平线以上/以下 |
| Numeric | 数值比较 |
| Template | 模板求值 |
| Zone | 人在某区域 |
| And/Or/Not | 逻辑运算符 |

### 动作

| 动作 | 说明 |
|--------|-------------|
| Service call | 调用服务 |
| Delay | 等待指定时间 |
| Wait | 等待条件满足 |
| Repeat | 重复动作 |
| Choose | 条件动作 |
| Variables | 设置变量 |

### 自动化示例

**感应灯：**

    automation:
      - alias: "Motion light"
        trigger:
          - platform: state
            entity_id: binary_sensor.motion
            to: "on"
        action:
          - service: light.turn_on
            target:
              entity_id: light.hallway
          - delay: "00:05:00"
          - service: light.turn_off
            target:
              entity_id: light.hallway

**温度控制：**

    automation:
      - alias: "Temperature alert"
        trigger:
          - platform: numeric_state
            entity_id: sensor.temperature
            above: 30
        action:
          - service: notify.mobile_app
            data:
              message: "Temperature is {{ states('sensor.temperature') }}C"

**定时自动化：**

    automation:
      - alias: "Good morning"
        trigger:
          - platform: time
            at: "07:00:00"
        condition:
          - condition: state
            entity_id: person.me
            state: home
        action:
          - service: light.turn_on
            target:
              entity_id: light.bedroom
            data:
              brightness: 100
              color_temp: 350
          - service: media_player.play_media
            target:
              entity_id: media_player.speaker
            data:
              media_content_id: "morning_playlist"
              media_content_type: playlist

### 自动化编辑器

Home Assistant 有可视化自动化编辑器：

1. 进入设置 > 自动化
2. 点击"创建自动化"
3. 使用可视化编辑器或 YAML 模式
4. 用"运行"按钮测试
5. 保存自动化

---

## 仪表盘

### 仪表盘类型

| 类型 | 说明 |
|------|-------------|
| Default | 自动生成的仪表盘 |
| Custom | 手动配置 |
| Lovelace | 基于 UI 的仪表盘 |

### 卡片类型

| 卡片 | 说明 |
|------|-------------|
| Entities | 实体列表 |
| Entity | 单个实体 |
| Light | 灯光控制 |
| Thermostat | 温度控制 |
| Media | 媒体播放器 |
| Camera | 摄像头画面 |
| History | 历史数据 |
| Statistics | 统计图表 |
| Gauge | 仪表盘 |
| Markdown | 自定义文本/HTML |
| Picture | 图片 |
| Button | 操作按钮 |
| Grid | 布局容器 |
| Vertical Stack | 垂直布局 |
| Horizontal Stack | 水平布局 |

### 仪表盘配置示例

    views:
      - title: Home
        path: home
        cards:
          - type: entities
            title: Lights
            entities:
              - entity: light.living_room
                name: Living Room
              - entity: light.bedroom
                name: Bedroom
              - entity: light.kitchen
                name: Kitchen

          - type: thermostat
            entity: climate.thermostat
            name: Temperature

          - type: history-graph
            hours_to_show: 24
            entities:
              - entity: sensor.temperature
              - entity: sensor.humidity

          - type: media-control
            entity: media_player.living_room

---

## 设备和实体

### 实体类型

| 类型 | 说明 | 示例 |
|------|-------------|---------|
| Light | 照明设备 | 灯泡、LED 灯带 |
| Switch | 开关设备 | 插座、继电器 |
| Sensor | 只读值 | 温度、湿度 |
| Binary Sensor | 开/关状态 | 感应器、门 |
| Climate | 气候控制 | 温控器 |
| Cover | 窗帘、门 | 电动窗帘 |
| Media Player | 音视频 | 音箱、电视 |
| Camera | 摄像头画面 | 安防摄像头 |
| Lock | 门锁 | 智能锁 |
| Fan | 风扇控制 | 吊扇 |
| Vacuum | 扫地机器人 | Roborock |

### 实体命名规则

    domain.device_name

| 域 | 示例 |
|--------|---------|
| light | light.living_room |
| switch | switch.kitchen_plug |
| sensor | sensor.temperature |
| binary_sensor | binary_sensor.motion |
| climate | climate.thermostat |
| cover | cover.blinds |

### 实体状态

| 实体类型 | 可能状态 |
|-------------|-----------------|
| Light | on、off |
| Switch | on、off |
| Sensor | 多种（数字、文本） |
| Binary Sensor | on、off |
| Climate | heat、cool、auto、off |
| Cover | open、closed、opening、closing |

---

## ESPHome

ESPHome 允许使用 ESP32/ESP8266 创建自定义 IoT 设备。

### 什么是 ESPHome？

| 功能 | 说明 |
|---------|-------------|
| YAML 配置 | 用 YAML 定义设备 |
| OTA 更新 | 通过 WiFi 更新 |
| 原生 HA | 自动集成 Home Assistant |
| 组件 | 支持 100+ 组件 |
| 本地控制 | 无需云 |

### 安装

**在 Home Assistant 中：**

1. 进入设置 > 插件
2. 安装 ESPHome
3. 打开 ESPHome 仪表盘

**独立安装：**

    pip install esphome
    esphome wizard living_room.yaml

### 基本配置

    esphome:
      name: living-room-sensor
      platform: ESP32
      board: esp32dev

    wifi:
      ssid: "MyWiFi"
      password: "password"

    api:
      encryption:
        key: "encryption_key"

    ota:
      password: "ota_password"

    logger:

    sensor:
      - platform: dht
        pin: GPIO4
        temperature:
          name: "Living Room Temperature"
        humidity:
          name: "Living Room Humidity"
        update_interval: 60s

### 常用组件

| 组件 | 用途 |
|-----------|---------|
| dht | 温湿度传感器 |
| bh1750 | 光照传感器 |
| bmp280 | 气压传感器 |
| ultrasonic | 距离传感器 |
| gpio | 数字输入/输出 |
| adc | 模拟输入 |
| pwm | PWM 输出 |
| switch | 开关控制 |
| binary_sensor | 数字输入 |
| output | 执行器控制 |

### 示例：感应传感器

    esphome:
      name: motion-sensor
      platform: ESP8266
      board: nodemcuv2

    wifi:
      ssid: "MyWiFi"
      password: "password"

    binary_sensor:
      - platform: gpio
        pin: D2
        name: "Motion Sensor"
        device_class: motion

---

## Zigbee

### 什么是 Zigbee？

| 功能 | 说明 |
|---------|-------------|
| 低功耗 | 设备电池可用数年 |
| 网状网络 | 设备中继信号 |
| 本地控制 | 无需云 |
| 设备众多 | 庞大的设备生态 |
| 安全 | 加密通信 |

### Zigbee 协调器

| 协调器 | 说明 |
|-------------|-------------|
| Sonoff Zigbee 3.0 USB Dongle Plus | 流行、实惠 |
| ConBee II | 可靠、支持良好 |
| SkyConnect | Home Assistant 官方 |
| Slaesh CC2652R stick | DIY 选项 |

### Zigbee 集成选项

| 选项 | 说明 |
|--------|-------------|
| ZHA | 内置、易用 |
| Zigbee2MQTT | 功能更多、基于 MQTT |
| deCONZ | ConBee/RaspBee 专用 |

### ZHA 设置

1. 插入 Zigbee 协调器
2. 进入设置 > 设备与服务
3. 点击"添加集成"
4. 选择"Zigbee Home Automation"
5. 选择你的协调器
6. 开始配对设备

### 配对设备

1. 将设备置于配对模式
2. 在 ZHA 中点击"添加设备"
3. 等待设备出现
4. 命名并分配区域

### 常用 Zigbee 设备

| 设备 | 品牌 | 类型 |
|--------|-------|------|
| 智能插座 | Sonoff、IKEA | 路由器 |
| 温度传感器 | Aqara、Sonoff | 终端设备 |
| 门窗传感器 | Aqara、Sonoff | 终端设备 |
| 感应传感器 | Aqara、IKEA | 终端设备 |
| 灯泡 | IKEA、Philips | 路由器 |
| 按钮 | IKEA、Aqara | 终端设备 |

---

## Z-Wave

### 什么是 Z-Wave？

| 功能 | 说明 |
|---------|-------------|
| 网状网络 | 设备中继信号 |
| 可靠 | 专用频段 |
| 安全 | S2 加密 |
| 互操作 | 所有 Z-Wave 设备兼容 |
| 远距离 | 每跳 100m+ |

### Z-Wave 控制器

| 控制器 | 说明 |
|------------|-------------|
| Zooz ZST39 | 流行的 USB 棒 |
| Aeotec Z-Stick | 可靠选项 |
| HomeSeer | 功能丰富 |

### Z-Wave JS 设置

1. 插入 Z-Wave 控制器
2. 安装 Z-Wave JS 插件
3. 配置串口
4. 添加集成

### Z-Wave vs Zigbee

| 功能 | Z-Wave | Zigbee |
|---------|--------|--------|
| 频段 | 868/908 MHz | 2.4 GHz |
| 距离 | 100m | 10-20m |
| 设备上限 | 232 | 65,000 |
| 功耗 | 低 | 低 |
| 成本 | 较高 | 较低 |
| 兼容性 | 优秀 | 良好 |

---

## 语音控制

### Home Assistant Voice (Assist)

| 功能 | 说明 |
|---------|-------------|
| 本地 | 无需互联网 |
| 隐私 | 语音本地处理 |
| 可定制 | 自定义句子和意图 |
| 多语言 | 语言支持不断增加 |

### 设置 Assist

**硬件选项：**

| 设备 | 说明 |
|--------|-------------|
| ESP32-S3-BOX | 实惠的语音设备 |
| Wyoming Satellite | 自定义语音卫星 |
| M5Stack Atom | 小型语音设备 |
| 手机 | 移动应用语音 |

**安装：**

1. 安装 Wyoming 集成
2. 安装 Whisper（语音转文字）
3. 安装 Piper（文字转语音）
4. 配置流水线

### 语音流水线

| 组件 | 用途 |
|-----------|---------|
| Wake word | 唤醒词（"OK Nabu"） |
| Speech-to-text | 语音转文字 |
| Intent | 理解命令 |
| Text-to-speech | 响应语音 |

### 外部语音助手

| 助手 | 集成 |
|-----------|-------------|
| Amazon Alexa | Alexa Smart Home |
| Google Home | Google Assistant |
| Siri | HomeKit |

---

## 能源监控

### 设置能源仪表盘

1. 进入设置 > 能源
2. 添加电网消耗
3. 添加单个设备
4. 配置费用

### 能源传感器

| 传感器类型 | 用途 |
|-------------|---------|
| 电网消耗 | 家庭总用量 |
| 太阳能发电 | 太阳能板输出 |
| 电池 | 电池储能 |
| 单个设备 | 每个设备用量 |

### 能源监控设备

| 设备 | 说明 |
|--------|-------------|
| Shelly EM | 全屋监控 |
| Shelly Plug | 单设备监控 |
| CT 钳 | 非侵入式电流传感器 |
| 智能电表读取器 | 读取公用事业电表 |

---

## 技巧和最佳实践

### 性能技巧

| 技巧 | 说明 |
|-----|-------------|
| 使用 SSD | 比 SD 卡快 |
| 充足 RAM | 建议 4GB+ |
| 有线网络 | 比 WiFi 更可靠 |
| 定期更新 | 保持 HA 更新 |
| 清理数据库 | 定期清除旧数据 |

### 备份策略

| 方式 | 频率 |
|--------|-----------|
| 自动 | 每天（内置） |
| Google Drive | 云备份 |
| 手动 | 重大更改前 |
| 快照 | 完整系统备份 |

### 安全最佳实践

| 实践 | 说明 |
|----------|-------------|
| 强密码 | 使用复杂密码 |
| 启用 2FA | 双因素认证 |
| 保持更新 | 安装安全更新 |
| 仅本地 | 如不需要远程访问则禁用 |
| VPN | 使用 VPN 远程访问 |
| 独立网络 | IoT 设备在独立 VLAN |

### 常见自动化模式

| 模式 | 说明 |
|---------|-------------|
| 存在 | 根据谁在家自动化 |
| 时间 | 定时操作 |
| 日落/日出 | 灯光控制 |
| 温度 | 气候控制 |
| 感应 | 安防和便利 |
| 门 | 锁/解锁自动化 |

### 实用插件

| 插件 | 用途 |
|--------|---------|
| File editor | 编辑 YAML 文件 |
| Terminal | 命令行访问 |
| Mosquitto | MQTT 代理 |
| Node-RED | 可视化自动化 |
| Grafana | 数据可视化 |
| InfluxDB | 时序数据库 |
| Samba | 文件共享 |
| SSH | 远程访问 |
| WireGuard | VPN |
| AdGuard | DNS 广告拦截 |

### 社区资源

| 资源 | 说明 |
|----------|-------------|
| Community Forum | 提问、分享 |
| Discord | 实时聊天 |
| Reddit | r/homeassistant |
| GitHub | 源码、问题 |
| HACS | 自定义集成商店 |
| Blueprint Exchange | 分享自动化 |
