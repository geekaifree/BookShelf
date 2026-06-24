# Klipper：带主机控制的 3D 打印机固件

## 简介

Klipper 是一款 3D 打印机固件，结合了主机计算机（如 Raspberry Pi）的处理能力和微控制器的实时能力。它将计算卸载到主机，从而实现传统固件无法支持的功能。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Klipper3d/klipper |
| 许可证 | GPL-3.0 |
| 语言 | C, Python |
| 主机 | Linux (Raspberry Pi, PC) |
| MCU | AVR, STM32, RP2040 等 |

## Klipper 工作原理

Klipper 使用两部分架构。

| 组件 | 角色 |
|-----------|------|
| Host (Linux) | 运行运动学、G-code 处理和 Web 界面 |
| MCU（打印机主板） | 执行实时步进生成和读取传感器 |

主机软件计算步进电机运动，并通过串行或 USB 连接向 MCU 发送定时命令。

## 主要功能

| 功能 | 描述 |
|---------|-------------|
| 高步进速率 | 实现比传统固件更高的步进速率 |
| 精确定时 | Linux 主机提供微秒级精确定时 |
| Input Shaper（输入整形） | 减少振铃和重影伪影 |
| Pressure Advance（压力补偿） | 补偿耗材压力变化 |
| Firmware Retraction（固件回抽） | 软件控制的回抽 |
| Bed Mesh Leveling（床网调平） | 自动热床补偿 |
| Multi-MCU Support（多 MCU 支持） | 控制多个微控制器 |
| Macros（宏） | 用 Jinja2 编写的自定义 G-code 命令 |

## 安装

### 前提条件

| 要求 | 描述 |
|-------------|-------------|
| 主机计算机 | Raspberry Pi 3+ 或 Linux PC |
| MicroSD 卡 | 8 GB 或更大，用于主机操作系统 |
| 网络 | Wi-Fi 或以太网连接 |
| 打印机主板 | 兼容的微控制器 |

### 第 1 步：在主机上安装

```bash
# 克隆仓库
git clone https://github.com/Klipper3d/klipper
cd klipper

# 运行安装脚本
./scripts/install-octopi.sh
```

### 第 2 步：配置 MCU

```bash
# 配置固件
make menuconfig

# 构建固件
make

# 刷写固件（因主板而异）
make flash FLASH_DEVICE=/dev/ttyUSB0
```

### 第 3 步：配置打印机

编辑配置文件 `~/printer_data/config/printer.cfg`。

## 配置

### 基本打印机配置

```ini
[printer]
kinematics: cartesian
max_velocity: 300
max_accel: 3000
max_z_velocity: 5
max_z_accel: 100

[stepper_x]
step_pin: PF0
dir_pin: PF1
enable_pin: !PD7
microsteps: 16
rotation_distance: 40
endstop_pin: ^PE5
position_endstop: 0
position_max: 220

[stepper_y]
step_pin: PF6
dir_pin: !PF7
enable_pin: !PF2
microsteps: 16
rotation_distance: 40
endstop_pin: ^PJ1
position_endstop: 0
position_max: 220

[stepper_z]
step_pin: PL3
dir_pin: PL1
enable_pin: !PK0
microsteps: 16
rotation_distance: 8
endstop_pin: ^PD3
position_endstop: 0.5
position_max: 250

[extruder]
step_pin: PA4
dir_pin: !PA6
enable_pin: !PA2
microsteps: 16
rotation_distance: 33.500
nozzle_diameter: 0.400
filament_diameter: 1.750
heater_pin: PB4
sensor_type: ATC Semitec 104NT-4-R025H42G
sensor_pin: PK5
min_temp: 0
max_temp: 260

[heater_bed]
heater_pin: PH5
sensor_type: EPCOS 100K B57560G104F
sensor_pin: PK6
min_temp: 0
max_temp: 130
```

### 运动学类型

| 类型 | 描述 |
|------|-------------|
| cartesian | 标准 X/Y/Z 运动（如 Ender 3） |
| corexy | CoreXY 运动系统（如 Voron） |
| delta | Delta 打印机几何 |
| rotary_delta | 旋转 Delta 机构 |
| polar | 极坐标系统 |
| winch | 绳索驱动系统 |
| none | 无运动学（仅手动控制） |

