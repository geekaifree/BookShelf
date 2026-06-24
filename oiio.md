# OpenImageIO (OIIO): 视觉特效图像处理

## 简介

OpenImageIO (OIIO) 是一个开源库，用于读取、写入和处理视觉特效和动画中常用的图像文件。它为处理数十种图像格式提供了统一接口，以及一套图像处理工具。

OIIO 在专业视觉特效流水线中被广泛使用，作为标准图像 I/O 层，在所有应用之间提供一致的行为。

## 为什么 OIIO 很重要

专业的视觉特效工作涉及多种图像格式、色彩空间和元数据标准。OIIO 提供了一个单一、可靠的库来一致地处理所有这些。

| 挑战 | OIIO 解决方案 |
|------|--------------|
| 多种图像格式 | 统一的读写 API |
| 色彩管理 | 集成 OCIO 支持 |
| 元数据处理 | 标准化的属性访问 |
| 性能 | 多线程分块 I/O |
| 大图像 | 扫描线和分块访问模式 |

## 支持的格式

OIIO 通过其插件架构支持广泛的图像格式。

| 格式 | 扩展名 | 读取 | 写入 | 特性 |
|------|--------|------|------|------|
| OpenEXR | .exr | 是 | 是 | 多通道、深度、分块 |
| TIFF | .tif | 是 | 是 | 多页、ZIP 压缩 |
| PNG | .png | 是 | 是 | 8/16 位、alpha |
| JPEG | .jpg | 是 | 是 | 有损压缩 |
| DICOM | .dcm | 是 | 否 | 医学影像 |
| FITS | .fits | 是 | 是 | 天文学 |
| BMP | .bmp | 是 | 是 | Windows 位图 |
| TGA | .tga | 是 | 是 | Targa 格式 |
| PSD | .psd | 是 | 否 | Photoshop 图层 |
| HEIF/HEIC | .heic | 是 | 否 | 现代压缩格式 |
| WebP | .webp | 是 | 是 | Web 优化 |
| JPEG 2000 | .jp2 | 是 | 是 | 小波压缩 |

## 安装

### 从源码构建

```bash
git clone https://github.com/AcademySoftwareFoundation/oiio.git
cd oiio
mkdir build && cd build
cmake .. -DCMAKE_INSTALL_PREFIX=/usr/local \
         -DUSE_PYTHON=ON \
         -DUSE_OPENGL=ON
make -j$(nproc)
sudo make install
```

### 包管理器

| 平台 | 命令 |
|------|------|
| macOS | `brew install openimageio` |
| Ubuntu | `sudo apt install libopenimageio-dev` |
| Conda | `conda install -c conda-forge openimageio` |
| vcpkg | `vcpkg install openimageio` |

## 核心架构

### ImageSpec

ImageSpec 类描述图像属性。

| 属性 | 类型 | 描述 |
|------|------|------|
| width | int | 图像宽度（像素） |
| height | int | 图像高度（像素） |
| nchannels | int | 通道数量 |
| format | TypeDesc | 像素数据类型 |
| tile_width | int | 分块宽度（扫描线为 0） |
| channelnames | vector | 每通道名称 |
| attribs | map | 任意元数据 |

### ImageBuf

ImageBuf 是在内存中保存图像数据的主要类。

```python
import OpenImageIO as oiio

# 读取图像
buf = oiio.ImageBuf("input.exr")

# 获取图像信息
spec = buf.spec()
print(f"Size: {spec.width} x {spec.height}")
print(f"Channels: {spec.nchannels}")
print(f"Format: {spec.format}")
```

### ImageInput / ImageOutput

这些类为大图像提供流式 I/O。

```python
import OpenImageIO as oiio

# 流式读取
inp = oiio.ImageInput.open("large.exr")
spec = inp.spec()

# 逐扫描线读取
for y in range(spec.height):
    scanline = inp.read_scanline(y, 0)
    # 处理扫描线
inp.close()
```

