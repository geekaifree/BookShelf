# 使用 LinuxCNC 进行 CNC 机床控制

## 简介

LinuxCNC 是一个开源软件系统，用于计算机控制铣床、车床、等离子切割机和机器人等机床。它提供步进电机和伺服电机的实时控制。

### 什么是 CNC？

计算机数控 (CNC) 使用计算机控制机床。LinuxCNC 解释 G-code 指令并将其转换为精确的电机运动。

| 组件 | 功能 |
|------|------|
| 计算机 | 运行 LinuxCNC 软件 |
| 运动控制器 | 生成步进脉冲 |
| 电机 | 驱动机床轴 |
| 机床 | 物理切削工具 |

### LinuxCNC 特性

| 特性 | 描述 |
|------|------|
| 实时控制 | 精确的电机控制时序 |
| G-code 解释器 | 处理加工指令 |
| 刀路显示 | 切削路径可视化 |
| 配置工具 | 机床设置向导 |
| HAL | 硬件抽象层 |

## 系统要求

### 硬件要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 GHz | 2+ GHz 多核 |
| 内存 | 1 GB | 4 GB |
| 存储 | 10 GB | 50 GB |
| 网络 | 可选 | 远程以太网 |

### 实时要求

| 方面 | 要求 |
|------|------|
| 延迟 | < 50 微秒抖动 |
| 内核 | PREEMPT_RT 补丁内核 |
| BIOS | 禁用电源管理 |
| USB | 避免 USB 用于运动控制 |

### 支持的硬件

| 硬件类型 | 示例 |
|----------|------|
| 步进驱动 | TB6600、DM542、Gecko G203V |
| 伺服驱动 | Mesa 7i77、Granite Devices |
| 转接板 | Mesa 7i76、C10 |
| 接口卡 | Mesa 5i25、6i25 |

## 安装

### 安装 LinuxCNC

```bash
# 下载 LinuxCNC ISO
# 从 USB 启动安装
# 或在现有 Debian/Ubuntu 上安装
sudo apt update
sudo apt install linuxcnc-uspace
```

### 安装后设置

```bash
# 检查延迟
latency-test

# 验证安装
linuxcnc --version
```

### 延迟测试

| 延迟值 | 质量 | 用例 |
|--------|------|------|
| < 15,000 ns | 优秀 | 伺服系统 |
| 15,000-30,000 ns | 良好 | 步进系统 |
| 30,000-100,000 ns | 一般 | 基本操作 |
| > 100,000 ns | 差 | 不推荐 |

## 配置

### 配置向导

LinuxCNC 包含分步配置向导：

| 向导 | 用途 |
|------|------|
| 步进配置 | 配置步进电机系统 |
| 伺服配置 | 配置伺服电机系统 |
| 主轴配置 | 配置主轴速度控制 |
| 车床配置 | 配置车床特定设置 |

### INI 文件结构

```ini
[EMC]
MACHINE = My Mill
VERSION = 1.0

[DISPLAY]
DISPLAY = axis
POSITION_OFFSET = RELATIVE
POSITION_FEEDBACK = ACTUAL

[TRAJ]
AXES = 3
COORDINATES = X Y Z
LINEAR_UNITS = inch
ANGULAR_UNITS = degree

[EMCIO]
EMCIO = io
CYCLE_TIME = 0.100
TOOL_TABLE = tool.tbl
```

### 轴配置

```ini
[AXIS_0]
TYPE = LINEAR
HOME = 0.0
MAX_VELOCITY = 5.0
MAX_ACCELERATION = 50.0
SCALE = 4000
MIN_LIMIT = -10.0
MAX_LIMIT = 10.0
```

| 参数 | 描述 |
|------|------|
| TYPE | LINEAR（线性）或 ANGULAR（角度） |
| HOME | 原点位置 |
| MAX_VELOCITY | 最大速度（单位/秒） |
| MAX_ACCELERATION | 最大加速度 |
| SCALE | 每单位步数 |

## 硬件抽象层 (HAL)

### 什么是 HAL？

HAL 允许将软件组件连接在一起，创建自定义控制配置。

| 组件类型 | 示例 |
|----------|------|
| Pin | 输入/输出信号 |
| Signal | 引脚之间的连接 |
| Function | 处理模块 |
| Thread | 执行时序 |

### 基本 HAL 命令

