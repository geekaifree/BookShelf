# Marlin：3D 打印机固件

## 简介

Marlin 是使用最广泛的开源 3D 打印机固件。它运行在基于 AVR 和 ARM 的微控制器上，支持大量打印机配置。

| 属性 | 详情 |
|----------|--------|
| 仓库 | MarlinFirmware/Marlin |
| 许可证 | GPL-3.0 |
| 语言 | C++ |
| 平台 | AVR (ATmega), ARM (STM32, SAM, LPC, ESP32) |
| IDE | PlatformIO, Arduino IDE |

## 主要功能

| 功能 | 描述 |
|---------|-------------|
| Cartesian Support | 标准 XYZ 运动 |
| Delta Support | Delta 打印机运动学 |
| CoreXY Support | CoreXY 运动系统 |
| Auto Bed Leveling | 基于探针的热床补偿 |
| Linear Advance | 压力补偿 |
| S-Curve Acceleration | 更平滑的运动曲线 |
| Trinamic Support | TMC 步进驱动集成 |
| Dual Extrusion | 多挤出头支持 |
| LCD Support | 各种显示器类型 |
| SD Card | 从 SD 卡打印 |

## 支持的硬件

### 微控制器板

| 板 | MCU | 备注 |
|-------|-----|-------|
| RAMPS 1.4 | ATmega2560 | 经典 Arduino 板 |
| SKR 1.4 | LPC1768 | 流行的 32 位板 |
| SKR 2.0 | STM32 | 现代 32 位板 |
| SKR Mini E3 | STM32 | Ender 3 直接替换升级 |
| MKS Robin Nano | STM32 | 彩色触摸屏板 |
| Duet 2 | SAM4E8E | 高端板 |
| Einsy Rambo | ATmega2560 | 原装 Prusa 板 |

### 步进驱动

| 驱动 | 特性 |
|--------|----------|
| A4988 | 基础，1/16 微步 |
| DRV8825 | 1/32 微步 |
| TMC2208 | 静音，UART 模式 |
| TMC2209 | 静音，无传感器归位 |
| TMC2226 | TMC2209 变体 |
| TMC5160 | 大电流，SPI 模式 |

## 安装

### 前提条件

| 工具 | 描述 |
|------|-------------|
| PlatformIO | 构建系统（推荐） |
| Arduino IDE | 替代构建环境 |
| VS Code | 带 PlatformIO 扩展的代码编辑器 |
| Git | 版本控制 |

### 使用 PlatformIO 构建

```bash
# 克隆仓库
git clone https://github.com/MarlinFirmware/Marlin.git
cd Marlin

# 编辑配置文件
# Configuration.h
# Configuration_adv.h

# 为您的板构建
pio run -e mega2560

# 上传到打印机
pio run -e mega2560 --target upload
```

### 使用 Arduino IDE 构建

1. 安装 Arduino IDE。
2. 添加您的 MCU 的板定义。
3. 打开 Marlin.ino。
4. 选择正确的板和端口。
5. 编辑 Configuration.h 和 Configuration_adv.h。
6. 点击上传。

## 配置

### Configuration.h

主配置文件定义打印机硬件。

| 部分 | 设置 |
|---------|----------|
| Serial（串口） | 串口配置 |
| Motherboard（主板） | 板类型定义 |
| Temperature（温度） | 热敏电阻类型和 PID 设置 |
| Extruder（挤出头） | 挤出头数量和配置 |
| Bed Size（热床尺寸） | 打印区域尺寸 |
| Kinematics（运动学） | 运动系统类型 |
| Auto Leveling（自动调平） | 热床探针配置 |
| LCD | 显示器类型选择 |

### 基本配置

```cpp
// 主板
#define MOTHERBOARD BOARD_BTT_SKR_V1_4

// 串口
#define SERIAL_PORT 0
#define BAUDRATE 115200

// 挤出头
#define EXTRUDERS 1
#define DEFAULT_NOMINAL_FILAMENT_DIA 1.75

// 热床尺寸
#define X_BED_SIZE 220
#define Y_BED_SIZE 220
#define Z_MAX_POS 250

// 温度
#define TEMP_SENSOR_0 1    // 热端热敏电阻类型
#define TEMP_SENSOR_BED 1  // 热床热敏电阻类型

// PID 设置
#define PIDTEMP
#define DEFAULT_Kp 22.2
#define DEFAULT_Ki 1.08
#define DEFAULT_Kd 114
```

### Configuration_adv.h

用于微调的高级设置。

| 部分 | 设置 |
|---------|----------|
| Thermal（热保护） | 热失控保护 |
| Stepper（步进） | 驱动特定设置 |
| LCD | 显示器自定义 |
| SD Card | SD 卡支持 |
| WiFi | 网络连接 |
| Trinamic | TMC 驱动配置 |

## 自动热床调平

### 探针类型

| 探针 | 描述 |
|-------|-------------|
| BLTouch | 机械可伸缩探针 |
| Inductive（电感） | 电磁接近传感器 |
| Capacitive（电容） | 电容接近传感器 |
| Piezo（压电） | 压力敏感传感器 |
| Strain Gauge（应变片） | 力敏感传感器 |

### 调平方法

| 方法 | 描述 |
|--------|-------------|
| Linear（线性） | 3 点调平 |
| Bilinear（双线性） | 基于网格的调平 |
| Unified Bed Mesh（统一床网） | 高级网格调平 |
| 3-Point（3 点） | 三角调平 |