## Python API

### 读取像素数据

```python
import OpenImageIO as oiio
import numpy as np

# 将整张图像读取为 numpy 数组
buf = oiio.ImageBuf("input.exr")
pixels = buf.get_pixels(oiio.FLOAT)
print(f"Shape: {pixels.shape}")  # (height, width, channels)

# 读取特定区域
region = buf.get_pixels(oiio.FLOAT, roi=oiio.ROI(0, 100, 0, 100))
```

### 写入图像

```python
import OpenImageIO as oiio
import numpy as np

# 创建新图像
spec = oiio.ImageSpec(1920, 1080, 4, oiio.FLOAT)
spec.attribute("compression", "zip")

# 生成渐变数据
data = np.zeros((1080, 1920, 4), dtype=np.float32)
for y in range(1080):
    for x in range(1920):
        data[y, x] = [x/1920.0, y/1080.0, 0.5, 1.0]

# 写入图像
buf = oiio.ImageBuf(spec)
buf.set_pixels(oiio.ROI(), data)
buf.write("gradient.exr")
```

### 图像操作

```python
import OpenImageIO as oiio

# 调整大小
src = oiio.ImageBuf("input.exr")
dst = oiio.ImageBuf()
oiio.ImageBufAlgo.resize(dst, src, roi=oiio.ROI(0, 960, 0, 540))

# 使用 OCIO 进行色彩转换
result = oiio.ImageBuf()
oiio.ImageBufAlgo.colorconvert(result, dst, "acescg", "srgb_display")

# 两张图像相加
added = oiio.ImageBuf()
oiio.ImageBufAlgo.add(added, src, dst)

# 合成（over 操作）
comp = oiio.ImageBuf()
oiio.ImageBufAlgo.over(comp, fg, bg)
```

## 命令行工具

### oiiotool

oiiotool 是一个多功能的命令行图像处理实用工具。

| 操作 | 命令 |
|------|------|
| 获取信息 | `oiiotool --info image.exr` |
| 调整大小 | `oiiotool input.exr --resize 1920x1080 -o output.exr` |
| 转换格式 | `oiiotool input.exr -d uint8 -o output.png` |
| 色彩转换 | `oiiotool --colorconfig ocio.ocio input.exr --colorconvert acescg srgb -o out.exr` |
| 图像相加 | `oiiotool a.exr b.exr --add -o sum.exr` |
| 合并图层 | `oiiotool layered.exr --flatten -o flat.exr` |
| 裁剪 | `oiiotool input.exr --crop 100x100+50+50 -o cropped.exr` |

### oiiotool 流水线

```bash
# 调整大小、色彩转换并添加水印
oiiotool input.exr \
  --resize 1920x1080 \
  --colorconvert acescg srgb_display \
  --text:x=50:y=50:fontsize=24 "Studio Name" \
  -d uint8 -o output.jpg

# 分离通道并重新组合
oiiotool input.exr --ch R,G,B --ch A --appendpaste \
  -o split_output.exr

# 从序列创建联系表
oiiotool --pattern:width=1920:height=1080:channels=3 constant 0.2 0.2 0.2 \
  frame001.exr frame002.exr frame003.exr \
  --mosaic:pad=10 3x1 -o contact_sheet.exr
```

### idiff

比较两张图像并报告差异。

```bash
# 基本比较
idiff image_a.exr image_b.exr

# 输出差异图像
idiff --absdiff -o diff.exr image_a.exr image_b.exr

# 如果 PSNR 低于阈值则失败
idiff --fail 0.001 --warn 0.0001 a.exr b.exr
```

### igrep

搜索图像元数据和文件名。

```bash
# 查找具有特定属性的图像
igrep --attrib "compression" "zip" *.exr

# 按分辨率查找
igrep --res "1920x1080" /path/to/frames/*.exr
```

## 分块和扫描线访问

