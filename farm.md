# Awesome Agriculture：农业技术

## 简介

awesome-agriculture 仓库精选了用于农业技术的开源工具、数据源和平台。从精准农业到供应链管理，这些资源帮助开发者和农民利用技术实现更好的粮食生产。本教程涵盖关键类别和实用工具。

## 为什么农业需要技术

| 挑战 | 技术解决方案 |
|------|-------------|
| 气候变化 | 天气数据和预测 |
| 资源浪费 | 精准施用和监测 |
| 劳动力短缺 | 自动化和机器人 |
| 市场准入 | 数字平台和可追溯性 |
| 知识差距 | 决策支持系统 |

## 精准农业

### 什么是精准农业

精准农业使用数据在田间层面做出关于种植、施肥和收获的决策。

| 技术 | 用途 | 收集的数据 |
|------|------|-----------|
| GPS 导航 | 精确的田间导航 | 位置坐标 |
| 产量监测 | 跟踪收获生产力 | 每区域产量 |
| 土壤传感器 | 测量土壤条件 | 水分、pH、养分 |
| 无人机 | 航空田间扫描 | NDVI、植物健康 |
| 卫星图像 | 大规模监测 | 植被指数 |

### NDVI（归一化植被指数）

NDVI 使用卫星或无人机图像测量植物健康。

| NDVI 范围 | 解读 |
|-----------|------|
| -1.0 到 0.0 | 水体、裸土、岩石 |
| 0.0 到 0.2 | 稀疏植被 |
| 0.2 到 0.4 | 中等植被 |
| 0.4 到 0.6 | 密集植被 |
| 0.6 到 0.8 | 非常健康的植被 |
| 0.8 到 1.0 | 最大植被健康度 |

## 开源农场管理

### 农场管理软件

| 软件 | 描述 | 核心功能 |
|------|------|----------|
| FarmOS | 基于 Web 的农场管理 | 基于 Drupal、可扩展 |
| Tania | 农场任务管理 | 简单界面 |
| LiteFarm | 社交农业平台 | 社区功能 |
| AgroSense | 作物监测 | 传感器集成 |
| Open Agriculture | 受控环境 | 气候配方 |

### FarmOS 设置

```yaml
version: "3"
services:
  farmos:
    image: farmos/farmos:latest
    ports:
      - "80:80"
    volumes:
      - farmos_data:/var/www/html
    depends_on:
      - postgres
  postgres:
    image: postgres:13
    environment:
      POSTGRES_DB: farmos
      POSTGRES_USER: farmos
      POSTGRES_PASSWORD: secure_password
    volumes:
      - postgres_data:/var/lib/postgresql/data
volumes:
  farmos_data:
  postgres_data:
```

### FarmOS 功能

| 功能 | 描述 |
|------|------|
| 资产跟踪 | 跟踪动物、设备、土地 |
| 种植记录 | 记录作物种植和轮作 |
| 投入记录 | 记录肥料、农药 |
| 收获跟踪 | 记录产量和数量 |
| 地图集成 | 基于 GIS 的田间地图 |
| 观察记录 | 记录田间观察 |
| 任务 | 安排和跟踪农活 |

## 天气和气候数据

### 天气数据来源

| 来源 | 覆盖范围 | API 访问 |
|------|----------|----------|
| OpenWeatherMap | 全球 | 是 |
| NOAA | 美国 | 是 |
| Weather.gov | 美国 | 是 |
| ERA5 | 全球（再分析） | Copernicus API |
| AgERA5 | 农业专用 | Copernicus API |

### 天气 API 示例

```python
import requests

def get_weather(lat, lon, api_key):
    url = f"https://api.openweathermap.org/data/2.5/weather"
    params = {
        "lat": lat,
        "lon": lon,
        "appid": api_key,
        "units": "metric"
    }
    response = requests.get(url, params=params)
    data = response.json()

    return {
        "temperature": data["main"]["temp"],
        "humidity": data["main"]["humidity"],
        "description": data["weather"][0]["description"],
        "wind_speed": data["wind"]["speed"]
    }
```

## 土壤数据

### 土壤数据来源

| 来源 | 覆盖范围 | 可用数据 |
|------|----------|----------|
| SoilGrids | 全球 | 土壤类型、pH、有机碳 |
| USDA SSURGO | 美国 | 详细土壤调查 |
| ISRIC | 全球 | 世界土壤信息 |
| LandPKS | 全球 | 田间级土壤评估 |

### 土壤属性

| 属性 | 单位 | 最佳范围 |
|------|------|----------|
| pH | 0-14 | 6.0-7.0（大多数作物） |
| 有机质 | % | 3-5% |
| 氮（N） | ppm | 20-40 ppm |
| 磷（P） | ppm | 25-50 ppm |
| 钾（K） | ppm | 150-250 ppm |
| 水分 | % | 因作物而异 |

## 遥感

### 卫星数据来源

| 来源 | 分辨率 | 重访周期 | 费用 |
|------|--------|----------|------|
| Sentinel-2 | 10m | 5 天 | 免费 |
| Landsat 8/9 | 30m | 16 天 | 免费 |
| MODIS | 250m-1km | 1-2 天 | 免费 |
| Planet | 3m | 每天 | 商业 |
| Google Earth Engine | 各种 | 各种 | 免费套餐 |

### 处理 Sentinel-2 数据