```bash
# 列出所有引脚
halcmd show pin

# 连接信号
halcmd net signal-name pin1 pin2

# 设置值
halcmd setp pin-name value

# 加载组件
halcmd loadrt component_name
```

### HAL 文件示例

```hal
# 加载实时组件
loadrt stepper_gen step_type=0,0,0
loadrt pid names=pid.x,pid.y,pid.z

# 连接步进发生器到位置命令
net x-pos-cmd joint.0.motor-pos-cmd => stepgen.0.position-cmd
net x-pos-fb stepgen.0.position-fb => joint.0.motor-pos-fb

# 连接 PID 控制器
net x-pos-cmd pid.x.command
net x-pos-fb pid.x.feedback
net x-output pid.x.output => stepgen.0.velocity-cmd
```

## G-code 编程

### 基本 G-code 命令

| 代码 | 功能 | 示例 |
|------|------|------|
| G0 | 快速移动 | G0 X10 Y10 |
| G1 | 直线插补 | G1 X10 Y10 F100 |
| G2 | 顺时针圆弧 | G2 X10 Y10 I5 J0 |
| G3 | 逆时针圆弧 | G3 X10 Y10 I5 J0 |
| G90 | 绝对定位 | G90 |
| G91 | 增量定位 | G91 |

### 常用 M-code

| 代码 | 功能 |
|------|------|
| M0 | 程序停止 |
| M1 | 选择性停止 |
| M2 | 程序结束 |
| M3 | 主轴正转 (CW) |
| M4 | 主轴反转 (CCW) |
| M5 | 主轴停止 |
| M6 | 换刀 |
| M8 | 冷却液开 |
| M9 | 冷却液关 |

### 示例程序

```gcode
(Header)
G21 G90 G17

(Tool change)
T1 M6
S1000 M3

(First cut)
G0 X0 Y0 Z5
G1 Z-2 F100
G1 X50 F200
G1 Y50
G1 X0
G1 Y0

(End)
G0 Z25
M5
M2
```

## 刀具管理

### 刀具表

| 刀具 | 描述 | 直径 | 长度 |
|------|------|------|------|
| T1 | 立铣刀 6mm | 6.0 mm | 50 mm |
| T2 | 钻头 3mm | 3.0 mm | 40 mm |
| T3 | 球头铣刀 4mm | 4.0 mm | 45 mm |

### 刀具长度补偿

```gcode
G43 H1 (应用 T1 刀具长度补偿)
G49 (取消刀具长度补偿)
```

## 坐标系

### 工件坐标系

| 代码 | 描述 |
|------|------|
| G54 | 工件坐标系 1 |
| G55 | 工件坐标系 2 |
| G56 | 工件坐标系 3 |
| G57 | 工件坐标系 4 |
| G58 | 工件坐标系 5 |
| G59 | 工件坐标系 6 |

### 设置工件零点

```gcode
G10 L20 P1 X0 Y0 Z0 (将 G54 设为当前位置)
```

## 安全功能

### 急停

| 组件 | 功能 |
|------|------|
| 急停按钮 | 立即停止所有运动 |
| 软件急停 | 软件触发的停止 |
| 限位开关 | 防止超程 |

### 安全配置

```ini
[EMC]
EMCIO = io

[TRAJ]
MAX_VELOCITY = 10.0
MAX_ACCELERATION = 100.0
```

## 常见操作

### 回零序列

```gcode
G28.1 (所有轴回零)
G28 X0 Y0 (返回原点)
```

### 探测

```gcode
G38.2 Z-10 F100 (向下探测)
G92 Z0 (将当前位置设为零)
```

## 故障排除

### 常见问题

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 丢步 | 加速度太高 | 降低最大加速度 |
| 表面质量差 | 振动 | 检查机械刚性 |
| 通信错误 | USB 延迟 | 使用并口或 Mesa 卡 |
| 急停触发 | 限位开关 | 检查接线和配置 |

### 诊断命令

```bash
# 检查 HAL 状态
halcmd show

# 实时监控引脚
halcmd show pin -t

# 查看错误日志
dmesg | grep -i linuxcnc
```

## 总结

| 概念 | 描述 |
|------|------|
| INI 文件 | 机床配置 |
| HAL 文件 | 硬件连接 |
| G-code | 加工指令 |
| 实时 | 精确运动控制 |
| 安全 | 急停和限位开关 |