OIIO 支持两种主要的大图像访问模式。

| 模式 | 最适合 | 内存使用 |
|------|--------|---------|
| 扫描线 | 顺序处理 | 低 |
| 分块 | 随机访问 | 中等 |
| ImageBuf（完整） | 小图像或内存充足时 | 高 |

### 分块图像访问

```python
import OpenImageIO as oiio

# 使用分块访问打开
inp = oiio.ImageInput.open("tiled.exr")
spec = inp.spec()

# 读取单个分块
tw = spec.tile_width
th = spec.tile_height

for ty in range(0, spec.height, th):
    for tx in range(0, spec.width, tw):
        tile = inp.read_tile(tx, ty, 0)
        # 处理分块
inp.close()
```

## 深度图像

深度图像存储每像素可变数量的采样，用于体积渲染和合成。

| 特性 | 扫描线图像 | 深度图像 |
|------|-----------|---------|
| 每像素采样数 | 固定（1） | 可变 |
| 存储 | 规则网格 | 每像素列表 |
| 用例 | 标准渲染 | 体积、深度合成 |
| 文件大小 | 可预测 | 取决于内容 |

```python
import OpenImageIO as oiio

# 读取深度数据
inp = oiio.ImageInput.open("deep.exr")
spec = inp.spec()

# 读取像素的深度采样
samples = inp.read_deep_pixel(0, 0)
print(f"Number of samples: {len(samples)}")
```

## 元数据和属性

OIIO 提供标准化的图像元数据访问。

| 属性 | 访问方法 | 示例 |
|------|---------|------|
| 图像描述 | `spec.attribute("ImageDescription")` | "Shot 010 comp v3" |
| 压缩 | `spec.attribute("compression")` | "zip" |
| 像素宽高比 | `spec.attribute("PixelAspectRatio")` | 1.0 |
| 显示窗口 | `spec.attribute("displayWindow")` | 完整图像边界 |
| 数据窗口 | `spec.attribute("dataWindow")` | 活动区域 |
| 自定义元数据 | `spec.attribute("custom_key")` | 任意值 |

## 多通道图像

视觉特效图像通常包含超出标准 RGBA 的许多通道。

```python
import OpenImageIO as oiio

spec = oiio.ImageSpec(1920, 1080, 7, oiio.FLOAT)
spec.channelnames = ["R", "G", "B", "A", "depth", "motion.x", "motion.y"]

# 写入多通道 EXR
buf = oiio.ImageBuf(spec)
buf.write("multichannel.exr")

# 读取特定通道
buf = oiio.ImageBuf("multichannel.exr")
ch = oiio.ImageBuf()
oiio.ImageBufAlgo.channels(ch, buf, (0, 1, 2, 3))  # 仅提取 RGBA
```

## 与视觉特效工具的集成

| 工具 | OIIO 用途 |
|------|----------|
| Blender | 图像 I/O 后端 |
| Nuke | 可选图像格式支持 |
| Gaffer | 主要图像处理 |
| MaterialX | 纹理处理 |
| USD | 纹理资产处理 |
| OpenShadingLanguage | 纹理查找 |

## 性能提示

| 提示 | 实现方式 |
|------|---------|
| 使用分块 EXR | 将分块大小设为 64x64 或 128x128 |
| 多线程 | OIIO 自动检测核心数；设置 OIIO_THREADS |
| 流式处理用扫描线 | 避免加载整个大图像 |
| 压缩 I/O | EXR 使用 ZIP 或 PIZ 压缩 |
| 内存映射 | 对大文件只读访问启用 |
| 避免复制 | 使用基于 ROI 的操作而非完整复制 |

## 附加资源

| 资源 | URL |
|------|-----|
| 官方文档 | openimageio.org |
| GitHub 仓库 | github.com/AcademySoftwareFoundation/oiio |
| Python API 参考 | openimageio.org/python |
| 邮件列表 | groups.google.com/g/openimageio |