## 温度配置

### 热敏电阻类型

| 类型 | 描述 |
|------|-------------|
| EPCOS 100K | 常见 NTC 热敏电阻 |
| ATC Semitec 104GT-2 | 高温热敏电阻 |
| SliceEngineering 450C | 高温热电偶 |
| PT100 | 铂金 RTD 传感器 |
| PT1000 | 铂金 RTD 传感器（更高电阻） |

### PID 调参

```bash
# 调整热端 PID
PID_CALIBRATE HEATER=extruder TARGET=210

# 调整热床 PID
PID_CALIBRATE HEATER=heater_bed TARGET=60

# 保存配置
SAVE_CONFIG
```

## Input Shaper（输入整形）

输入整形通过补偿机械共振来减少振铃伪影。

### 校准

```bash
# 测量共振频率
SHAPER_CALIBRATE

# 测试特定轴
SHAPER_CALIBRATE AXIS=X
SHAPER_CALIBRATE AXIS=Y
```

### 整形器类型

| 类型 | 描述 |
|------|-------------|
| mzv | 适用于大多数打印机 |
| ei | 更适合较高频率 |
| 2hump_ei | 用于多个共振峰 |
| 3hump_ei | 用于复杂的共振模式 |

## Pressure Advance（压力补偿）

压力补偿在加速和减速期间补偿耗材流动的延迟。

```ini
[extruder]
pressure_advance: 0.04
pressure_advance_smooth_time: 0.040
```

### 校准

```bash
# 运行测试图案
TUNING_TOWER COMMAND=SET_VELOCITY_LIMIT PARAMETER=VELOCITY START=50 FACTOR=2
```

## Bed Mesh Leveling（床网调平）

```ini
[bed_mesh]
probe_count: 5, 5
speed: 120
horizontal_move_z: 5
mesh_min: 30, 30
mesh_max: 190, 190
```

### 使用

```bash
# 探测热床
BED_MESH_CALIBRATE

# 加载已保存的网格
BED_MESH LOAD=default

# 清除网格
BED_MESH CLEAR
```

## Web 界面

Klipper 与 Web 界面配合使用，实现远程控制。

| 界面 | 描述 |
|-----------|-------------|
| Mainsail | 现代、响应式 Web 界面 |
| Fluidd | 功能丰富的 Web 界面 |
| OctoPrint | 基于插件的 Web 界面 |

## 宏

自定义宏扩展了 Klipper 的功能。

```ini
[gcode_macro START_PRINT]
gcode:
    G28                           ; 归位所有轴
    BED_MESH_CALIBRATE            ; 热床调平
    G1 Z5 F3000                  ; 抬高喷嘴
    M109 S{params.EXTRUDER_TEMP} ; 等待热端
    M190 S{params.BED_TEMP}      ; 等待热床

[gcode_macro END_PRINT]
gcode:
    M104 S0                      ; 关闭热端
    M140 S0                      ; 关闭热床
    G91                          ; 相对定位
    G1 Z10 F3000                ; 抬高喷嘴
    G90                          ; 绝对定位
    G1 X0 Y200 F5000            ; 展示打印件
    M84                          ; 禁用步进电机
```

## 故障排除

| 问题 | 解决方案 |
|-------|----------|
| MCU 连接错误 | 检查 USB 线和串口 |
| 温度失控 | 验证热敏电阻接线 |
| 层偏移 | 降低加速度或检查皮带张力 |
| 附着力差 | 校准 Z 偏移和床网 |
| 拉丝 | 调整回抽和压力补偿 |

## 与传统固件的比较

| 方面 | Klipper | Marlin |
|--------|---------|--------|
| 处理 | 主机 CPU | 仅 MCU |
| 步进速率 | 非常高 | 受 MCU 速度限制 |
| 配置 | 文本文件，热重载 | 重新编译固件 |
| Input Shaper | 内置 | 手动或不可用 |
| Web 界面 | 原生支持 | 需要 OctoPrint |
| 可扩展性 | Python 宏 | 有限 |

## 结论

Klipper 为 3D 打印机控制提供了一个强大而灵活的平台。其架构利用主机计算机的处理能力来提供改进打印质量和简化配置的高级功能。
