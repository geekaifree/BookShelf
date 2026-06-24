# OpenEXR: 高动态范围图像格式

## 简介

OpenEXR 是视觉特效和电影制作行业的标准高动态范围 (HDR) 图像文件格式。由 Industrial Light & Magic (ILM) 开发，现由学院软件基金会维护，OpenEXR 是专业视觉特效流水线中存储渲染帧、合成元素和纹理贴图的主要格式。

## 为什么选择 OpenEXR？

标准图像格式如 JPEG 和 PNG 使用 8 位整数值，限制了它们能表示的颜色和亮度范围。OpenEXR 支持浮点数据，能够捕获场景中光线的完整范围。

| 特性 | JPEG/PNG | OpenEXR |
|------|----------|---------|
| 位深度 | 8 位整数 | 16/32 位浮点 |
| 动态范围 | 有限（0-255） | 几乎无限 |
| 色彩空间 | sRGB | 场景参考线性 |
| 通道 | RGB(A) | 无限命名通道 |
| 压缩 | 有损或无损 | 无损选项 |
| 元数据 | 基本 | 丰富的自定义属性 |
| 分块 | 否 | 是 |
| 深度数据 | 否 | 是 |

## 文件结构

OpenEXR 文件由头部和像素数据组成。

### 头部组件

| 组件 | 描述 | 示例 |
|------|------|------|
| 显示窗口 | 完整图像边界 | (0,0) 到 (1920,1080) |
| 数据窗口 | 活动像素区域 | 可能小于显示窗口 |
| 通道 | 命名像素通道 | R, G, B, A, depth, velocity |
| 压缩 | 数据压缩方法 | ZIP, PIZ, DWAA |
| 行序 | 扫描线排列 | 递增 Y |
| 属性 | 自定义元数据 | 摄像机、帧号 |

### 通道类型

| 类型 | 位数 | 范围 | 用例 |
|------|------|------|------|
| HALF | 16 | -65504 到 65504 | 颜色数据、节省存储 |
| FLOAT | 32 | 完全精度 | 深度、速度、合成 |
| UINT | 32 | 0 到 40 亿 | ID、标签 |

## 压缩方法

OpenEXR 提供多种针对不同内容类型优化的压缩算法。

| 方法 | 压缩比 | 速度 | 最适合 |
|------|--------|------|--------|
| NONE | 1:1 | 最快 | 调试、临时文件 |
| RLE | ~2:1 | 快 | 简单图像、遮罩 |
| ZIP（单行） | ~3:1 | 中等 | 扫描线图像 |
| ZIP（多行） | ~3.5:1 | 中等 | 扫描线图像 |
| PIZ | ~2.5:1 | 中等 | 噪声渲染 |
| PXR24 | ~3:1 | 快 | CG 渲染（有损 half） |
| B44 | ~4:1 | 快 | 预览、背景 |
| DWAA | ~10:1 | 慢 | 有损、感知质量 |
| DWAB | ~20:1 | 慢 | 重有损压缩 |

### 选择压缩

| 用例 | 推荐压缩 | 原因 |
|------|---------|------|
| 最终渲染 | ZIP 多行 | 良好压缩比、无损 |
| 合成元素 | ZIP 多行 | 需要无损 |
| 纹理 | PIZ 或 ZIP | 适合噪声数据 |
| 预览/审阅 | DWAA | 可接受小文件 |
| 深度图像 | ZIP 或 PIZ | 深度数据兼容性 |
| 存档 | ZIP 多行 | 最佳无损压缩比 |

## 读取 OpenEXR 文件

### Python 使用 openexr

