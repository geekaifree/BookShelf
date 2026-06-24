# 农业技术：现代农业的技术与资源

## 目录

1. [简介](#introduction)
2. [农场管理](#farm-management)
3. [作物监测](#crop-monitoring)
4. [土壤分析](#soil-analysis)
5. [气象服务](#weather-services)
6. [灌溉系统](#irrigation-systems)
7. [畜牧管理](#livestock-management)
8. [精准农业](#precision-farming)
9. [农业无人机](#drones-in-agriculture)
10. [IoT 传感器](#iot-sensors)
11. [开放数据资源](#open-data-resources)
12. [市场分析](#market-analysis)

---

## 简介

农业技术（AgTech）涵盖帮助农民提高生产力、降低成本和进行数据驱动决策的工具、软件和方法。本指南涵盖农业技术的主要类别以及面向农民和开发者的开源资源。

### 技术全景

| 类别 | 用途 | 关键技术 |
|------|------|----------|
| 农场管理 | 规划和记录 | ERP 系统、移动应用 |
| 作物监测 | 追踪作物健康和生长 | 遥感、成像 |
| 土壤分析 | 了解土壤状况 | 传感器、实验室检测 |
| 气象 | 环境预测 | API、气象站 |
| 灌溉 | 水资源管理 | 智能控制器、传感器 |
| 畜牧 | 动物健康和追踪 | 可穿戴设备、RFID |
| 精准农业 | 地块特定管理 | GPS、变量施用 |
| 无人机 | 航空监测 | UAV 平台 |
| IoT | 联网设备 | 传感器网络 |
| 开放数据 | 共享农业数据 | 政府数据集 |
| 市场分析 | 价格和趋势数据 | 市场平台 |

### AgTech 的优势

- **提高产量**：优化生长条件
- **降低成本**：高效利用资源
- **更好的决策**：数据驱动管理
- **可持续性**：减少环境影响
- **可追溯性**：供应链透明

---

## 农场管理

### 农场管理软件（FMS）

农场管理软件帮助规划、追踪和分析所有农场运营。

| 软件 | 类型 | 功能 | 许可证 |
|------|------|------|--------|
| FarmOS | 基于 Web | 作物规划、记录、地图 | 开源 |
| AgroSense | Web/移动端 | 田间作业、气象 | 开源 |
| LiteFarm | 基于 Web | 作物规划、劳动力追踪 | 开源 |
| OpenAg | IoT 平台 | 传感器集成、自动化 | 开源 |
| Cropio | 卫星 | 田间监测、分析 | 商业 |

### FarmOS 平台

FarmOS 是领先的开源农场管理平台：

**核心模块：**

| 模块 | 功能 |
|------|------|
| 作物规划 | 种植计划、轮作 |
| 活动日志 | 记录所有农场活动 |
| 资产管理 | 追踪设备、建筑、土地 |
| 观察 | 巡查报告、病虫害观察 |
| 地图 | 田块边界、分区 |
| 库存 | 种子、投入品、收获追踪 |

**安装：**

```bash
# 使用 Docker
docker pull farmos/farmos:3.x
docker run -d -p 80:80 farmos/farmos:3.x

# 使用 Drush（已有 Drupal 站点）
drush en farm farm_crop farm_animal farm_equipment
```

**数据结构：**

```
农场
├── 土地
│   ├── 田块
│   ├── 地块
│   └── 苗床
├── 资产
│   ├── 作物
│   ├── 动物
│   └── 设备
├── 日志
│   ├── 活动
│   ├── 观察
│   └── 投入
└── 计划
    ├── 轮作
    └── 种植计划
```

### 记录管理

农场管理的基本记录：

| 记录类型 | 追踪信息 |
|----------|----------|
| 种植 | 日期、品种、位置、播种量 |
| 投入 | 肥料、农药、水量 |
| 收获 | 产量、质量、日期 |
| 气象 | 温度、降雨、事件 |
| 财务 | 成本、收入、利润 |
| 劳动力 | 工时、任务、工人 |

### 轮作规划

规划多年轮作计划：

| 年份 | 田块 A | 田块 B | 田块 C | 田块 D |
|------|--------|--------|--------|--------|
| 1 | 玉米 | 大豆 | 小麦 | 覆盖作物 |
| 2 | 大豆 | 小麦 | 覆盖作物 | 玉米 |
| 3 | 小麦 | 覆盖作物 | 玉米 | 大豆 |
| 4 | 覆盖作物 | 玉米 | 大豆 | 小麦 |

轮作的好处：
- 打断病虫害循环
- 改善土壤结构
- 平衡养分需求
- 减少杂草压力

---

## 作物监测

### 遥感技术

| 技术 | 分辨率 | 覆盖范围 | 成本 |
|------|--------|----------|------|
| 卫星 | 10-30m | 大面积 | 免费-低 |
| 飞机 | 1-5m | 区域 | 中等 |
| 无人机 | 1-10cm | 田块级 | 低-中等 |
| 地面传感器 | 点 | 特定位置 | 低 |

### 植被指数

作物监测中常用的指数：

| 指数 | 公式 | 用途 |
|------|------|------|
| NDVI | (NIR-Red)/(NIR+Red) | 植被总体健康 |
| NDRE | (NIR-RedEdge)/(NIR+RedEdge) | 叶绿素含量 |
| SAVI | ((NIR-Red)/(NIR+Red+L))*(1+L) | 稀疏植被 |
| GNDVI | (NIR-Green)/(NIR+Green) | 绿色植被 |
| CWSI | 热红外数据 | 水分胁迫 |

### NDVI 解读

| NDVI 值 | 解读 | 操作 |
|---------|------|------|
| < 0.1 | 裸地、水体 | 无植被 |
| 0.1 - 0.3 | 稀疏植被 | 调查胁迫原因 |
| 0.3 - 0.5 | 中等植被 | 密切监测 |
| 0.5 - 0.7 | 茂密、健康 | 常规管理 |
| > 0.7 | 非常茂密 | 最佳状态 |

### 开源监测工具

**QGIS 配合 QField：**

```python
# QGIS Python 脚本计算 NDVI
from qgis.core import *

# 加载波段
red_band = QgsRasterLayer('red.tif', 'Red')
nir_band = QgsRasterLayer('nir.tif', 'NIR')

# 使用栅格计算器计算 NDVI
# NDVI = (NIR - Red) / (NIR + Red)
expression = '( "NIR@1" - "Red@1" ) / ( "NIR@1" + "Red@1" )'
```

**Sentinel Hub：**

```python
# 访问 Sentinel-2 数据
from sentinelhub import SHConfig, SentinelHubRequest, MimeType

config = SHConfig()
config.sh_client_id = 'your-client-id'
config.sh_client_secret = 'your-client-secret'

# 请求 NDVI 数据
evalscript = """
//VERSION=3
function setup() {
    return {
        input: [{bands: ["B04", "B08"], units: "DN"}],
        output: {bands: 1, sampleType: "FLOAT32"}
    };
}

function evaluatePixel(sample) {
    let ndvi = (sample.B08 - sample.B04) / (sample.B08 + sample.B04);
    return [ndvi];
}
"""
```

### 作物病害检测

使用图像识别进行病害识别：

| 病害 | 作物 | 症状 | 检测方法 |
|------|------|------|----------|
| 晚疫病 | 马铃薯 | 深色病斑、白色霉层 | 图像分类 |
| 锈病 | 小麦 | 橙色脓疱 | 光谱分析 |
| 白粉病 | 葡萄 | 白色覆盖物 | 目视检查 |
| 细菌性斑点 | 番茄 | 果实深色斑点 | 图像处理 |

---

## 土壤分析

### 土壤检测方法

| 方法 | 参数 | 精度 | 成本 |
|------|------|------|------|
| 实验室分析 | 全谱 | 高 | 中等 |
| 现场检测套件 | pH、NPK | 中等 | 低 |
| 传感器 | 水分、EC | 高 | 中高 |
| 光谱分析 | 多种 | 高 | 高 |

### 关键土壤参数

| 参数 | 最佳范围 | 影响 |
|------|----------|------|
| pH | 6.0 - 7.0 | 养分有效性 |
| 有机质 | 3 - 5% | 土壤结构、保水性 |
| 氮（N） | 20-40 ppm | 作物生长 |
| 磷（P） | 25-50 ppm | 根系发育 |
| 钾（K） | 150-250 ppm | 抗病性 |
| CEC | 10-30 meq/100g | 养分保持 |
| EC | 0-2 dS/m | 盐分 |

### 土壤采样方案

1. **网格采样**：将田块划分为均匀网格
2. **分区采样**：基于土壤类型或产量分区
3. **混合采样**：每个区域混合多个土芯

```
采样模式（网格）：
+---+---+---+---+
| * |   | * |   |
+---+---+---+---+
|   | * |   | * |
+---+---+---+---+
| * |   | * |   |
+---+---+---+---+

* = 采样点
```

### 开源土壤工具

**SoilGrids：**
- 全球土壤属性预测
- 250m 分辨率
- 通过 REST API 免费访问

```python
# 访问 SoilGrids API
import requests

def get_soil_properties(lat, lon):
    url = f"https://rest.soilgrids.org/soilgrids/v2.0/properties/query"
    params = {
        'lon': lon,
        'lat': lat,
        'property': ['clay', 'sand', 'phh2o', 'soc'],
        'depth': ['0-5cm', '5-15cm', '15-30cm'],
        'value': 'mean'
    }
    response = requests.get(url, params=params)
    return response.json()
```

### 土壤健康指标

| 指标 | 健康范围 | 检测方法 |
|------|----------|----------|
| 蚯蚓数量 | > 10 条/立方英尺 | 人工计数 |
| 水分渗透 | > 1 英寸/小时 | 环式入渗仪 |
| 容重 | < 1.4 g/cm³ | 取芯采样 |
| 呼吸作用 | > 20 mg CO2/天 | Solvita 测试 |
| 团聚体稳定性 | > 50% | 湿筛法 |

---

## 气象服务

### 气象数据来源

| 来源 | 覆盖范围 | 分辨率 | 成本 |
|------|----------|--------|------|
| OpenWeatherMap | 全球 | 城市级 | 免费/付费 |
| NOAA | 美国 | 区域 | 免费 |
| Meteostat | 全球 | 站点 | 免费 |
| Weather Underground | 全球 | 站点 | 免费/付费 |
| Dark Sky (Apple) | 全球 | 点 | 付费 |

### 气象 API

**OpenWeatherMap：**

```python
import requests

API_KEY = 'your_api_key'

def get_weather(lat, lon):
    url = f"https://api.openweathermap.org/data/2.5/weather"
    params = {
        'lat': lat,
        'lon': lon,
        'appid': API_KEY,
        'units': 'metric'
    }
    response = requests.get(url, params=params)
    data = response.json()
    
    return {
        'temperature': data['main']['temp'],
        'humidity': data['main']['humidity'],
        'rain': data.get('rain', {}).get('1h', 0),
        'wind': data['wind']['speed']
    }
```

### 农业气象指标

| 指标 | 重要性 | 应用 |
|------|--------|------|
| 生长积温（GDD） | 作物发育 | 成熟预测 |
| 蒸散量（ET） | 水分需求 | 灌溉计划 |
| 霜冻概率 | 作物保护 | 种植决策 |
| 土壤温度 | 种子发芽 | 播种时机 |
| 病害压力 | 真菌风险 | 喷药决策 |

### GDD 计算

```python
def calculate_gdd(t_max, t_min, t_base=10):
    """计算生长积温"""
    t_avg = (t_max + t_min) / 2
    gdd = max(0, t_avg - t_base)
    return gdd

# 示例
gdd = calculate_gdd(t_max=28, t_min=15, t_base=10)
# GDD = max(0, 21.5 - 10) = 11.5
```

### 气象站设置

农场气象站组件：

| 组件 | 用途 | 推荐型号 |
|------|------|----------|
| 温度传感器 | 气温 | DHT22、BME280 |
| 雨量计 | 降水量 | 翻斗式 |
| 风速计 | 风速 | 杯式 |
| 风向标 | 风向 | 电位器式 |
| 湿度传感器 | 相对湿度 | DHT22、BME280 |
| 太阳辐射传感器 | 辐射 | 辐射表 |
| 土壤传感器 | 土壤温度 | DS18B20 |

---

## 灌溉系统

### 灌溉方式

| 方式 | 效率 | 最佳用途 | 成本 |
|------|------|----------|------|
| 滴灌 | 90-95% | 行栽作物、果园 | 中等 |
| 喷灌 | 70-80% | 大田作物、草坪 | 中等 |
| 漫灌 | 40-60% | 水稻、牧场 | 低 |
| 中心支轴 | 75-85% | 大面积田块 | 高 |
| 微喷 | 85-90% | 果园、蔬菜 | 中等 |

### 智能灌溉控制器

| 控制器 | 功能 | 集成 |
|--------|------|------|
| OpenSprinkler | 开源、基于 Web | API、MQTT |
| Rachio | 基于天气 | 智能家居 |
| RainMachine | 本地 AI | 气象 API |
| IrrigationCaddy | 简单可靠 | Web 界面 |

### OpenSprinkler 设置

```bash
# 安装 OpenSprinkler 固件
git clone https://github.com/OpenSprinkler/OpenSprinkler-Firmware.git
cd OpenSprinkler-Firmware

# 配置
cp defines.h.example defines.h
# 根据硬件编辑 defines.h

# 编译并刷写
make
```

**API 使用：**

```python
import requests

OPENSPRINKLER_IP = '192.168.1.100'
PASSWORD = 'your_md5_password'

def start_zone(zone, duration):
    """启动灌溉区"""
    url = f"http://{OPENSPRINKLER_IP}/cm"
    params = {
        'cmd': f'pz{zone}',
        'pid': zone,
        'dur': duration,
        'en': 1,
        'pw': PASSWORD
    }
    response = requests.get(url, params=params)
    return response.json()

def get_status():
    """获取系统状态"""
    url = f"http://{OPENSPRINKLER_IP}/jo"
    params = {'pw': PASSWORD}
    response = requests.get(url, params=params)
    return response.json()
```

### 基于土壤水分的灌溉

| 土壤水分 | 状态 | 操作 |
|----------|------|------|
| < 20% | 萎蔫点 | 立即灌溉 |
| 20-40% | 胁迫区 | 安排灌溉 |
| 40-60% | 适宜 | 监测 |
| 60-80% | 最佳 | 无需灌溉 |
| > 80% | 过量 | 涝渍风险 |

### 灌溉调度

```python
def calculate_irrigation_need(et, rainfall, soil_moisture, field_capacity):
    """
    计算灌溉需求
    et: 蒸散量（mm/天）
    rainfall: 近期降雨（mm）
    soil_moisture: 当前水分（%）
    field_capacity: 最大持水量（%）
    """
    # 水分亏缺
    deficit = field_capacity - soil_moisture
    
    # 净灌溉需求
    net_need = et - rainfall + (deficit * root_depth_factor)
    
    # 加入效率因子
    gross_need = net_need / irrigation_efficiency
    
    return max(0, gross_need)
```

---

## 畜牧管理

### 畜牧追踪技术

| 技术 | 用途 | 范围 | 成本 |
|------|------|------|------|
| RFID 标签 | 个体识别 | 近距离 | 低 |
| GPS 项圈 | 位置追踪 | 全球 | 中等 |
| 耳标传感器 | 健康监测 | 近距离 | 中等 |
| 瘤胃传感器 | 体内温度 | 近距离 | 高 |
| 摄像系统 | 行为分析 | 视野范围内 | 中等 |

### 开源畜牧平台

| 平台 | 重点 | 功能 |
|------|------|------|
| FarmOS Animals | 通用畜牧 | 健康记录、繁殖 |
| OpenLivestock | 牛群管理 | 追踪、分析 |
| CattleMax | 肉牛 | 牛群管理 |
| HerdDogg | 智能耳标 | 健康监测 |

### 动物健康监测

| 指标 | 正常范围 | 警报阈值 |
|------|----------|----------|
| 体温 | 38-39.5°C（牛） | > 40°C |
| 心率 | 60-80 bpm（牛） | > 100 bpm |
| 活动水平 | 品种相关 | 偏差50% |
| 反刍 | 7-10 小时/天 | < 5 小时 |
| 采食量 | 品种相关 | 下降20% |

### RFID 标签系统

```python
# RFID 读取器集成
import serial

class RFIDReader:
    def __init__(self, port='/dev/ttyUSB0', baudrate=9600):
        self.serial = serial.Serial(port, baudrate)
    
    def read_tag(self):
        """读取 RFID 标签数据"""
        if self.serial.in_waiting > 0:
            tag_data = self.serial.readline().decode().strip()
            return self.parse_tag(tag_data)
        return None
    
    def parse_tag(self, data):
        """解析 RFID 标签格式"""
        return {
            'tag_id': data[:12],
            'country_code': data[12:15],
            'animal_id': data[15:]
        }

# 使用
reader = RFIDReader()
tag = reader.read_tag()
if tag:
    print(f"Animal ID: {tag['animal_id']}")
```

---

## 精准农业

### 精准农业技术

| 技术 | 应用 | 优势 |
|------|------|------|
| GPS 导航 | 自动驾驶、测绘 | 减少重叠 |
| 变量施用 | 投入品施用 | 优化投入 |
| 产量图 | 收获数据 | 田块变异性 |
| 土壤测绘 | 分区管理 | 定向处理 |
| 遥感 | 作物监测 | 早期发现 |

### 变量施用（VRA）

根据田块变异性施用投入品：

```
田块分区图：
┌───────────────────────────────────┐
│ Zone A (High) │ Zone B (Medium)   │
│ Rate: 150 kg/ha│ Rate: 100 kg/ha  │
├────────────────┼──────────────────┤
│ Zone C (Low)  │ Zone D (Medium)   │
│ Rate: 50 kg/ha │ Rate: 100 kg/ha  │
└────────────────┴──────────────────┘
```

### GPS 和导航系统

| 系统 | 精度 | 应用 |
|------|------|------|
| 自主 GPS | 1-3m | 基本导航 |
| SBAS (WAAS/EGNOS) | 15-30cm | 田间作业 |
| RTK GPS | 2-5cm | 精密播种 |
| PPP | 10-20cm | 测量 |

### 产量监测

```python
# 产量数据处理
import pandas as pd

def process_yield_data(file_path):
    """处理产量监测数据"""
    df = pd.read_csv(file_path)
    
    # 清洗数据
    df = df[df['moisture'] < 25]  # 去除异常值
    df = df[df['yield'] > 0]  # 去除零产量
    
    # 计算统计数据
    stats = {
        'mean_yield': df['yield'].mean(),
        'std_yield': df['yield'].std(),
        'min_yield': df['yield'].min(),
        'max_yield': df['yield'].max(),
        'total_area': df['area'].sum(),
        'total_production': (df['yield'] * df['area']).sum()
    }
    
    return stats
```

### 处方图

创建变量施用处方图：

```python
import numpy as np

def create_prescription(soil_data, yield_data, target_rate):
    """
    根据土壤和产量数据创建处方图
    """
    # 数据标准化
    soil_norm = (soil_data - soil_data.min()) / (soil_data.max() - soil_data.min())
    yield_norm = (yield_data - yield_data.min()) / (yield_data.max() - yield_data.min())
    
    # 计算分区（k-means 聚类）
    from sklearn.cluster import KMeans
    features = np.column_stack([soil_norm, yield_norm])
    kmeans = KMeans(n_clusters=4)
    zones = kmeans.fit_predict(features)
    
    # 根据分区分配用量
    rates = {
        0: target_rate * 0.5,  # 低区
        1: target_rate * 0.75, # 中低
        2: target_rate * 1.0,  # 中高
        3: target_rate * 1.25  # 高区
    }
    
    prescription = np.vectorize(rates.get)(zones)
    return prescription
```

---

## 农业无人机

### 农业无人机平台

| 无人机 | 续航 | 载荷 | 功能 |
|--------|------|------|------|
| DJI Agras T40 | 15 分钟 | 40kg | 喷洒 |
| DJI Phantom 4 RTK | 30 分钟 | 相机 | 测绘 |
| senseFly eBee X | 90 分钟 | 传感器 | 固定翼 |
| Autel EVO II | 42 分钟 | 相机 | 多光谱 |

### 无人机传感器

| 传感器类型 | 采集数据 | 应用 |
|------------|----------|------|
| RGB | 彩色图像 | 目视检查 |
| 多光谱 | 4-6 波段 | NDVI、作物健康 |
| 热红外 | 温度 | 水分胁迫 |
| LiDAR | 3D 结构 | 冠层分析 |
| 高光谱 | 100+ 波段 | 病害检测 |

### 无人机测绘流程

1. **航线规划**

```python
# 使用 DJI Mobile SDK 或 QGroundControl
flight_plan = {
    'altitude': 60,  # 米
    'speed': 5,  # m/s
    'overlap': {
        'front': 80,  # 百分比
        'side': 70
    },
    'waypoints': [
        {'lat': 40.7128, 'lon': -74.0060},
        {'lat': 40.7130, 'lon': -74.0058},
        # ... 更多航点
    ]
}
```

2. **使用 OpenDroneMap 处理图像**

```bash
# 安装 OpenDroneMap
git clone https://github.com/OpenDroneMap/ODM.git
cd ODM

# 处理图像
python run.py --project-path /path/to/images \
    --orthophoton-resolution 2 \
    --dsm \
    --dtm
```

3. **NDVI 图生成**

```python
from osgeo import gdal
import numpy as np

def calculate_ndvi(red_band, nir_band):
    """从红光和近红外波段计算 NDVI"""
    red = red_band.ReadAsArray().astype(float)
    nir = nir_band.ReadAsArray().astype(float)
    
    # 避免除以零
    np.seterr(divide='ignore', invalid='ignore')
    
    ndvi = (nir - red) / (nir + red)
    ndvi = np.nan_to_num(ndvi)
    
    return ndvi
```

### 无人机法规

| 地区 | 主要要求 |
|------|----------|
| 美国（FAA） | Part 107 执照，< 55 磅，目视范围内 |
| 欧盟（EASA） | 开放/特定/认证类别 |
| 加拿大（RPAS） | 飞行员证书、注册 |
| 澳大利亚（CASA） | 商业需 RePL、注册 |

---

## IoT 传感器

### 农业 IoT 架构

```
┌─────────────────────────────────────────────────┐
│                 云平台                            │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │ 数据存储     │  │  分析       │  │ 仪表盘  │ │
│  └─────────────┘  └─────────────┘  └─────────┘ │
├─────────────────────────────────────────────────┤
│                 连接层                            │
│  ┌─────────┐  ┌─────────┐  ┌─────────────────┐ │
│  │  LoRa   │  │  WiFi   │  │ Cellular (4G/5G)│ │
│  └─────────┘  └─────────┘  └─────────────────┘ │
├─────────────────────────────────────────────────┤
│                 田间传感器                        │
│  ┌─────────┐  ┌─────────┐  ┌─────────────────┐ │
│  │  土壤   │  │  气象   │  │    作物         │ │
│  │ 传感器  │  │   站    │  │   传感器        │ │
│  └─────────┘  └─────────┘  └─────────────────┘ │
└─────────────────────────────────────────────────┘
```

### 传感器类型

| 传感器 | 测量 | 协议 | 功耗 |
|--------|------|------|------|
| 土壤水分 | 含水量 | Analog/I2C | 低 |
| 温度 | 气温/土温 | 1-Wire/I2C | 极低 |
| 湿度 | 相对湿度 | I2C | 低 |
| 光照 | PAR/Lux | I2C | 低 |
| EC | 电导率 | Analog | 低 |
| pH | 酸碱度 | Analog | 低 |
| 风速 | 速度、方向 | Pulse/Serial | 中等 |
| 雨量 | 降水量 | Pulse | 极低 |

### LoRaWAN 农业应用

```cpp
// Arduino LoRa 传感器节点
#include <LoRa.h>
#include <DHT.h>

#define DHT_PIN 4
#define SOIL_PIN A0
#define LORA_FREQ 868E6  // EU 频率

DHT dht(DHT_PIN, DHT22);

void setup() {
    Serial.begin(115200);
    dht.begin();
    LoRa.begin(LORA_FREQ);
}

void loop() {
    float temperature = dht.readTemperature();
    float humidity = dht.readHumidity();
    int soilMoisture = analogRead(SOIL_PIN);
    
    // 发送数据
    LoRa.beginPacket();
    LoRa.print("temp=");
    LoRa.print(temperature);
    LoRa.print(",hum=");
    LoRa.print(humidity);
    LoRa.print(",soil=");
    LoRa.print(soilMoisture);
    LoRa.endPacket();
    
    delay(300000);  // 5 分钟
}
```

### MQTT 传感器数据

```python
# Python MQTT 客户端用于传感器数据
import paho.mqtt.client as mqtt
import json

def on_connect(client, userdata, flags, rc):
    print(f"Connected with result code {rc}")
    client.subscribe("farm/+/sensors/#")

def on_message(client, userdata, msg):
    topic = msg.topic
    data = json.loads(msg.payload.decode())
    
    # 处理传感器数据
    if 'soil_moisture' in data:
        check_irrigation_need(data)
    if 'temperature' in data:
        check_frost_risk(data)

client = mqtt.Client()
client.on_connect = on_connect
client.on_message = on_message
client.connect("mqtt.farm.local", 1883, 60)
client.loop_forever()
```

### 数据平台

| 平台 | 类型 | 功能 |
|------|------|------|
| ThingsBoard | 开源 | 设备管理、仪表盘 |
| Node-RED | 开源 | 流式编程 |
| InfluxDB | 时序数据库 | 高性能存储 |
| Grafana | 可视化 | 仪表盘、告警 |
| FarmOS IoT | 农业 | 农场特定集成 |

---

## 开放数据资源

### 政府农业数据

| 来源 | 国家 | 数据类型 |
|------|------|----------|
| USDA NASS | 美国 | 作物统计、调查 |
| Eurostat | 欧盟 | 农业统计 |
| FAO | 全球 | 粮食和农业数据 |
| India Data Portal | 印度 | 农业数据集 |
| AgriFood Atlas | 全球 | 供应链数据 |

### 气象和气候数据

| 来源 | 覆盖范围 | 分辨率 |
|------|----------|--------|
| NOAA GHCN | 全球 | 站点 |
| ERA5 (ECMWF) | 全球 | 30km |
| PRISM | 美国 | 800m |
| CHIRPS | 全球 | 5km |
| NASA POWER | 全球 | 点 |

### 卫星数据来源

| 来源 | 卫星 | 分辨率 | 重访周期 |
|------|------|--------|----------|
| Copernicus | Sentinel-2 | 10m | 5 天 |
| USGS | Landsat | 30m | 16 天 |
| Planet | PlanetScope | 3m | 每天 |
| Google Earth Engine | 多种 | 不等 | 不等 |

### 使用 Google Earth Engine

```javascript
// Google Earth Engine JavaScript
var region = ee.Geometry.Rectangle([-95.5, 40.5, -95.0, 41.0]);

var sentinel2 = ee.ImageCollection('COPERNICUS/S2_SR')
    .filterDate('2024-06-01', '2024-06-30')
    .filterBounds(region)
    .filter(ee.Filter.lt('CLOUDY_PIXEL_PERCENTAGE', 20))
    .median();

var ndvi = sentinel2.normalizedDifference(['B8', 'B4']).rename('NDVI');

Map.addLayer(ndvi, {min: -1, max: 1, palette: ['red', 'yellow', 'green']}, 'NDVI');
```

### 土壤数据

| 来源 | 覆盖范围 | 参数 |
|------|----------|------|
| SoilGrids | 全球 | 质地、pH、SOC、养分 |
| gSSURGO | 美国 | 详细土壤调查 |
| LUCAS | 欧盟 | 土壤属性 |
| iSDA Africa | 非洲 | 土壤养分 |

---

## 市场分析

### 农业市场数据来源

| 来源 | 覆盖范围 | 数据类型 |
|------|----------|----------|
| CME Group | 美国 | 期货价格 |
| FAO GIEWS | 全球 | 粮食价格 |
| AgriPulse | 美国 | 市场新闻 |
| Farmers.gov | 美国 | 市场报告 |
| Agmarknet | 印度 | 市场价格 |

### 价格追踪工具

```python
# 农业价格监测
import requests
from datetime import datetime

class AgMarketMonitor:
    def __init__(self):
        self.commodities = ['corn', 'soybeans', 'wheat', 'cotton']
    
    def get_futures_prices(self, commodity):
        """从 API 获取期货价格"""
        url = f"https://api.example.com/futures/{commodity}"
        response = requests.get(url)
        return response.json()
    
    def calculate_price_change(self, prices):
        """计算价格变化"""
        changes = {}
        for commodity, price_data in prices.items():
            if len(price_data) >= 2:
                current = price_data[-1]['price']
                previous = price_data[-2]['price']
                change = ((current - previous) / previous) * 100
                changes[commodity] = {
                    'current': current,
                    'change': change,
                    'trend': 'up' if change > 0 else 'down'
                }
        return changes
    
    def generate_report(self, prices):
        """生成市场报告"""
        report = {
            'date': datetime.now().isoformat(),
            'prices': prices,
            'summary': self.generate_summary(prices)
        }
        return report
```

### 市场分析指标

| 指标 | 描述 | 用途 |
|------|------|------|
| 基差 | 现货 - 期货价格 | 销售决策 |
| 季节平均 | 历史平均 | 选择销售时机 |
| 价格预测 | 预测价格 | 规划 |
| 供需 | 平衡表 | 长期策略 |

### 决策支持

| 市场信号 | 操作 |
|----------|------|
| 强基差 | 本地销售 |
| 弱基差 | 储存或运往其他市场 |
| 高期货价 | 远期合约 |
| 低期货价 | 等待或使用 LDP |

---

## 总结

农业技术为现代农业提供了强大的工具：

- **农场管理**：规划和记录软件
- **作物监测**：遥感和植被指数
- **土壤分析**：土壤属性检测和测绘
- **气象服务**：预测和历史数据
- **灌溉**：智能水资源管理系统
- **畜牧**：追踪和健康监测
- **精准农业**：地块特定管理
- **无人机**：航空监测和测绘
- **IoT 传感器**：联网田间监测
- **开放数据**：共享农业数据集
- **市场分析**：价格追踪和决策支持

这些技术帮助农民做出更好的决策、降低成本并提高可持续性。
