# OpenColorIO (OCIO): 影视和视觉特效的色彩管理

## 简介

OpenColorIO (OCIO) 是一个开源色彩管理框架，专为电影、动画和视觉特效工作流设计。它在不同应用和制作阶段之间提供一致的色彩处理。

无论你是在 Nuke 中合成、在 Blender 中渲染还是在 DaVinci Resolve 中调色，OCIO 都能确保色彩显示正确。没有适当的色彩管理，同一图像在不同工具之间可能看起来完全不同，导致代价高昂的返工。

## 为什么色彩管理很重要

在专业视觉特效流水线中，图像会经过多个应用。每个工具可能以不同方式解释色彩数据。OCIO 通过集中化色彩变换规则来解决这个问题。

| 问题 | 没有 OCIO | 使用 OCIO |
|------|-----------|-----------|
| 色彩不一致 | 不同应用显示不同 | 统一外观 |
| 流水线交接 | 手动调整色彩 | 自动变换 |
| 显示准确性 | 靠猜测 | 校准输出 |
| 存档/检索 | 色彩数据可能丢失 | 完整记录的变换 |

## 核心概念

### 色彩空间

色彩空间定义了数值如何映射到实际颜色。OCIO 区分几种类别。

| 色彩空间类型 | 用途 | 示例 |
|-------------|------|------|
| 场景参考 | 表示场景中的光线 | ACEScg, Linear sRGB |
| 显示参考 | 表示显示器上的颜色 | sRGB, Rec. 709 |
| 角色 | 应用的命名引用 | compositing_linear, color_picking |
| 数据 | 非颜色数据（法线、遮罩） | Raw |

### 变换

变换将数据从一个色彩空间转换到另一个。OCIO 支持多种变换类型。

| 变换类型 | 描述 | 用例 |
|---------|------|------|
| MatrixTransform | 3x3 或 4x4 矩阵乘法 | 线性色彩空间转换 |
| ExponentTransform | 幂函数 | Gamma 校正 |
| CDLTransform | 色彩决策列表 | 现场外观管理 |
| LookTransform | 命名创意外观 | 应用节目 LUT |
| FileTransform | 外部 LUT 文件 | 供应商特定 LUT |
| GradingPrimaryTransform | Lift/Gamma/Gain | 调色调整 |

### 角色

角色是色彩空间的命名别名。它们让应用无需知道确切名称即可引用色彩空间。

| 角色名称 | 典型分配 | 用途 |
|---------|---------|------|
| scene_linear | ACEScg 或 Linear | 合成和渲染 |
| compositing_log | ACEScc 或 Log | Log 空间合成 |
| color_picking | sRGB | UI 取色器 |
| texture_paint | sRGB | 纹理绘制 |
| reference | ACES 2065-1 | 存档交换 |

## 安装

### 从源码构建

```bash
git clone https://github.com/AcademySoftwareFoundation/ocio.git
cd ocio
mkdir build && cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/usr/local
make -j$(nproc)
sudo make install
```

### 使用包管理器

| 平台 | 命令 |
|------|------|
| macOS (Homebrew) | `brew install opencolorio` |
| Ubuntu/Debian | `sudo apt install libopencolorio-dev` |
| Windows (vcpkg) | `vcpkg install opencolorio` |
| Python (pip) | `pip install opencolorio` |

## 配置文件

OCIO 使用 YAML 配置文件来定义所有色彩空间、变换和角色。

### 基本结构

```yaml
ocio_profile_version: 2

roles:
  scene_linear: acescg
  compositing_log: acescc
  color_picking: srgb_texture

colorspaces:
  - name: acescg
    family: ACES
    description: ACEScg linear color space
    to_reference:
      !<MatrixTransform> {matrix: [1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1]}

  - name: srgb_texture
    family: sRGB
    description: sRGB texture color space
    to_reference:
      !<FileTransform> {src: srgb_to_linear.spi1d, interpolation: linear}

displays:
  sRGB:
    - !<ViewTransform> {name: ACES, view_transform: aces_output, display_colorspace: srgb_display}
```

### 内置配置

OCIO 附带多个标准配置。

| 配置 | 用例 | 包含的色彩空间 |
|------|------|---------------|
| studio-config | 完整电影流水线 | 100+ 空间 |
| cg-config | CG/VFX 专注 | ACES, sRGB, Rec.709 |
| nuke-default | Nuke 兼容性 | 传统 Nuke 空间 |
| spi-vfx | SPI 制作 | 工作室特定 |

## Python API

OCIO 提供全面的 Python API 用于编程式色彩管理。

### 列出色彩空间

```python
import PyOpenColorIO as ocio

config = ocio.GetCurrentConfig()

for cs in config.getColorSpaces():
    print(f"Name: {cs.getName()}")
    print(f"Family: {cs.getFamily()}")
    print(f"Description: {cs.getDescription()}")
```

### 应用变换