### 配置

```cpp
// 启用自动热床调平
#define AUTO_BED_LEVELING_BILINEAR

// 探针设置
#define BLTOUCH
#define Z_PROBE_OFFSET_FROM_EXTRUDER { 0, 0, -1.5 }

// 热床调平网格
#define GRID_MAX_POINTS_X 5
#define GRID_MAX_POINTS_Y 5

// 探针边距
#define LEFT_PROBE_BED_POSITION 30
#define RIGHT_PROBE_BED_POSITION 190
#define FRONT_PROBE_BED_POSITION 30
#define BACK_PROBE_BED_POSITION 190
```

## Linear Advance（线性推进）

线性推进在加速和减速期间补偿喷嘴中的压力变化。

```cpp
#define LIN_ADVANCE
#define LIN_ADVANCE_K 0.0
```

### 校准

1. 打印线性推进校准图案。
2. 根据结果调整 K 值。
3. 直驱挤出头使用较低的 K 值。
4. Bowden 挤出头使用较高的 K 值。

| 挤出头类型 | 典型 K 值 |
|---------------|-----------------|
| Direct Drive（直驱） | 0.0 - 0.2 |
| Bowden (short)（短） | 0.2 - 0.7 |
| Bowden (long)（长） | 0.7 - 2.0 |

## S-Curve Acceleration（S 曲线加速度）

S 曲线加速度提供比梯形加速度更平滑的运动。

```cpp
#define S_CURVE_ACCELERATION
```

## Trinamic 驱动配置

### TMC2209 UART 配置

```cpp
#define X_DRIVER_TYPE  TMC2209
#define Y_DRIVER_TYPE  TMC2209
#define Z_DRIVER_TYPE  TMC2209
#define E0_DRIVER_TYPE TMC2209

// UART 连接
#define X_SLAVE_ADDRESS  0
#define Y_SLAVE_ADDRESS  0
#define Z_SLAVE_ADDRESS  0
#define E0_SLAVE_ADDRESS 0

// StealthChop（静音模式）
#define STEALTHCHOP_XY
#define STEALTHCHOP_Z

// 无传感器归位
#define SENSORLESS_HOMING
#define X_STALL_SENSITIVITY  80
#define Y_STALL_SENSITIVITY  80
```

### 电流设置

| 轴 | 典型电流 (mA) |
|------|---------------------|
| X | 800 |
| Y | 800 |
| Z | 800 |
| E0 | 600 |

## LCD 和显示器

### 支持的显示器

| 显示器 | 类型 |
|---------|------|
| RepRapDiscount 12864 | 字符 LCD |
| RepRapDiscount Full Graphic | 单色图形 |
| TFT Color | 彩色触摸屏 |
| DWIN T5 | DGUS 触摸屏 |
| Fysetc Mini 12864 | RGB 背光 |

## G-Code 命令

### 运动命令

| 命令 | 描述 |
|---------|-------------|
| G28 | 归位所有轴 |
| G29 | 自动热床调平 |
| G1 | 线性移动 |
| G0 | 快速移动 |
| G92 | 设置位置 |

### 温度命令

| 命令 | 描述 |
|---------|-------------|
| M104 | 设置热端温度 |
| M109 | 等待热端温度 |
| M140 | 设置热床温度 |
| M190 | 等待热床温度 |
| M106 | 设置风扇速度 |

### 配置命令

| 命令 | 描述 |
|---------|-------------|
| M500 | 保存设置到 EEPROM |
| M501 | 从 EEPROM 加载设置 |
| M502 | 恢复出厂默认 |
| M503 | 报告当前设置 |
| M851 | 设置 Z 探针偏移 |

## PID 调参

```bash
# 调整热端 PID
M303 E0 C8 S210

# 调整热床 PID
M303 E-1 C8 S60

# 保存 PID 值
M301 P22.2 I1.08 D114
M500
```

## 故障排除

| 问题 | 解决方案 |
|-------|----------|
| 热失控 | 检查热敏电阻接线 |
| 层偏移 | 检查皮带张力和驱动电流 |
| 附着力差 | 校准 Z 偏移和热床水平 |
| 拉丝 | 调整回抽和温度 |
| 欠挤出 | 校准 e-steps 和流量率 |
| 过挤出 | 降低流量率 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 备份配置 | 保存配置文件的副本 |
| 启用热保护 | 安全功能，始终保持启用 |
| 使用 S 曲线 | 更平滑的运动减少伪影 |
| 调参 PID | 稳定的温度提高打印质量 |
| 逐步测试 | 一次只更改一个设置 |
| 使用版本控制 | 用 Git 跟踪配置更改 |

## 与 Klipper 的比较

| 方面 | Marlin | Klipper |
|--------|--------|---------|
| 处理 | 仅 MCU | 主机 + MCU |
| 配置 | 重新编译固件 | 编辑文本文件，重启 |
| 步进速率 | 受 MCU 限制 | 非常高（主机 CPU） |
| Web 界面 | 需要 OctoPrint | 内置支持 |
| Input Shaper | 手动校准 | 自动校准 |
| 社区 | 最大的用户群 | 增长中的社区 |

## 结论

Marlin 是最成熟、支持最广泛的 3D 打印机固件。其广泛的配置选项和广泛的硬件支持使其适用于几乎任何 3D 打印机设计，从入门级机器到高级自定义构建。