```python
import OpenEXR
import Imath
import numpy as np

# 打开 EXR 文件
exr = OpenEXR.InputFile("render.exr")

# 获取头部信息
header = exr.header()
dw = header["dataWindow"]
width = dw.max.x - dw.min.x + 1
height = dw.max.y - dw.min.y + 1

print(f"Size: {width} x {height}")
print(f"Channels: {list(header['channels'].keys())}")
print(f"Compression: {header['compression']}")

# 读取 RGB 通道
FLOAT = Imath.PixelType(Imath.PixelType.FLOAT)
channels = exr.channel("R", FLOAT), exr.channel("G", FLOAT), exr.channel("B", FLOAT)

# 转换为 numpy
r = np.frombuffer(channels[0], dtype=np.float32).reshape(height, width)
g = np.frombuffer(channels[1], dtype=np.float32).reshape(height, width)
b = np.frombuffer(channels[2], dtype=np.float32).reshape(height, width)

rgb = np.stack([r, g, b], axis=-1)
```

### Python 使用 OpenImageIO

```python
import OpenImageIO as oiio

buf = oiio.ImageBuf("render.exr")
spec = buf.spec()

print(f"Resolution: {spec.width} x {spec.height}")
print(f"Channels: {spec.nchannels}")
print(f"Compression: {spec.get_string_attribute('compression')}")
print(f"Pixel aspect: {spec.get_float_attribute('PixelAspectRatio')}")
```

### C++ API

```cpp
#include <OpenEXR/ImfRgbaFile.h>
#include <OpenEXR/ImfArray.h>

using namespace OPENEXR_IMF_NAMESPACE;

// 读取半精度浮点 RGBA 图像
RgbaInputFile file("render.exr");
Box2i dw = file.dataWindow();
int width = dw.max.x - dw.min.x + 1;
int height = dw.max.y - dw.min.y + 1;

Array2D<Rgba> pixels(height, width);
file.setFrameBuffer(&pixels[0][0], 1, width);
file.readPixels(dw.min.y, dw.max.y);
```

## 写入 OpenEXR 文件

### Python

```python
import OpenEXR
import Imath
import numpy as np

# 准备图像数据
width, height = 1920, 1080
r = np.random.rand(height, width).astype(np.float32)
g = np.random.rand(height, width).astype(np.float32)
b = np.random.rand(height, width).astype(np.float32)

# 定义头部
header = OpenEXR.Header(width, height)
header["compression"] = OpenEXR.ZIP_COMPRESSION
header["custom_data"] = "shot_010_v3"

# 写入文件
exr = OpenEXR.OutputFile("output.exr", header)
exr.writePixels({
    "R": r.tobytes(),
    "G": g.tobytes(),
    "B": b.tobytes()
})
```

### 写入多通道 EXR

```python
import OpenEXR
import Imath
import numpy as np

width, height = 1920, 1080

header = OpenEXR.Header(width, height)
header["channels"] = {
    "R": Imath.Channel(Imath.PixelType(Imath.PixelType.FLOAT)),
    "G": Imath.Channel(Imath.PixelType(Imath.PixelType.FLOAT)),
    "B": Imath.Channel(Imath.PixelType(Imath.PixelType.FLOAT)),
    "A": Imath.Channel(Imath.PixelType(Imath.PixelType.FLOAT)),
    "depth.Z": Imath.Channel(Imath.PixelType(Imath.PixelType.FLOAT)),
    "motion.x": Imath.Channel(Imath.PixelType(Imath.PixelType.FLOAT)),
    "motion.y": Imath.Channel(Imath.PixelType(Imath.PixelType.FLOAT)),
}

# 生成示例数据
data = {}
for name in ["R", "G", "B", "A"]:
    data[name] = np.ones((height, width), dtype=np.float32).tobytes()
data["depth.Z"] = np.random.rand(height, width).astype(np.float32).tobytes()
data["motion.x"] = np.zeros((height, width), dtype=np.float32).tobytes()
data["motion.y"] = np.zeros((height, width), dtype=np.float32).tobytes()

exr = OpenEXR.OutputFile("multichannel.exr", header)
exr.writePixels(data)
```

## 分块 EXR 文件

分块图像以矩形块而非扫描线存储数据。

| 特性 | 扫描线 | 分块 |
|------|--------|------|
| 访问模式 | 顺序行 | 随机分块访问 |
| Mipmap | 否 | 是 |
| 内存使用 | 流式处理时低 | 中等 |
| 最适合 | 全帧合成 | 纹理流式处理 |

### 创建分块图像