```python
import PyOpenColorIO as ocio

config = ocio.GetCurrentConfig()

# 创建从 scene_linear 到 sRGB display 的处理器
processor = config.getProcessor("scene_linear", "srgb_display")

# 应用到像素值 (R, G, B, A)
cpu = processor.getDefaultCPUProcessor()
pixel = [0.5, 0.3, 0.8, 1.0]
result = cpu.applyRGBA(pixel)
print(f"Input:  {pixel}")
print(f"Output: {result}")
```

### 创建烘焙 LUT

```python
import PyOpenColorIO as ocio

config = ocio.GetCurrentConfig()

# 定义源和目标
src = "acescg"
dst = "srgb_display"

processor = config.getProcessor(src, dst)

# 创建 3D LUT
baker = ocio.Baker()
baker.setConfig(config)
baker.setFormat("cinespace")
baker.setCubeSize(32)
baker.setInputSpace(src)
baker.setTargetSpace(dst)

# 将 LUT 写入文件
with open("aces_to_srgb.cube", "w") as f:
    f.write(baker.bake())
```

## 与视觉特效应用的集成

| 应用 | OCIO 支持 | 集成方式 |
|------|----------|---------|
| Nuke | 完全原生 | 内置 OCIO 节点 |
| Blender | 完全原生 | 色彩管理设置 |
| Houdini | 完全原生 | OCIO VOP 节点 |
| Maya | 部分 | 第三方插件 |
| DaVinci Resolve | 原生 | ACES 和自定义配置 |
| Natron | 完全原生 | OCIOColorSpace 节点 |

## ACES 工作流

学院色彩编码系统 (ACES) 是 OCIO 最常见的用例。

### ACES 流水线阶段

| 阶段 | 色彩空间 | 用途 |
|------|---------|------|
| 捕获 | 摄像机原生 | 原始传感器数据 |
| 输入变换 | ACES 2065-1 (AP0) | 转换为 ACES 参考 |
| 工作空间 | ACEScg (AP1) | 合成和渲染 |
| 外观 | ACEScc 或 ACEScct | 创意调色 |
| 输出变换 | 显示参考 | 最终显示器输出 |

### 常见 ACES 变换

| 从 | 到 | 变换 |
|----|----|----|
| Camera LogC | ACEScg | 输入设备变换 (IDT) |
| ACEScg | sRGB | 输出变换 (ODT) |
| ACEScg | ACEScc | ACES 到 Log |
| ACES 2065-1 | Rec.2020 | 参考到显示 |

## 命令行工具

OCIO 包含多个命令行实用工具。

| 工具 | 用途 | 示例 |
|------|------|------|
| ociocheck | 验证配置 | `ociocheck config.ocio` |
| ociobakelut | 烘焙 LUT 文件 | `ociobakelut -lut film.look output.cube` |
| ocioperf | 性能测试 | `ocioperf --config config.ocio` |

### 从命令行烘焙 LUT

```bash
# 创建用于 gamma 校正的 1D LUT
ociobakelut --format houdini --shaperspace log --iconfig config.ocio \
  acescg srgb_display output.lut

# 创建 3D LUT
ociobakelut --format cinespace --cubesize 32 \
  acescg srgb_display output_3d.cube
```

## OCIO v2 特性

版本 2 引入了重大改进。

| 特性 | 描述 | 好处 |
|------|------|------|
| GPU 渲染器 | HLSL/GLSL 着色器生成 | 实时预览 |
| 内置变换 | 按名称引用 | 更小的配置文件 |
| 分级变换 | CDL 和初级调色 | 现场工作流 |
| 动态属性 | 运行时可调值 | 交互式工具 |
| 配置归档 | 自包含包 | 可靠共享 |
| 命名变换 | 面向用户的变换 | 简化 UI |

## 最佳实践

### 配置管理

| 实践 | 建议 |
|------|------|
| 版本控制 | 将配置与项目文件一起存储在 Git 中 |
| 命名约定 | 使用小写加下划线 |
| 角色 | 始终定义常见角色以确保应用兼容性 |
| 显示/视图 | 至少定义 sRGB 和 Rec.709 显示 |
| 文档 | 为所有色彩空间添加描述 |

### 性能优化

| 优化 | 实现方式 |
|------|---------|
| 预烘焙 LUT | 对静态变换使用 ociobakelut |
| 缓存处理器 | 在脚本中重用处理器对象 |
| GPU 着色器 | 为交互式工作启用 GPU 处理 |
| 最小化链深度 | 尽可能简化变换链 |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|---------|---------|
| 配置无法加载 | YAML 语法错误 | 对文件运行 ociocheck |
| 查看器中颜色错误 | 显示设置不匹配 | 验证显示/视图分配 |
| 缺少色彩空间 | 配置中缺少该空间 | 使用 API 检查可用空间 |
| LUT 色带 | 立方体尺寸太小 | 增加立方体尺寸（32 或 64） |
| 性能问题 | 复杂变换链 | 烘焙中间 LUT |

## 附加资源

| 资源 | URL |
|------|-----|
| 官方文档 | opencolorio.org |
| GitHub 仓库 | github.com/AcademySoftwareFoundation/ocio |
| ACES Central | acescentral.com |
| OCIO 配置仓库 | github.com/AcademySoftwareFoundation/OpenColorIO-Config-ACES |