```python
import rasterio
import numpy as np

def calculate_ndvi(nir_band, red_band):
    """从近红外和红波段计算 NDVI。"""
    nir = nir_band.astype(float)
    red = red_band.astype(float)
    ndvi = (nir - red) / (nir + red)
    return ndvi

# 读取 Sentinel-2 波段
with rasterio.open("B04.tif") as red_src:
    red = red_src.read(1)
with rasterio.open("B08.tif") as nir_src:
    nir = nir_src.read(1)

ndvi = calculate_ndvi(nir, red)
```

## IoT 和传感器

### 农业传感器

| 传感器类型 | 测量内容 | 协议 |
|-----------|----------|------|
| 土壤湿度 | 含水量 | LoRa、WiFi |
| 气象站 | 温度、湿度、风速 | LoRa、蜂窝网络 |
| 光照传感器 | PAR（光合有效辐射） | I2C |
| pH 传感器 | 土壤/水酸碱度 | 模拟、I2C |
| EC 传感器 | 电导率 | RS-485 |
| 叶面湿度 | 表面水分 | 模拟 |

### IoT 架构

```
传感器 -> 网关 -> 云平台 -> 仪表板
  |         |        |          |
  |         |        |          |
LoRa    Raspberry Pi  MQTT Broker  Grafana
WiFi    ESP32        InfluxDB     FarmOS
```

### 用于农场数据的 MQTT

```python
import paho.mqtt.client as mqtt
import json

def on_message(client, userdata, message):
    payload = json.loads(message.payload.decode())
    topic = message.topic

    if "soil_moisture" in topic:
        print(f"土壤湿度：{payload['value']}%")
    elif "temperature" in topic:
        print(f"温度：{payload['value']}°C")

client = mqtt.Client()
client.on_message = on_message
client.connect("mqtt.farm.example.com", 1883)
client.subscribe("farm/+/sensor/#")
client.loop_forever()
```

## 作物规划

### 轮作规划

| 年份 | 田块 A | 田块 B | 田块 C |
|------|--------|--------|--------|
| 1 | 玉米 | 大豆 | 小麦 |
| 2 | 大豆 | 小麦 | 玉米 |
| 3 | 小麦 | 玉米 | 大豆 |

### 伴生种植

| 作物 | 好搭档 | 差搭档 |
|------|--------|--------|
| 番茄 | 罗勒、胡萝卜 | 卷心菜、茴香 |
| 玉米 | 豆类、南瓜 | 番茄 |
| 胡萝卜 | 洋葱、韭菜 | 莳萝 |
| 生菜 | 胡萝卜、萝卜 | 无显著差搭档 |

## 供应链

### 可追溯性工具

| 工具 | 用途 | 标准 |
|------|------|------|
| Open Food Facts | 产品数据库 | 条形码 |
| AgriLedger | 区块链可追溯性 | GS1 |
| TE-FOOD | 牲畜可追溯性 | 二维码 |
| OpenSC | 供应链透明度 | 区块链 |

## 数据标准

### 农业数据标准

| 标准 | 范围 | 描述 |
|------|------|------|
| AgGateway ADAPT | 数据交换 | 互操作性框架 |
| ISO 11783 (ISOBUS) | 设备 | 拖拉机-农具通信 |
| FieldML | 田间数据 | 田间数据标记语言 |
| OGC SensorThings | IoT 传感器 | 传感器数据标准 |

## 农业中的机器学习

### 常见 ML 应用

| 应用 | 模型类型 | 数据输入 |
|------|----------|----------|
| 作物病害检测 | CNN（图像分类） | 叶片照片 |
| 产量预测 | 回归 | 天气、土壤、管理 |
| 杂草检测 | 目标检测 | 田间图像 |
| 灌溉调度 | 时间序列 | 土壤湿度、天气 |

### 病害检测示例

```python
import tensorflow as tf
from tensorflow.keras.preprocessing.image import ImageDataGenerator

# 加载预训练模型
model = tf.keras.models.load_model("crop_disease_model.h5")

# 从叶片图像预测病害
def predict_disease(image_path):
    img = tf.keras.preprocessing.image.load_img(
        image_path, target_size=(224, 224)
    )
    img_array = tf.keras.preprocessing.image.img_to_array(img)
    img_array = tf.expand_dims(img_array, 0) / 255.0

    predictions = model.predict(img_array)
    classes = ["Healthy", "Blight", "Rust", "Mildew"]
    return classes[predictions.argmax()]
```

## 法规和合规

| 领域 | 法规 | 工具 |
|------|------|------|
| 有机认证 | USDA NOP | 记录保持软件 |
| 食品安全 | FSMA | 可追溯系统 |
| 农药使用 | EPA 法规 | 施用记录 |
| 水权 | 州/地方 | 用水跟踪 |

## 社区资源

| 资源 | 类型 | 重点 |
|------|------|------|
| OpenAg Data Alliance | 数据共享 | 农业数据 |
| Farm Hack | 社区 | DIY 农具 |
| AgStack | 基金会 | 开源农业 |
| r/agriculture | 论坛 | 综合讨论 |

## 总结

农业技术从简单的农场管理软件到复杂的 IoT 和遥感系统。从 FarmOS 开始用于记录保持，集成天气 API 用于规划，探索卫星数据用于田间监测。开源工具使精准农业对各种规模的农场都触手可及。