```python
import OpenEXR
import Imath

header = OpenEXR.Header(1920, 1080)
header["tiles"] = OpenEXR.TileDescription(64, 64, OpenEXR.ONE_LEVEL)

exr = OpenEXR.TiledOutputFile("tiled.exr", header)
# 写入分块数据...
```

## 深度 EXR 文件

深度图像存储每像素可变数量的采样，对体积渲染至关重要。

| 方面 | 平面图像 | 深度图像 |
|------|---------|---------|
| 每像素采样数 | 1 | 可变 |
| 存储 | 固定网格 | 每像素数组 |
| 合成 | 标准 over | 深度感知 |
| 文件大小 | 可预测 | 取决于内容 |

```python
import OpenEXR
import numpy as np

# 深度图像数据：每像素的采样列表
deep_data = {
    (100, 200): [
        {"R": 0.5, "G": 0.3, "B": 0.8, "A": 0.9, "Z": 10.0},
        {"R": 0.2, "G": 0.1, "B": 0.4, "A": 0.5, "Z": 15.0},
    ],
    (100, 201): [
        {"R": 1.0, "G": 1.0, "B": 1.0, "A": 1.0, "Z": 5.0},
    ],
}
```

## 多部分 EXR

多部分文件在一个文件中存储多个独立图像。

| 用例 | 部分内容 | 好处 |
|------|---------|------|
| 多视图 | 左眼、右眼 | 立体合成 |
| 多图层 | 美术、漫反射、高光 | 灵活合成 |
| 多帧 | 帧 1、帧 2、... | 单文件序列 |

## 标准属性

OpenEXR 定义了许多标准元数据属性。

| 属性 | 类型 | 描述 |
|------|------|------|
| displayWindow | Box2i | 完整图像范围 |
| dataWindow | Box2i | 活动像素区域 |
| pixelAspectRatio | float | 像素形状比 |
| screenWindowCenter | V2f | 投影中心 |
| compression | enum | 压缩方法 |
| chromaticities | Chromaticities | 色彩原色 |
| whiteLuminance | float | 白点亮度 |
| owner | string | 版权所有者 |
| comments | string | 用户注释 |
| capDate | string | 捕获日期/时间 |
| focus | float | 摄像机焦距 |
| expTime | float | 曝光时间 |
| aperture | float | 镜头光圈 |
| isoSpeed | float | ISO 感光度 |
| timeCode | Timecode | SMPTE 时间码 |

## 最佳实践

### 存储和性能

| 实践 | 建议 |
|------|------|
| 压缩 | 最终帧使用 ZIP 多行 |
| 分块大小 | 纹理用 64x64，帧用 256x256 |
| 通道精度 | 颜色用 HALF，深度/速度用 FLOAT |
| 数据窗口 | 裁剪到活动区域以节省空间 |
| 命名 | 使用 show_shot_version_frame.ext 约定 |

### 流水线考量

| 考量 | 指导 |
|------|------|
| 色彩管理 | 存储线性场景参考数据 |
| 元数据 | 包含摄像机、镜头、帧信息 |
| 深度图像 | 用于体积和运动模糊 |
| 多部分 | 用于多图层合成 |
| 验证 | 检查像素宽高比和数据窗口 |

## 命令行工具

OpenEXR 库包含多个实用工具。

| 工具 | 用途 | 示例 |
|------|------|------|
| exrheader | 显示文件头部 | `exrheader render.exr` |
| exrstdattr | 修改标准属性 | `exrstdattr -comment "v3" in.exr out.exr` |
| exrmaketiled | 创建分块版本 | `exrmaketiled in.exr out.exr` |
| exrenvmap | 生成环境贴图 | `exrenvmap -o latlong.exr input.exr` |
| exrmultipart | 合并/分离多部分 | `exrmultipart -combine parts.exr out.exr` |

## 附加资源

| 资源 | URL |
|------|-----|
| OpenEXR 网站 | openexr.com |
| GitHub 仓库 | github.com/AcademySoftwareFoundation/openexr |
| 技术介绍 | openexr.com/documentation |
| ILM OpenEXR 指南 | openexr.com/docs |
