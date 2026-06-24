# 图像处理与VFX

> 本文档整合了以下源文件：image.md, imageLib.md, imageIo.md, oiio.md, ocio.md, hdr.md, openexr.md, openimageio.md, paint.md, vector.md, viewer.md

---

## 来源：image.md

## 简介

GIMP（GNU Image Manipulation Program）是一款免费的开源图像编辑器，适用于照片修图、图像合成和平面设计。它提供了与商业软件相当的专业级工具。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| CPU | 2 核 | 4 核 |
| 内存 | 2 GB | 8 GB |
| 磁盘 | 200 MB | 1 GB |
| 显示 | 1024x768 | 1920x1080 |
| 操作系统 | Windows/macOS/Linux | 任意 |

## 安装

| 平台 | 方法 |
|------|------|
| Windows | 从 gimp.org 下载安装包 |
| macOS | 从 gimp.org 下载 DMG 或使用 Homebrew |
| Ubuntu/Debian | `sudo apt install gimp` |
| Fedora | `sudo dnf install gimp` |
| Flatpak | `flatpak install org.gimp.GIMP` |
| Snap | `snap install gimp` |

## 界面概览

| 窗口 | 用途 |
|------|------|
| 工具箱 | 工具选择和选项 |
| 图像窗口 | 主编辑画布 |
| 图层面板 | 图层管理 |
| 通道面板 | 颜色通道编辑 |
| 路径面板 | 矢量路径管理 |
| 历史面板 | 撤销历史 |

## 工具参考

### 选择工具

| 工具 | 快捷键 | 用途 |
|------|--------|------|
| 矩形选择 | R | 矩形选区 |
| 椭圆选择 | E | 圆形/椭圆选区 |
| 自由选择 | F | 套索式选择 |
| 模糊选择 | U | 魔棒（按颜色） |
| 按颜色 | Shift+O | 选择所有匹配颜色 |
| 剪刀 | I | 智能边缘选择 |
| 前景选择 | 手动 | 提取前景对象 |

### 变换工具

| 工具 | 快捷键 | 用途 |
|------|--------|------|
| 移动 | M | 移动图层或选区 |
| 旋转 | Shift+R | 旋转元素 |
| 缩放 | Shift+S | 调整元素大小 |
| 错切 | Shift+H | 倾斜元素 |
| 透视 | Shift+P | 改变透视 |
| 翻转 | Shift+F | 水平或垂直镜像 |
| 笼式变换 | 手动 | 自由变形 |

### 绘画工具

| 工具 | 快捷键 | 用途 |
|------|--------|------|
| 桶填充 | Shift+B | 用颜色填充区域 |
| 渐变 | L | 渐变填充 |
| 铅笔 | N | 硬边绘制 |
| 画笔 | P | 软边绘制 |
| 橡皮擦 | E | 擦除像素 |
| 喷枪 | A | 喷枪效果 |
| 墨水 | K | 书法笔 |
| 克隆 | C | 克隆图章 |
| 修复 | H | 修复工具 |
| 模糊/锐化 | Shift+U | 模糊或锐化区域 |
| 涂抹 | S | 涂抹像素 |
| 减淡/加深 | Shift+D | 变亮或变暗 |

### 颜色工具

| 工具 | 用途 |
|------|------|
| 色彩平衡 | 调整颜色通道 |
| 色相-饱和度 | 修改色相、饱和度、亮度 |
| 色温 | 暖色或冷色调 |
| 曲线 | 精确色调调整 |
| 色阶 | 黑白点调整 |
| 阈值 | 转换为黑白 |
| 色调分离 | 减少颜色级别 |
| 去色 | 移除颜色 |

## 图层系统

### 图层操作

| 操作 | 菜单路径 | 说明 |
|------|---------|------|
| 新建图层 | Layer > New Layer | 创建空图层 |
| 复制图层 | Layer > Duplicate Layer | 复制图层 |
| 向下合并 | Layer > Merge Down | 与下方图层合并 |
| 拼合 | Image > Flatten Image | 合并所有图层 |
| 分组 | Layer > New Layer Group | 组织图层 |
| 蒙版 | Layer > Mask > Add Layer Mask | 添加透明蒙版 |

### 图层混合模式

| 模式 | 效果 | 用途 |
|------|------|------|
| 正常 | 标准叠加 | 默认模式 |
| 正片叠底 | 通过乘法变暗 | 阴影 |
| 滤色 | 通过乘法变亮 | 高光 |
| 叠加 | 对比度增强 | 一般调整 |
| 柔光 | 柔和光照效果 | 微妙调整 |
| 强光 | 强烈光照效果 | 戏剧效果 |
| 差值 | 颜色反转效果 | 特殊效果 |
| 相加 | 通过加法变亮 | 光效 |

### 图层属性

| 属性 | 说明 |
|------|------|
| 不透明度 | 图层透明度（0-100%） |
| 可见性 | 显示或隐藏图层 |
| 锁定 | 防止编辑 |
| 模式 | 混合模式选择 |
| 名称 | 图层标识符 |

## 选区操作

| 操作 | 快捷键 | 说明 |
|------|--------|------|
| 全选 | Ctrl+A | 选择整个图像 |
| 取消选择 | Ctrl+Shift+A | 取消选区 |
| 反选 | Ctrl+I | 反转选区 |
| 扩展 | Select > Grow | 扩展选区 |
| 收缩 | Select > Shrink | 收缩选区 |
| 羽化 | Select > Feather | 柔化边缘 |
| 保存 | Select > Save to Channel | 存储选区 |
| 转为路径 | Select > To Path | 转换为矢量路径 |

## 图像调整

### 色彩校正工作流

| 步骤 | 工具 | 用途 |
|------|------|------|
| 1 | 色阶 | 设置黑白点 |
| 2 | 曲线 | 微调色调范围 |
| 3 | 色彩平衡 | 校正色偏 |
| 4 | 色相-饱和度 | 调整鲜艳度 |
| 5 | 锐化 | 增强细节 |

### 色阶工具

| 控制 | 效果 |
|------|------|
| 黑点 | 设置最暗值 |
| 白点 | 设置最亮值 |
| 中间调 | 调整 gamma |
| 输出 | 限制色调范围 |

### 曲线工具

| 调整 | 曲线形状 | 效果 |
|------|---------|------|
| 变亮 | 提高中间调 | 更亮的图像 |
| 变暗 | 降低中间调 | 更暗的图像 |
| 增加对比度 | S 曲线 | 更大动态范围 |
| 降低对比度 | 反 S 曲线 | 更平坦的图像 |

## 滤镜

### 常用滤镜

| 滤镜 | 菜单路径 | 用途 |
|------|---------|------|
| 高斯模糊 | Filters > Blur | 平滑模糊效果 |
| USM 锐化 | Filters > Enhance | 锐化细节 |
| 噪点 | Filters > Noise | 添加或移除噪点 |
| 浮雕 | Filters > Distorts | 3D 浮雕效果 |
| 投影 | Filters > Light and Shadow | 添加阴影 |
| 暗角 | Filters > Light and Shadow | 边缘变暗 |
| 霓虹光 | Filters > Light and Shadow | 发光边缘 |
| 卡通 | Filters > Artistic | 卡通效果 |

### 滤镜分类

| 分类 | 示例 |
|------|------|
| 模糊 | 高斯、动感、像素化 |
| 增强 | 锐化、USM、去隔行 |
| 扭曲 | 波纹、旋转、镜头畸变 |
| 光影 | 镜头光晕、渐变光晕、闪光 |
| 噪点 | HSV 噪点、拾取、涂抹 |
| 边缘检测 | Sobel、Laplace、梯度 |
| 艺术 | 油画化、卡通、立体主义 |
| 映射 | 凹凸映射、扭曲、分形追踪 |

## 文件格式

| 格式 | 扩展名 | 最佳场景 |
|------|--------|---------|
| XCF | .xcf | GIMP 项目（保留图层） |
| PNG | .png | Web 图形、透明度 |
| JPEG | .jpg | 照片、Web 图片 |
| TIFF | .tif | 打印、高质量 |
| WebP | .webp | Web 优化 |
| GIF | .gif | 动画、简单图形 |
| BMP | .bmp | 未压缩位图 |
| PSD | .psd | Photoshop 兼容 |
| SVG | .svg | 矢量图形导出 |

## 快捷键

### 基础快捷键

| 操作 | Windows/Linux | macOS |
|------|--------------|-------|
| 撤销 | Ctrl+Z | Cmd+Z |
| 重做 | Ctrl+Shift+Z | Cmd+Shift+Z |
| 复制 | Ctrl+C | Cmd+C |
| 粘贴 | Ctrl+V | Cmd+V |
| 剪切 | Ctrl+X | Cmd+X |
| 保存 | Ctrl+S | Cmd+S |
| 导出 | Ctrl+Shift+E | Cmd+Shift+E |
| 放大 | + | + |
| 缩小 | - | - |
| 适合窗口 | Ctrl+Shift+J | Cmd+Shift+J |
| 新建图层 | Ctrl+Shift+N | Cmd+Shift+N |
| 拼合 | Ctrl+Shift+F | Cmd+Shift+F |

## 批处理

### Script-Fu 控制台

```scheme
; 批量调整图片大小
(let* (
  (filelist (cadr (file-glob "*.jpg" 1)))
)
  (while (not (null? filelist))
    (let* (
      (filename (car filelist))
      (image (car (gimp-file-load RUN-NONINTERACTIVE filename filename)))
    )
      (gimp-image-scale image 800 600)
      (file-png-save RUN-NONINTERACTIVE image (car (gimp-image-get-active-drawable image))
        filename filename 0 9 1 1 1 1 1)
      (gimp-image-delete image)
    )
    (set! filelist (cdr filelist))
  )
)
```

### Python-Fu 脚本

```python
#!/usr/bin/env python
from gimpfu import *
import glob

def batch_resize(input_dir, output_dir, width, height):
    for filepath in glob.glob(input_dir + "/*.jpg"):
        image = pdb.gimp_file_load(filepath, filepath)
        pdb.gimp_image_scale(image, width, height)
        drawable = pdb.gimp_image_get_active_drawable(image)
        output = output_dir + "/" + filepath.split("/")[-1]
        pdb.file_jpeg_save(image, drawable, output, output, 0.9, 0, 1, 1, "", 0, 1, 0, 2)
        pdb.gimp_image_delete(image)
```

## 照片编辑技巧

| 任务 | 推荐方法 |
|------|---------|
| 移除背景 | 使用前景选择或路径工具 |
| 皮肤修图 | 使用软刷修复工具 |
| 移除对象 | 使用克隆图章采样区域 |
| 色彩校正 | 先色阶后曲线 |
| 锐化 | USM 锐化（数量：0.5，半径：1.0） |
| 降噪 | Filters > Enhance > Selective Gaussian Blur |
| 调整大小 | Image > Scale Image（使用三次插值） |
| 裁剪 | 使用固定宽高比的裁剪工具 |

## 性能优化

| 设置 | 位置 | 影响 |
|------|------|------|
| 磁贴缓存 | Edit > Preferences > System Resources | 撤销用内存 |
| 处理器数量 | Edit > Preferences > System Resources | 并行处理 |
| 交换目录 | Edit > Preferences > System Resources | 磁盘溢出 |
| 撤销级别 | Edit > Preferences > System Resources | 内存使用 |

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 性能缓慢 | 大图 + 低内存 | 增加磁贴缓存大小 |
| 工具不工作 | 选错图层 | 检查活动图层 |
| 无法保存格式 | 仅 XCF 用于项目 | 使用 Export 导出其他格式 |
| 颜色不正确 | 色彩配置文件不匹配 | 检查图像色彩配置文件 |
| 插件未找到 | 未安装 | 检查 Filters 菜单 |

## 总结

GIMP 提供了全面的图像编辑解决方案，具有专业级的照片修图、平面设计和图像处理工具。其图层系统、滤镜库和脚本能力使其适合简单编辑和复杂合成。


---

## 来源：imageLib.md

## 简介

OpenImageIO (OIIO) 是一个开源库，用于读取、写入和处理视觉特效与动画中常用的图像文件。它提供了统一的接口来处理数十种图像格式，并附带一套图像处理工具。

OIIO 在专业视觉特效管线中被广泛用作标准图像 I/O 层，在所有应用中提供一致的行为。

## 为什么 OIIO 很重要

专业的视觉特效工作涉及许多图像格式、色彩空间和元数据标准。OIIO 提供了一个单一、可靠的库来一致地处理所有这些。

| 挑战 | OIIO 解决方案 |
|------|-------------|
| 多种图像格式 | 统一的读写 API |
| 色彩管理 | 集成 OCIO 支持 |
| 元数据处理 | 标准化属性访问 |
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

### 从源码编译

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

# 逐行读取
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

# 将整个图像读取为 numpy 数组
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

# 缩放
src = oiio.ImageBuf("input.exr")
dst = oiio.ImageBuf()
oiio.ImageBufAlgo.resize(dst, src, roi=oiio.ROI(0, 960, 0, 540))

# 使用 OCIO 进行色彩转换
result = oiio.ImageBuf()
oiio.ImageBufAlgo.colorconvert(result, dst, "acescg", "srgb_display")

# 合并两张图像
added = oiio.ImageBuf()
oiio.ImageBufAlgo.add(added, src, dst)

# 合成（over 操作）
comp = oiio.ImageBuf()
oiio.ImageBufAlgo.over(comp, fg, bg)
```

## 命令行工具

### oiiotool

oiiotool 是一个多功能的命令行图像处理工具。

| 操作 | 命令 |
|------|------|
| 获取信息 | `oiiotool --info image.exr` |
| 缩放 | `oiiotool input.exr --resize 1920x1080 -o output.exr` |
| 转换格式 | `oiiotool input.exr -d uint8 -o output.png` |
| 色彩转换 | `oiiotool --colorconfig ocio.ocio input.exr --colorconvert acescg srgb -o out.exr` |
| 合并图像 | `oiiotool a.exr b.exr --add -o sum.exr` |
| 合并图层 | `oiiotool layered.exr --flatten -o flat.exr` |
| 裁剪 | `oiiotool input.exr --crop 100x100+50+50 -o cropped.exr` |

### oiiotool 管线

```bash
# 缩放、色彩转换并添加水印
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

OIIO 支持大图像的两种主要访问模式。

| 模式 | 最适合 | 内存使用 |
|------|-------|---------|
| 扫描线 | 顺序处理 | 低 |
| 分块 | 随机访问 | 中等 |
| ImageBuf（完整） | 小图像或内存充足时 | 高 |

### 分块图像访问

```python
import OpenImageIO as oiio

# 以分块方式打开
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

深度图像存储每个像素的可变数量的采样，用于体积渲染和合成。

| 特性 | 扫描线图像 | 深度图像 |
|------|----------|---------|
| 每像素采样数 | 固定（1） | 可变 |
| 存储 | 规则网格 | 按像素列表 |
| 使用场景 | 标准渲染 | 体积渲染、深度合成 |
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

视觉特效图像通常包含超出标准 RGBA 的多个通道。

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
|------|---------|
| Blender | 图像 I/O 后端 |
| Nuke | 可选图像格式支持 |
| Gaffer | 主要图像处理 |
| MaterialX | 纹理处理 |
| USD | 纹理资源处理 |
| OpenShadingLanguage | 纹理查找 |

## 性能优化技巧

| 技巧 | 实现方式 |
|------|---------|
| 使用分块 EXR | 将分块大小设为 64x64 或 128x128 |
| 多线程 | OIIO 自动检测核心数；设置 OIIO_THREADS |
| 流式扫描线 | 避免加载整个大图像 |
| 压缩 I/O | EXR 使用 ZIP 或 PIZ 压缩 |
| 内存映射 | 对大文件的只读访问启用 |
| 避免复制 | 使用基于 ROI 的操作代替完整复制 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方文档 | openimageio.org |
| GitHub 仓库 | github.com/AcademySoftwareFoundation/oiio |
| Python API 参考 | openimageio.org/python |
| 邮件列表 | groups.google.com/g/openimageio |


---

## 来源：imageIo.md

## 简介

OpenImageIO (OIIO) 是一组库和命令行工具，用于读取、写入和处理视觉特效与动画相关的任何格式的图像文件。它是电影和视觉特效行业使用的标准图像 I/O 层。

OIIO 在统一的 API 背后抽象了格式差异，使应用无需格式特定代码即可处理任何支持的图像格式。

## 架构概述

OIIO 基于插件架构构建。每种图像格式由一个实现标准接口的独立插件处理。

| 组件 | 用途 | 描述 |
|------|------|------|
| ImageInput | 读取 | 格式特定的读取实现 |
| ImageOutput | 写入 | 格式特定的写入实现 |
| ImageBuf | 缓冲 | 内存中的图像表示 |
| ImageCache | 缓存 | 基于分块的纹理缓存 |
| TextureSystem | 纹理 | Mipmap 纹理查找 |
| ImageSpec | 元数据 | 图像属性描述 |
| ImageBufAlgo | 处理 | 图像处理操作 |

## 支持的图像格式

| 格式 | 扩展名 | 读取 | 写入 | 备注 |
|------|--------|------|------|------|
| OpenEXR | .exr | 是 | 是 | HDR、深度、分块、多部分 |
| TIFF | .tif, .tiff | 是 | 是 | 多页、多种位深度 |
| PNG | .png | 是 | 是 | Web 标准 |
| JPEG | .jpg, .jpeg | 是 | 是 | 有损压缩 |
| BMP | .bmp | 是 | 是 | Windows 位图 |
| TGA | .tga | 是 | 是 | Targa |
| PSD | .psd | 是 | 否 | Photoshop |
| FITS | .fits | 是 | 是 | 天文学 |
| DICOM | .dcm | 是 | 否 | 医学 |
| RLA | .rla | 是 | 否 | Wavefront |
| SGI | .sgi, .rgb | 是 | 是 | Silicon Graphics |
| WebP | .webp | 是 | 是 | Web 格式 |
| HEIF/HEIC | .heif, .heic | 是 | 否 | Apple/现代 |
| JPEG 2000 | .jp2 | 是 | 是 | 小波压缩 |
| Cineon | .cin | 是 | 是 | 胶片扫描 |

## 安装

### 从源码编译

```bash
git clone https://github.com/AcademySoftwareFoundation/oiio.git
cd oiio
mkdir build && cd build
cmake .. \
  -DCMAKE_INSTALL_PREFIX=/usr/local \
  -DUSE_PYTHON=ON \
  -DUSE_OPENGL=ON \
  -DUSE_QT=ON
make -j$(nproc)
sudo make install
```

### 依赖

| 依赖 | 必需 | 用途 |
|------|------|------|
| OpenEXR | 是 | EXR 格式支持 |
| libtiff | 是 | TIFF 格式支持 |
| libpng | 是 | PNG 格式支持 |
| libjpeg | 是 | JPEG 格式支持 |
| Boost | 是 | 各种工具 |
| Python | 可选 | Python 绑定 |
| OpenGL | 可选 | GPU 显示 |
| Qt | 可选 | GUI 工具 |
| OpenCV | 可选 | 计算机视觉 |
| FFmpeg | 可选 | 视频文件支持 |
| OpenColorIO | 可选 | 色彩管理 |

### 包管理器安装

| 平台 | 命令 |
|------|------|
| macOS (Homebrew) | `brew install openimageio` |
| Ubuntu 22.04 | `sudo apt install openimageio-tools libopenimageio-dev` |
| Fedora | `sudo dnf install OpenImageIO` |
| Conda | `conda install -c conda-forge openimageio` |
| vcpkg | `vcpkg install openimageio` |

## 核心类

### ImageSpec

ImageSpec 描述图像的结构和元数据。

```python
import OpenImageIO as oiio

spec = oiio.ImageSpec(1920, 1080, 4, oiio.FLOAT)
spec.tile_width = 64
spec.tile_height = 64
spec["compression"] = "zip"
spec["ImageDescription"] = "Beauty pass"

print(f"Width: {spec.width}")
print(f"Height: {spec.height}")
print(f"Channels: {spec.nchannels}")
print(f"Data type: {spec.format}")
print(f"Tile size: {spec.tile_width}x{spec.tile_height}")
```

### ImageBuf

ImageBuf 在内存中保存图像及相关元数据。

```python
import OpenImageIO as oiio

# 从文件读取
buf = oiio.ImageBuf("render.exr")

# 从 spec 创建
spec = oiio.ImageSpec(512, 512, 3, oiio.FLOAT)
buf = oiio.ImageBuf(spec)

# 填充颜色
oiio.ImageBufAlgo.fill(buf, (0.5, 0.3, 0.8))

# 获取像素值
pixel = buf.getpixel(256, 256)
print(f"Pixel at (256,256): {pixel}")

# 写入文件
buf.write("output.exr")
```

## 图像处理操作

OIIO 通过 ImageBufAlgo 提供全面的图像处理操作。

### 色彩操作

| 操作 | 函数 | 描述 |
|------|------|------|
| 色彩转换 | `colorconvert()` | 在色彩空间间变换 |
| 通道复制 | `channels()` | 重排或提取通道 |
| 钳位 | `clamp()` | 限制像素值 |
| 预乘 | `premult()` | 应用 alpha 预乘 |
| 反预乘 | `unpremult()` | 反转预乘 |
| 色彩平衡 | `colorbalance()` | 调整阴影/中间调/高光 |
| 饱和度 | `saturate()` | 调整色彩饱和度 |

### 几何操作

| 操作 | 函数 | 描述 |
|------|------|------|
| 缩放 | `resize()` | 缩放图像尺寸 |
| 重采样 | `resample()` | 快速最近邻缩放 |
| 旋转 | `rotate()` | 按角度旋转 |
| 垂直翻转 | `flip()` | 垂直镜像 |
| 水平翻转 | `flop()` | 水平镜像 |
| 转置 | `transpose()` | 交换轴 |
| 变形 | `warp()` | 任意 2D 变换 |
| 裁剪 | `cut()` | 提取矩形区域 |

### 算术操作

| 操作 | 函数 | 描述 |
|------|------|------|
| 加法 | `add()` | 图像相加或加常数 |
| 减法 | `sub()` | 图像相减或减常数 |
| 乘法 | `mul()` | 图像相乘或乘常数 |
| 除法 | `div()` | 图像相除或除常数 |
| 差值 | `diff()` | 绝对像素差 |
| 最小值 | `min()` | 逐像素最小值 |
| 最大值 | `max()` | 逐像素最大值 |

### 滤镜和增强

| 操作 | 函数 | 描述 |
|------|------|------|
| 模糊 | `blur()` | 高斯模糊 |
| 中值 | `median_filter()` | 降噪 |
| 反锐化掩模 | `unsharp_mask()` | 锐化 |
| 卷积 | `convolve()` | 自定义卷积核 |
| 膨胀 | `dilate()` | 形态学膨胀 |
| 腐蚀 | `erode()` | 形态学腐蚀 |

### 合成操作

| 操作 | 函数 | 描述 |
|------|------|------|
| Over | `over()` | Porter-Duff over |
| Atop | `atop()` | Porter-Duff atop |
| In | `in()` | Porter-Duff in |
| Out | `out()` | Porter-Duff out |
| Z 合成 | `zover()` | 基于深度的合成 |

## 纹理系统

TextureSystem 为渲染提供优化的 mipmap 纹理访问。

| 特性 | 描述 |
|------|------|
| Mipmap | 自动细节层次选择 |
| 滤波 | EWA 各向异性滤波 |
| 缓存 | 基于分块的 LRU 缓存 |
| UDIM | 多分块 UV 支持 |
| 每通道 | 独立通道查找 |

## 命令行工具参考

### oiiotool

最通用的图像处理命令行工具。

```bash
# 图像信息
oiiotool --info -v image.exr

# 格式转换
oiiotool input.exr -d uint8 -o output.png

# 缩放
oiiotool input.exr --resize:filter=lanczos3 1920x1080 -o output.exr

# 色彩操作
oiiotool input.exr --colorconvert:from=acescg:to=srgb -o output.exr

# 合成
oiiotool fg.exr bg.exr --over -o comp.exr

# 文本标注
oiiotool input.exr --text:x=50:y=50:color=1,1,1 "Shot 010" -o output.exr

# 通道操作
oiiotool input.exr --ch R,G,B -o rgb.exr
```

### iinfo

显示图像元数据而不加载像素数据。

```bash
iinfo -v image.exr
iinfo --hash image.exr
iinfo -d image.exr  # 数据类型信息
```

### idiff

定量比较两张图像。

```bash
idiff a.exr b.exr
idiff --fail 0.01 a.exr b.exr
idiff --absdiff --output diff.exr a.exr b.exr
```

### maketx

创建分块、mipmap 纹理文件。

```bash
maketx input.exr -o texture.tx
maketx --oiio --filter lanczos3 input.exr -o texture.tx
maketx --udim input_####.exr -o texture.tx
```

## 集成示例

| 工具 | OIIO 用途 |
|------|---------|
| Blender | 图像 I/O 后端 |
| Nuke | 可选图像格式支持 |
| Gaffer | 主要图像处理 |
| MaterialX | 纹理处理 |
| USD | 纹理资源处理 |

## 性能优化

| 优化 | 技术 | 影响 |
|------|------|------|
| 分块 I/O | 使用分块 EXR 进行随机访问 | 高 |
| 图像缓存 | 对纹理密集场景启用 | 高 |
| 扫描线流式 | 大图像逐行处理 | 中 |
| 数据类型匹配 | 避免不必要的类型转换 | 中 |
| 压缩选择 | 存储用 ZIP，临时文件用 NONE | 中 |
| 多线程 | OIIO 自动检测核心数 | 高 |

## 更多资源

| 资源 | URL |
|------|-----|
| 文档 | openimageio.org |
| API 参考 | openimageio.org/python |
| GitHub | github.com/AcademySoftwareFoundation/oiio |
| 教程 | openimageio.org/tutorials |


---

## 来源：oiio.md

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


---

## 来源：ocio.md

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


---

## 来源：hdr.md

## 简介

OpenEXR 是视觉特效和电影制作领域的行业标准高动态范围 (HDR) 图像文件格式。由 Industrial Light & Magic (ILM) 开发，现由 Academy Software Foundation 维护，OpenEXR 是专业视觉特效管线中存储渲染帧、合成元素和纹理贴图的主要格式。

## 为什么选择 OpenEXR？

标准图像格式如 JPEG 和 PNG 使用 8 位整数值，限制了它们能表示的颜色和亮度范围。OpenEXR 支持浮点数据，可以捕捉场景中的完整光线范围。

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

| 类型 | 位数 | 范围 | 使用场景 |
|------|------|------|---------|
| HALF | 16 | -65504 到 65504 | 色彩数据，节省存储 |
| FLOAT | 32 | 完全精度 | 深度、速度、合成 |
| UINT | 32 | 0 到 40 亿 | ID、标签 |

## 压缩方法

OpenEXR 提供多种针对不同内容类型优化的压缩算法。

| 方法 | 压缩比 | 速度 | 最适合 |
|------|-------|------|-------|
| NONE | 1:1 | 最快 | 调试、临时文件 |
| RLE | ~2:1 | 快 | 简单图像、遮罩 |
| ZIP（单行） | ~3:1 | 中等 | 扫描线图像 |
| ZIP（多行） | ~3.5:1 | 中等 | 扫描线图像 |
| PIZ | ~2.5:1 | 中等 | 噪点多的渲染 |
| PXR24 | ~3:1 | 快 | CG 渲染（有损 half） |
| B44 | ~4:1 | 快 | 预览、背景 |
| DWAA | ~10:1 | 慢 | 有损，感知质量 |
| DWAB | ~20:1 | 慢 | 重度有损压缩 |

### 选择压缩方式

| 使用场景 | 推荐压缩 | 原因 |
|---------|---------|------|
| 最终渲染 | ZIP 多行 | 好的压缩比，无损 |
| 合成元素 | ZIP 多行 | 需要无损 |
| 纹理 | PIZ 或 ZIP | 适合噪点数据 |
| 预览/审阅 | DWAA | 小文件可接受 |
| 深度图像 | ZIP 或 PIZ | 深度数据兼容性 |
| 归档 | ZIP 多行 | 最佳无损压缩比 |

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

// 读取 half-float RGBA 图像
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
|------|-------|------|
| 访问模式 | 顺序行 | 随机分块访问 |
| Mipmap | 否 | 是 |
| 内存使用 | 流式时低 | 中等 |
| 最适合 | 全帧合成 | 纹理流式加载 |

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

深度图像存储每个像素的可变数量采样，对体积渲染至关重要。

| 方面 | 平面图像 | 深度图像 |
|------|---------|---------|
| 每像素采样数 | 1 | 可变 |
| 存储 | 固定网格 | 按像素数组 |
| 合成 | 标准 over | 深度感知 |
| 文件大小 | 可预测 | 取决于内容 |

```python
import OpenEXR
import numpy as np

# 深度图像数据：每个像素的采样列表
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

| 使用场景 | 部分内容 | 优势 |
|---------|---------|------|
| 多视角 | 左眼、右眼 | 立体合成 |
| 多图层 | 美术、漫反射、高光 | 灵活合成 |
| 多帧 | 帧 1、帧 2... | 单文件序列 |

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
| capDate | string | 拍摄日期/时间 |
| focus | float | 摄像机焦距 |
| expTime | float | 曝光时间 |
| aperture | float | 镜头光圈 |
| isoSpeed | float | ISO 感光度 |
| timeCode | Timecode | SMPTE 时间码 |

## 最佳实践

### 存储与性能

| 实践 | 建议 |
|------|------|
| 压缩 | 最终帧使用 ZIP 多行 |
| 分块大小 | 纹理用 64x64，帧用 256x256 |
| 通道精度 | 色彩用 HALF，深度/速度用 FLOAT |
| 数据窗口 | 裁剪到活动区域以节省空间 |
| 命名 | 使用 show_shot_version_frame.ext 约定 |

### 管线考量

| 考量 | 指导 |
|------|------|
| 色彩管理 | 存储场景参考线性数据 |
| 元数据 | 包含摄像机、镜头、帧信息 |
| 深度图像 | 用于体积渲染和运动模糊 |
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
| exrmultipart | 合并/拆分多部分 | `exrmultipart -combine parts.exr out.exr` |

## 更多资源

| 资源 | URL |
|------|-----|
| OpenEXR 网站 | openexr.com |
| GitHub 仓库 | github.com/AcademySoftwareFoundation/openexr |
| 技术介绍 | openexr.com/documentation |
| ILM OpenEXR 指南 | openexr.com/docs |


---

## 来源：openexr.md

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


---

## 来源：openimageio.md

## 简介

OpenImageIO (OIIO) 是一个库和命令行工具集，用于读取、写入和处理与 VFX 和动画相关的任何格式的图像文件。它是电影和视觉效果行业使用的标准图像 I/O 层。

OIIO 将格式差异抽象到一致的 API 背后，使应用程序能够处理任何支持的图像格式而无需格式特定的代码。

## 架构概览

OIIO 建立在插件架构之上。每种图像格式由实现标准接口的单独插件处理。

| 组件 | 用途 | 描述 |
|------|------|------|
| ImageInput | 读取 | 格式特定的读取实现 |
| ImageOutput | 写入 | 格式特定的写入实现 |
| ImageBuf | 缓冲 | 内存中的图像表示 |
| ImageCache | 缓存 | 基于图块的纹理缓存 |
| TextureSystem | 纹理 | Mip-mapped 纹理查找 |
| ImageSpec | 元数据 | 图像属性描述 |
| ImageBufAlgo | 处理 | 图像处理操作 |

## 支持的图像格式

| 格式 | 扩展名 | 读取 | 写入 | 备注 |
|------|--------|------|------|------|
| OpenEXR | .exr | 是 | 是 | HDR、深度、分块、多部分 |
| TIFF | .tif, .tiff | 是 | 是 | 多页、多种位深 |
| PNG | .png | 是 | 是 | Web 标准 |
| JPEG | .jpg, .jpeg | 是 | 是 | 有损压缩 |
| BMP | .bmp | 是 | 是 | Windows 位图 |
| TGA | .tga | 是 | 是 | Targa |
| PSD | .psd | 是 | 否 | Photoshop |
| FITS | .fits | 是 | 是 | 天文学 |
| DICOM | .dcm | 是 | 否 | 医学 |
| RLA | .rla | 是 | 否 | Wavefront |
| SGI | .sgi, .rgb | 是 | 是 | Silicon Graphics |
| WebP | .webp | 是 | 是 | Web 格式 |
| HEIF/HEIC | .heif, .heic | 是 | 否 | Apple/现代 |
| JPEG 2000 | .jp2 | 是 | 是 | 小波压缩 |
| Cineon | .cin | 是 | 是 | 胶片扫描 |

## 安装

### 从源码构建

```bash
git clone https://github.com/AcademySoftwareFoundation/oiio.git
cd oiio
mkdir build && cd build
cmake .. \
  -DCMAKE_INSTALL_PREFIX=/usr/local \
  -DUSE_PYTHON=ON \
  -DUSE_OPENGL=ON \
  -DUSE_QT=ON
make -j$(nproc)
sudo make install
```

### 依赖项

| 依赖 | 必需 | 用途 |
|------|------|------|
| OpenEXR | 是 | EXR 格式支持 |
| libtiff | 是 | TIFF 格式支持 |
| libpng | 是 | PNG 格式支持 |
| libjpeg | 是 | JPEG 格式支持 |
| Boost | 是 | 各种工具 |
| Python | 可选 | Python 绑定 |
| OpenGL | 可选 | GPU 显示 |
| Qt | 可选 | GUI 工具 |
| OpenCV | 可选 | 计算机视觉 |
| FFmpeg | 可选 | 视频文件支持 |
| OpenColorIO | 可选 | 色彩管理 |

### 包管理器安装

| 平台 | 命令 |
|------|------|
| macOS (Homebrew) | `brew install openimageio` |
| Ubuntu 22.04 | `sudo apt install openimageio-tools libopenimageio-dev` |
| Fedora | `sudo dnf install OpenImageIO` |
| Conda | `conda install -c conda-forge openimageio` |
| vcpkg | `vcpkg install openimageio` |

## 核心类

### ImageSpec

ImageSpec 描述图像的结构和元数据。

```python
import OpenImageIO as oiio

spec = oiio.ImageSpec(1920, 1080, 4, oiio.FLOAT)
spec.tile_width = 64
spec.tile_height = 64
spec["compression"] = "zip"
spec["ImageDescription"] = "Beauty pass"

print(f"Width: {spec.width}")
print(f"Height: {spec.height}")
print(f"Channels: {spec.nchannels}")
print(f"Data type: {spec.format}")
print(f"Tile size: {spec.tile_width}x{spec.tile_height}")
```

### ImageBuf

ImageBuf 在内存中保存图像及其关联的元数据。

```python
import OpenImageIO as oiio

# 从文件读取
buf = oiio.ImageBuf("render.exr")

# 从 spec 创建
spec = oiio.ImageSpec(512, 512, 3, oiio.FLOAT)
buf = oiio.ImageBuf(spec)

# 填充颜色
oiio.ImageBufAlgo.fill(buf, (0.5, 0.3, 0.8))

# 获取像素值
pixel = buf.getpixel(256, 256)
print(f"Pixel at (256,256): {pixel}")

# 写入文件
buf.write("output.exr")
```

## 图像处理操作

OIIO 通过 ImageBufAlgo 提供了一套全面的图像处理操作。

### 颜色操作

| 操作 | 函数 | 描述 |
|------|------|------|
| 颜色转换 | `colorconvert()` | 在色彩空间之间转换 |
| 通道复制 | `channels()` | 重新排序或提取通道 |
| 钳制 | `clamp()` | 限制像素值 |
| 预乘 | `premult()` | 应用 alpha 预乘 |
| 反预乘 | `unpremult()` | 反转预乘 |
| 色彩平衡 | `colorbalance()` | 调整阴影/中间调/高光 |
| 饱和度 | `saturate()` | 调整颜色饱和度 |

### 几何操作

| 操作 | 函数 | 描述 |
|------|------|------|
| 调整大小 | `resize()` | 缩放图像尺寸 |
| 重采样 | `resample()` | 快速最近邻缩放 |
| 旋转 | `rotate()` | 按角度旋转 |
| 垂直翻转 | `flip()` | 垂直镜像 |
| 水平翻转 | `flop()` | 水平镜像 |
| 转置 | `transpose()` | 交换轴 |
| 扭曲 | `warp()` | 任意 2D 变换 |
| 裁剪 | `cut()` | 提取矩形区域 |

### 算术操作

| 操作 | 函数 | 描述 |
|------|------|------|
| 加法 | `add()` | 图像相加或加常数 |
| 减法 | `sub()` | 图像相减或减常数 |
| 乘法 | `mul()` | 图像相乘或乘常数 |
| 除法 | `div()` | 图像相除或除常数 |
| 差异 | `diff()` | 绝对像素差异 |
| 最小值 | `min()` | 逐像素最小值 |
| 最大值 | `max()` | 逐像素最大值 |

### 滤镜和增强

| 操作 | 函数 | 描述 |
|------|------|------|
| 模糊 | `blur()` | 高斯模糊 |
| 中值 | `median_filter()` | 降噪 |
| USM 锐化 | `unsharp_mask()` | 锐化 |
| 卷积 | `convolve()` | 自定义卷积核 |
| 膨胀 | `dilate()` | 形态学膨胀 |
| 腐蚀 | `erode()` | 形态学腐蚀 |

### 合成操作

| 操作 | 函数 | 描述 |
|------|------|------|
| Over | `over()` | Porter-Duff over |
| Atop | `atop()` | Porter-Duff atop |
| In | `in()` | Porter-Duff in |
| Out | `out()` | Porter-Duff out |
| Z 合成 | `zover()` | 基于深度的合成 |

## 纹理系统

TextureSystem 为渲染提供优化的 mip-mapped 纹理访问。

| 功能 | 描述 |
|------|------|
| Mip-mapping | 自动细节级别选择 |
| 过滤 | EWA 各向异性过滤 |
| 缓存 | 基于图块的 LRU 缓存 |
| UDIM | 多图块 UV 支持 |
| 每通道 | 独立通道查找 |

## 命令行工具参考

### oiiotool

最通用的图像处理命令行工具。

```bash
# 图像信息
oiiotool --info -v image.exr

# 格式转换
oiiotool input.exr -d uint8 -o output.png

# 调整大小
oiiotool input.exr --resize:filter=lanczos3 1920x1080 -o output.exr

# 颜色操作
oiiotool input.exr --colorconvert:from=acescg:to=srgb -o output.exr

# 合成
oiiotool fg.exr bg.exr --over -o comp.exr

# 文本标注
oiiotool input.exr --text:x=50:y=50:color=1,1,1 "Shot 010" -o output.exr

# 通道操作
oiiotool input.exr --ch R,G,B -o rgb.exr
```

### iinfo

显示图像元数据而不加载像素数据。

```bash
iinfo -v image.exr
iinfo --hash image.exr
iinfo -d image.exr  # 数据类型信息
```

### idiff

定量比较两幅图像。

```bash
idiff a.exr b.exr
idiff --fail 0.01 a.exr b.exr
idiff --absdiff --output diff.exr a.exr b.exr
```

### maketx

创建分块、mip-mapped 的纹理文件。

```bash
maketx input.exr -o texture.tx
maketx --oiio --filter lanczos3 input.exr -o texture.tx
maketx --udim input_####.exr -o texture.tx
```

## 集成示例

| 工具 | OIIO 用途 |
|------|-----------|
| Blender | 图像 I/O 后端 |
| Nuke | 可选图像格式支持 |
| Gaffer | 主要图像处理 |
| MaterialX | 纹理处理 |
| USD | 纹理资产处理 |

## 性能优化

| 优化 | 技术 | 影响 |
|------|------|------|
| 分块 I/O | 使用分块 EXR 进行随机访问 | 高 |
| 图像缓存 | 对纹理密集场景启用 | 高 |
| 扫描线流式处理 | 对大图像逐行处理 | 中 |
| 数据类型匹配 | 避免不必要的类型转换 | 中 |
| 压缩选择 | ZIP 用于存储，NONE 用于临时文件 | 中 |
| 多线程 | OIIO 自动检测核心数 | 高 |

## 附加资源

| 资源 | URL |
|------|-----|
| 文档 | openimageio.org |
| API 参考 | openimageio.org/python |
| GitHub | github.com/AcademySoftwareFoundation/oiio |
| 教程 | openimageio.org/tutorials |


---

## 来源：paint.md

## 简介

Krita 是一款免费、开源的数字绘画应用程序，专为概念艺术、纹理绘制、插画和漫画设计。它为各级技能水平的艺术家提供专业级工具集。

| 属性 | 详情 |
|----------|--------|
| 仓库 | KDE/krita |
| 许可证 | GPL-3.0 |
| 语言 | C++, Python |
| 平台 | Windows, macOS, Linux |
| 文件格式 | .kra（原生）, PSD, PNG, JPEG, TIFF, OpenEXR |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install krita

# Fedora
sudo dnf install krita

# Flatpak
flatpak install org.kde.krita
```

### macOS 和 Windows

从 Krita 官方网站或 Steam 下载。

## 界面概览

| 区域 | 描述 |
|------|-------------|
| Canvas（画布） | 中央绘图区域 |
| Toolbox（工具箱） | 工具选择面板（左侧） |
| Tool Options（工具选项） | 活动工具的设置 |
| Brush Presets（画笔预设） | 快速访问画笔库 |
| Layers Panel（图层面板） | 图层管理（右侧） |
| Color Selector（颜色选择器） | 取色工具 |
| Docker Panels（停靠面板） | 可配置的实用面板 |

## 基本工具

| 工具 | 快捷键 | 用途 |
|------|----------|---------|
| Freehand Brush（手绘画笔） | B | 主要绘画工具 |
| Line Tool（线条工具） | L | 绘制直线 |
| Rectangle（矩形） | R | 绘制矩形 |
| Ellipse（椭圆） | E | 绘制椭圆 |
| Fill Tool（填充工具） | F | 填充区域 |
| Gradient（渐变） | G | 创建渐变 |
| Transform（变换） | Ctrl+T | 缩放、旋转、倾斜 |
| Crop（裁剪） | C | 裁剪画布 |
| Selection（选区） | S | 选择区域 |
| Move（移动） | M | 移动图层或选区 |
| Text（文本） | T | 添加文本 |

## 画笔

### 画笔引擎

Krita 支持多种画笔引擎，每种提供不同的功能。

| 引擎 | 描述 |
|--------|-------------|
| Pixel Brush（像素画笔） | 标准绘画画笔 |
| Color Smudge（颜色涂抹） | 绘画时混合颜色 |
| Shape Brush（形状画笔） | 使用矢量形状绘画 |
| Sketch Brush（素描画笔） | 铅笔式素描 |
| Spray Brush（喷雾画笔） | 散射粒子 |
| Hatching（影线） | 交叉影线笔触 |
| Chalk（粉笔） | 纹理粉笔效果 |
| Filter Brush（滤镜画笔） | 将滤镜作为绘画应用 |

### 画笔设置

| 设置 | 描述 |
|---------|-------------|
| Size（大小） | 画笔直径（像素） |
| Opacity（不透明度） | 笔触的透明度 |
| Flow（流量） | 每次点触的颜料量 |
| Spacing（间距） | 点触之间的距离 |
| Hardness（硬度） | 边缘柔和度 |
| Rotation（旋转） | 画笔笔尖角度 |
| Scatter（散布） | 随机化点触位置 |

### 画笔预设

Krita 包含数百个按类别组织的预配置画笔预设。

| 类别 | 示例 |
|----------|----------|
| Ink（墨水） | 钢笔、马克笔、书法 |
| Paint（颜料） | 油画、丙烯、水彩 |
| Sketch（素描） | 铅笔、炭笔、蜡笔 |
| Smudge（涂抹） | 混合器、搅拌器 |
| Effects（效果） | 粒子、纹理、图案 |

## 图层

### 图层类型

| 类型 | 描述 |
|------|-------------|
| Paint Layer（绘画图层） | 标准光栅图层 |
| Vector Layer（矢量图层） | 包含矢量形状 |
| Group Layer（组图层） | 其他图层的容器 |
| Clone Layer（克隆图层） | 另一图层的链接副本 |
| Filter Layer（滤镜图层） | 非破坏性滤镜效果 |
| Fill Layer（填充图层） | 纯色或图案填充 |
| File Layer（文件图层） | 引用外部文件 |

### 图层操作

| 操作 | 描述 |
|-----------|-------------|
| Add（添加） | 创建新图层 |
| Duplicate（复制） | 复制当前图层 |
| Merge Down（向下合并） | 与下方图层合并 |
| Flatten（展平） | 合并所有可见图层 |
| Lock（锁定） | 防止编辑 |
| Opacity（不透明度） | 调整图层透明度 |
| Blending Mode（混合模式） | 图层与下方图层的合成方式 |

### 混合模式

| 模式 | 描述 |
|------|-------------|
| Normal（正常） | 标准绘画 |
| Multiply（正片叠底） | 通过相乘颜色变暗 |
| Screen（滤色） | 通过反转和相乘变亮 |
| Overlay（叠加） | 结合正片叠底和滤色 |
| Soft Light（柔光） | 轻柔变亮或变暗 |
| Hard Light（强光） | 强烈变亮或变暗 |
| Color Dodge（颜色减淡） | 基于混合颜色提亮 |
| Color Burn（颜色加深） | 基于混合颜色加深 |
| Darken（变暗） | 保留两种颜色中较暗的 |
| Lighten（变亮） | 保留两种颜色中较亮的 |

## 选区

| 选区模式 | 描述 |
|----------------|-------------|
| Replace（替换） | 替换当前选区 |
| Add（添加） | 添加到当前选区 |
| Subtract（减去） | 从当前选区中移除 |
| Intersect（相交） | 仅保留重叠区域 |

### 选区工具

| 工具 | 描述 |
|------|-------------|
| Rectangular（矩形） | 选择矩形区域 |
| Elliptical（椭圆） | 选择椭圆区域 |
| Polygonal（多边形） | 用直线边缘选择 |
| Freehand（手绘） | 用手绘方式选择 |
| Contiguous（连续） | 按颜色相似性选择 |
| Similar（相似） | 选择所有匹配的颜色 |
| Bezier（贝塞尔） | 用贝塞尔曲线选择 |

## 变换工具

| 变换模式 | 描述 |
|----------------|-------------|
| Scale（缩放） | 调整选区或图层大小 |
| Rotate（旋转） | 围绕中心旋转 |
| Shear（剪切） | 倾斜选区 |
| Perspective（透视） | 应用透视变形 |
| Warp（弯曲） | 自由变形 |
| Cage（笼形） | 基于网格的变形 |
| Liquify（液化） | 推拉像素 |

## 颜色管理

| 功能 | 描述 |
|---------|-------------|
| Color Selector（颜色选择器） | 可视化选取颜色 |
| Color Sliders（颜色滑块） | 按通道调整（RGB, HSV, CMYK） |
| Color History（颜色历史） | 最近使用的颜色 |
| Palette（调色板） | 保存的颜色集 |
| Color Space（色彩空间） | 在 RGB、CMYK 或 Lab 中工作 |
| HDR Painting（HDR 绘画） | 高动态范围支持 |

## 辅助线

Krita 提供绘图辅助线，帮助处理透视、对称和其他几何约束。

| 辅助线 | 描述 |
|-----------|-------------|
| Parallel（平行） | 线条汇聚到消失点 |
| Concentric（同心） | 圆共享共同中心 |
| Vanishing Point（消失点） | 两点透视 |
| Fish Eye（鱼眼） | 弯曲透视 |
| Spline（样条） | 通过点的平滑曲线 |
| Ellipse（椭圆） | 完美的椭圆 |
| Mirror（镜像） | 跨轴对称 |

## 动画

Krita 包含逐帧动画支持。

| 功能 | 描述 |
|---------|-------------|
| Timeline（时间轴） | 帧管理的可视化时间轴 |
| Onion Skinning（洋葱皮） | 查看前后帧 |
| Playback（播放） | 实时预览动画 |
| Export（导出） | 导出为 GIF、MP4 或图像序列 |

## 滤镜

| 滤镜 | 描述 |
|--------|-------------|
| Blur（模糊） | 高斯、运动、镜头模糊 |
| Sharpen（锐化） | 增加边缘对比度 |
| Adjust Levels（调整色阶） | 修改色调范围 |
| Adjust Curves（调整曲线） | 精细色调控制 |
| HSV Adjustment（HSV 调整） | 修改色相、饱和度、明度 |
| Color Balance（色彩平衡） | 调整颜色通道 |
| Emboss（浮雕） | 创建浮雕效果 |
| Pixelize（像素化） | 创建马赛克效果 |

## 数字绘画技巧

| 技巧 | 说明 |
|-----|-------------|
| 使用图层 | 分离元素以便编辑 |
| 设置辅助线 | 使用透视辅助线提高准确性 |
| 保存画笔预设 | 保持自定义画笔有序 |
| 使用颜色管理 | 在正确的色彩空间中工作 |
| 使用参考图片 | 将参考图作为文件图层导入 |
| 学习快捷键 | 加快工作流程 |

## 结论

Krita 是一款功能丰富的数字绘画应用程序，可与商业替代品媲美。其广泛的画笔引擎、图层系统和动画支持使其适用于各种艺术工作流程。


---

## 来源：vector.md

## 简介

Inkscape 是一个专业的开源矢量图形编辑器，用于创建可缩放的插图、图表、标志和艺术作品。本教程涵盖界面、绘图工具、路径操作、文本处理和导出选项。

## 界面概览

### 主要区域

| 区域 | 位置 | 用途 |
|------|------|------|
| Menu Bar | 顶部 | 文件、编辑、视图、图层菜单 |
| Command Bar | 菜单下方 | 常用工具快速访问 |
| Tool Controls | 命令下方 | 选定工具的选项 |
| Canvas | 中央 | 主绘图区域 |
| Toolbox | 左侧 | 绘图和编辑工具 |
| Commands Bar | 右侧 | 对象操作 |
| Fill/Stroke | 底部 | 颜色和样式属性 |
| Status Bar | 底部 | 坐标、缩放、提示 |

### 画布导航

| 操作 | 方法 |
|------|------|
| 放大 | Ctrl++ 或滚轮 |
| 缩小 | Ctrl+- 或滚轮 |
| 适合窗口 | Ctrl+Shift+E |
| 平移 | 中键鼠标拖动 |
| 适合选区 | Ctrl+Shift+F |

## 基本工具

### 选择工具

| 工具 | 快捷键 | 用途 |
|------|--------|------|
| Select | S | 选择和移动对象 |
| Node Edit | N | 编辑路径节点 |
| Tweak | W | 塑形和扭曲路径 |
| Zoom | Z | 放大区域 |

### 形状工具

| 工具 | 快捷键 | 形状 |
|------|--------|------|
| Rectangle | R | 矩形、正方形 |
| Ellipse | E | 圆形、椭圆、弧线 |
| Star | * | 星形、多边形 |
| Spiral | I | 螺旋形状 |
| 3D Box | X | 透视立方体 |

### 绘图工具

| 工具 | 快捷键 | 用途 |
|------|--------|------|
| Pen | B | 点击放置路径 |
| Pencil | P | 自由手绘 |
| Calligraphy | C | 压感笔画 |
| Paint Bucket | U | 填充封闭区域 |

## 创建形状

### 矩形工具

| 修饰键 | 效果 |
|--------|------|
| 点击并拖动 | 创建矩形 |
| 按住 Ctrl | 约束为正方形 |
| 点击属性 | 设置精确尺寸 |
| 圆角 | 拖动角控制柄 |

### 椭圆工具

| 修饰键 | 效果 |
|--------|------|
| 点击并拖动 | 创建椭圆 |
| 按住 Ctrl | 约束为圆形 |
| 在弧线上拖动 | 创建弧线段 |
| 属性 | 设置起始/结束角度 |

### 星形工具

| 设置 | 选项 | 效果 |
|------|------|------|
| Corners | 3-1000 | 角数 |
| Spoke ratio | 0-1 | 内外半径比 |
| Rounded | 0-1 | 圆角 |
| Randomized | 0-1 | 不规则变化 |

## 路径操作

### 节点编辑

| 操作 | 方法 |
|------|------|
| 添加节点 | 双击路径 |
| 删除节点 | 选择后按 Delete |
| 移动节点 | 用 Node 工具拖动 |
| 转换节点类型 | 选择后使用工具栏按钮 |
| 断开路径 | 选择节点，点击 Break |

### 节点类型

| 类型 | 控制柄 | 行为 |
|------|--------|------|
| Cusp | 独立 | 尖角 |
| Smooth | 对称 | 平滑曲线 |
| Symmetric | 等长 | 对称曲线 |
| Auto-smooth | 自动 | 自动平滑 |

### 布尔运算

| 运算 | 结果 | 快捷键 |
|------|------|--------|
| Union | 合并形状 | Ctrl++ |
| Difference | 减去重叠 | Ctrl+- |
| Intersection | 仅保留重叠 | Ctrl+* |
| Exclusion | 移除重叠 | Ctrl+^ |
| Division | 按重叠分割 | Ctrl+/ |
| Cut Path | 分割路径 | Ctrl+Alt+/ |

### 路径修改

| 操作 | 描述 | 菜单 |
|------|------|------|
| Offset | 扩展/收缩路径 | Path > Outset/Inset |
| Dynamic Offset | 可调偏移 | Path > Dynamic Offset |
| Linked Offset | 参数化偏移 | Path > Linked Offset |
| Simplify | 减少节点 | Ctrl+L |
| Flatten | 曲线转直线 | Path > Flatten |

## 填充和描边

### 填充类型

| 类型 | 描述 | 用途 |
|------|------|------|
| Flat | 纯色填充 | 基本填充 |
| Linear Gradient | 双点渐变 | 平滑过渡 |
| Radial Gradient | 圆形渐变 | 聚光灯、球体 |
| Pattern | 重复图案 | 纹理 |
| No Fill | 透明 | 仅轮廓 |

### 描边属性

| 属性 | 选项 | 效果 |
|------|------|------|
| Width | 0.01-1000px | 线条粗细 |
| Line Cap | Butt, Round, Square | 端点外观 |
| Line Join | Miter, Round, Bevel | 角落外观 |
| Dashes | 各种图案 | 虚线 |
| Markers | 箭头 | 起点/终点标记 |

### 颜色管理

| 操作 | 方法 |
|------|------|
| 设置填充颜色 | 点击调色板中的颜色 |
| 设置描边颜色 | Shift+点击颜色 |
| 拾色器 | 使用 Fill/Stroke 对话框 |
| 吸管 | I 键，点击采样 |
| HSL 调整 | Fill/Stroke 对话框 |

## 文本

### 文本工具

| 操作 | 方法 |
|------|------|
| 创建文本 | 点击并输入 |
| 创建文本框 | 点击并拖动 |
| 编辑文本 | 用 Text 工具双击 |
| 选择文本 | 拖动跨过字符 |

### 文本属性

| 属性 | 选项 | 效果 |
|------|------|------|
| Font | 系统字体 | 字体选择 |
| Size | 1-10000px | 文本大小 |
| Style | Regular, Bold, Italic | 粗细和倾斜 |
| Spacing | 字母、行、词 | 字符定位 |
| Alignment | 左、中、右 | 文本对齐 |

### 路径上的文本

1. 创建文本对象
2. 创建路径
3. 选择两个对象
4. Text > Put on Path
5. 使用路径调整位置

### 形状内的文本

1. 创建形状
2. 选择形状
3. Text > Flow into Frame
4. 在形状内输入文本

## 图层

### 图层管理

| 操作 | 方法 |
|------|------|
| 添加图层 | Layer > Add Layer |
| 删除图层 | Layer > Delete Layer |
| 重命名图层 | 双击图层名称 |
| 移动图层 | 在图层面板中拖动 |
| 锁定图层 | 点击锁定图标 |
| 隐藏图层 | 点击眼睛图标 |

### 图层属性

| 属性 | 描述 |
|------|------|
| Visibility | 显示或隐藏图层 |
| Lock | 防止编辑 |
| Opacity | 图层透明度 |
| Blend mode | 图层如何混合 |

### 混合模式

| 模式 | 效果 | 用途 |
|------|------|------|
| Normal | 标准叠加 | 默认 |
| Multiply | 按图层加深 | 阴影 |
| Screen | 按图层加亮 | 高光 |
| Overlay | 对比度增强 | 效果 |
| Darken | 保留较暗像素 | 颜色叠加 |
| Lighten | 保留较亮像素 | 提亮 |

## 对齐和分布

### 对齐选项

| 选项 | 描述 | 结果 |
|------|------|------|
| Left | 左边缘对齐 | 对象左齐 |
| Center | 中心对齐 | 对象居中 |
| Right | 右边缘对齐 | 对象右齐 |
| Top | 顶边缘对齐 | 对象顶齐 |
| Middle | 垂直中心对齐 | 对象垂直居中 |
| Bottom | 底边缘对齐 | 对象底齐 |

### 分布选项

| 选项 | 描述 | 结果 |
|------|------|------|
| Horizontal | 等水平间距 | 均匀水平间距 |
| Vertical | 等垂直间距 | 均匀垂直间距 |
| Center | 分布中心 | 均匀中心间距 |
| Gap | 设置精确间距值 | 精确间距 |

## 裁剪和蒙版

### 裁剪

1. 将裁剪形状放在目标上方
2. 选择两个对象
3. Object > Clip > Set
4. 裁剪形状定义可见区域

### 蒙版

1. 将蒙版放在目标上方
2. 选择两个对象
3. Object > Mask > Set
4. 蒙版透明度定义可见性

### 区别

| 功能 | 裁剪 | 蒙版 |
|------|------|------|
| 边界 | 硬边缘 | 柔边缘 |
| 透明度 | 二值 | 渐变 |
| 可编辑 | 释放后 | 释放后 |
| 性能 | 更快 | 更慢 |

## 滤镜和效果

### 内置滤镜

| 分类 | 滤镜 | 用途 |
|------|------|------|
| Blur | Gaussian, Motion | 柔化 |
| Distort | Warp, Twirl | 形状修改 |
| Color | Channel, HSL | 颜色效果 |
| Image | Pixelate, Noise | 纹理效果 |
| Shadows | Drop Shadow | 深度效果 |

### 应用滤镜

1. 选择对象
2. Filters > Filter Name
3. 调整参数
4. 应用

## 导出选项

### 导出格式

| 格式 | 类型 | 使用场景 |
|------|------|----------|
| SVG | 矢量 | Web、进一步编辑 |
| PNG | 光栅 | Web、文档 |
| PDF | 矢量 | 打印 |
| EPS | 矢量 | 专业印刷 |
| DXF | CAD | CAD 应用 |
| PS | 矢量 | PostScript 打印 |

### PNG 导出设置

| 设置 | 描述 | 建议 |
|------|------|------|
| DPI | 分辨率 | Web 用 72，印刷用 300 |
| Background | 透明 | Web 图形启用 |
| Selection area | 导出选区 | 用于单个对象 |
| Batch | 多页 | 一次全部导出 |

### SVG 导出选项

| 选项 | 描述 | 用途 |
|------|------|------|
| Plain SVG | 无 Inkscape 元数据 | Web 使用 |
| Inkscape SVG | 完整元数据 | 重新编辑 |
| Optimized SVG | 减小文件大小 | 生产环境 |

## 键盘快捷键

### 基本快捷键

| 操作 | 快捷键 | 分类 |
|------|--------|------|
| 全选 | Ctrl+A | 选择 |
| 分组 | Ctrl+G | 对象 |
| 取消分组 | Ctrl+Shift+G | 对象 |
| 复制 | Ctrl+D | 编辑 |
| 克隆 | Ctrl+Shift+D | 编辑 |
| 撤销 | Ctrl+Z | 编辑 |
| 重做 | Ctrl+Shift+Z | 编辑 |
| 保存 | Ctrl+S | 文件 |
| 导出 PNG | Ctrl+Shift+E | 文件 |

### 工具快捷键

| 工具 | 快捷键 | 工具 | 快捷键 |
|------|--------|------|--------|
| Select | S | Node | N |
| Rectangle | R | Ellipse | E |
| Star | * | Spiral | I |
| Pen | B | Pencil | P |
| Text | T | Zoom | Z |
| Dropper | I | Paint Bucket | U |

## 实际项目

### 标志设计工作流

| 步骤 | 工具 | 操作 |
|------|------|------|
| 1 | Pen, Shapes | 创建基础形状 |
| 2 | Node Edit | 精修路径 |
| 3 | Boolean | 合并形状 |
| 4 | Fill/Stroke | 应用颜色 |
| 5 | Text | 添加文本 |
| 6 | Export | SVG 和 PNG |

### 图标设计工作流

| 步骤 | 工具 | 操作 |
|------|------|------|
| 1 | Grid | 启用像素网格 |
| 2 | Shapes | 从基本形状构建 |
| 3 | Boolean | 合并和减去 |
| 4 | Stroke | 统一描边宽度 |
| 5 | Align | 完美对齐 |
| 6 | Export | 多种尺寸 |

## 总结

Inkscape 提供了一套全面的矢量图形工具，适用于专业插图和设计工作。其路径编辑功能、文本处理和滤镜效果使其适用于各种图形设计任务。

关键实践：

- 使用路径操作和布尔工具创建复杂形状
- 使用图层组织复杂插图
- 利用节点编辑进行精确路径控制
- 导出 SVG 用于 Web 和印刷，PNG 用于光栅需求
- 使用对齐工具精确定位对象


---

## 来源：viewer.md

## 简介

qView 是一个极简的开源图片查看器，专为速度和简洁而设计。它专注于提供纯净的查看体验，没有多余的功能。本教程涵盖安装、导航、配置和键盘快捷键。

## 设计理念

| 原则 | 实现 |
|------|------|
| Minimalism | 默认无工具栏或面板 |
| Speed | 快速图片加载和切换 |
| Focus | 内容优先的查看体验 |
| Native | 平台特定的外观和感觉 |

## 安装

### 平台特定

| 平台 | 方式 | 命令/来源 |
|------|------|-----------|
| macOS | Homebrew | `brew install --cask qview` |
| macOS | DMG | 从 GitHub releases 下载 |
| Windows | Installer | 从 GitHub releases 下载 |
| Windows | Scoop | `scoop install qview` |
| Linux | Flatpak | `flatpak install com.github.jurple-l.qview` |
| Linux | AppImage | 从 GitHub releases 下载 |

### 验证安装

从应用菜单打开 qView 或从终端运行：

```bash
qview /path/to/image.jpg
```

## 支持格式

### 图片格式

| 格式 | 扩展名 | 支持级别 |
|------|--------|----------|
| JPEG | .jpg, .jpeg | 完全 |
| PNG | .png | 完全 |
| GIF | .gif | 完全，动画 |
| BMP | .bmp | 完全 |
| WebP | .webp | 完全 |
| TIFF | .tiff, .tif | 完全 |
| SVG | .svg | 完全 |
| ICO | .ico | 完全 |
| AVIF | .avif | 完全 |
| HEIF | .heif, .heic | 完全 |

### 格式能力

| 能力 | 支持的格式 |
|------|-----------|
| Animation | GIF, WebP, APNG |
| Transparency | PNG, GIF, WebP, SVG |
| Metadata | JPEG, PNG, TIFF |
| High bit depth | PNG, TIFF, WebP |

## 界面

### 窗口元素

| 元素 | 可见性 | 功能 |
|------|--------|------|
| Title bar | 始终 | 显示文件名 |
| Menu bar | 切换 | 文件、编辑、视图菜单 |
| Image area | 始终 | 主查看区域 |
| Info overlay | 切换 | 文件信息显示 |
| Window controls | 始终 | 最小化、最大化、关闭 |

### 显示模式

| 模式 | 描述 | 快捷键 |
|------|------|--------|
| Window | 可调大小窗口 | 默认 |
| Fullscreen | 全屏视图 | F11 |
| Frameless | 无窗口边框 | F10 |
| Always on Top | 保持可见 | Ctrl+Shift+T |

## 导航

### 打开图片

| 方法 | 描述 |
|------|------|
| File > Open | 浏览并选择文件 |
| Drag and drop | 拖放到窗口 |
| Command line | `qview image.jpg` |
| File association | 双击图片文件 |
| Recent files | File > Open Recent |

### 浏览图片

| 操作 | 方法 | 快捷键 |
|------|------|--------|
| 下一张 | 右箭头或点击 | Right |
| 上一张 | 左箭头或点击 | Left |
| 第一张 | Home | Home |
| 最后一张 | End | End |
| 跳转到 | 输入文件名 | Ctrl+G |

### 文件夹导航

打开图片时，qView 会加载同一文件夹中的所有图片：

| 行为 | 描述 |
|------|------|
| Sequential | 浏览文件夹内容 |
| Sorted | 按字母或日期排序 |
| Filtered | 仅显示支持的格式 |

## 缩放和平移

### 缩放控制

| 操作 | 方法 | 快捷键 |
|------|------|--------|
| 放大 | 向上滚动或 Ctrl++ | + |
| 缩小 | 向下滚动或 Ctrl+- | - |
| 适合窗口 | 双击 | F |
| 适合宽度 | Ctrl+W | W |
| 适合高度 | Ctrl+H | H |
| 原始大小 (100%) | Ctrl+0 | 0 |
| 自定义缩放 | Ctrl+滚动 | - |

### 平移控制

| 操作 | 方法 |
|------|------|
| 平移图片 | 点击并拖动 |
| 滚动平移 | 滚轮（缩放时） |
| 重置位置 | 双击 |

## 图片操作

### 旋转和翻转

| 操作 | 快捷键 | 效果 |
|------|--------|------|
| 右旋转 | R | 顺时针 90 度 |
| 左旋转 | Shift+R | 逆时针 90 度 |
| 水平翻转 | H | 左右镜像 |
| 垂直翻转 | V | 上下镜像 |
| 重置 | Ctrl+R | 返回原始 |

### 变换行为

| 变换 | 持久性 | 文件修改 |
|------|--------|----------|
| Rotation | 仅会话 | 否 |
| Flip | 仅会话 | 否 |
| Zoom | 仅会话 | 否 |

## 信息显示

### 文件信息

| 信息 | 描述 | 切换 |
|------|------|------|
| Filename | 当前文件名 | 始终可见 |
| Dimensions | 宽 x 高 | I 键 |
| File size | 字节、KB、MB | I 键 |
| Format | 图片类型 | I 键 |
| Color depth | 每通道位数 | I 键 |

### 信息覆盖

按 I 切换信息覆盖：

```
image.jpg
4000 x 3000
12.5 MB
JPEG
```

## 幻灯片

### 幻灯片控制

| 操作 | 快捷键 | 描述 |
|------|--------|------|
| 开始幻灯片 | S | 开始自动推进 |
| 停止幻灯片 | S 或 Esc | 结束幻灯片 |
| 下一张 | Right | 手动前进 |
| 上一张 | Left | 返回 |

### 幻灯片设置

| 设置 | 选项 | 默认值 |
|------|------|--------|
| Interval | 1-60 秒 | 5 秒 |
| Loop | 是/否 | 是 |
| Random order | 是/否 | 否 |
| Transition | 无、淡入淡出 | 无 |

## 配置

### 设置分类

| 分类 | 选项 |
|------|------|
| General | 启动行为、文件关联 |
| Interface | 窗口、工具栏、覆盖 |
| Controls | 鼠标、键盘、手势 |
| Image | 加载、缓存、质量 |
| Slideshow | 计时、过渡 |

### 关键设置

| 设置 | 描述 | 建议 |
|------|------|------|
| Startup image | 启动时的图片 | 上次查看或无 |
| Window remember | 保存位置 | 启用 |
| Filtering | 图片缩放 | 照片用双线性 |
| Bilinear | 平滑缩放 | 大图片启用 |
| Preloading | 加载相邻图片 | 速度启用 |

## 键盘快捷键

### 基本快捷键

| 操作 | 快捷键 | 分类 |
|------|--------|------|
| 打开文件 | Ctrl+O | 文件 |
| 退出 | Ctrl+Q | 文件 |
| 全屏 | F11 | 视图 |
| 信息切换 | I | 视图 |
| 放大 | + | 缩放 |
| 缩小 | - | 缩放 |
| 适合窗口 | F | 缩放 |
| 原始大小 | 0 | 缩放 |
| 下一张图片 | Right | 导航 |
| 上一张图片 | Left | 导航 |
| 右旋转 | R | 变换 |
| 左旋转 | Shift+R | 变换 |
| 水平翻转 | H | 变换 |
| 垂直翻转 | V | 变换 |
| 幻灯片 | S | 功能 |
| 删除 | Delete | 文件 |

### 快捷键参考

| 分类 | 快捷键 |
|------|--------|
| File | Ctrl+O, Ctrl+S, Delete, Ctrl+Q |
| View | F11, F10, I, B |
| Zoom | +, -, 0, F, W, H |
| Navigate | Right, Left, Home, End |
| Transform | R, Shift+R, H, V, Ctrl+R |
| Slideshow | S, Esc |

## 文件操作

### 快速操作

| 操作 | 快捷键 | 描述 |
|------|--------|------|
| Open location | Ctrl+L | 打开包含文件夹 |
| Copy path | Ctrl+Shift+C | 复制文件路径 |
| Copy image | Ctrl+C | 复制到剪贴板 |
| Rename | F2 | 重命名当前文件 |
| Delete | Delete | 移到回收站 |
| Properties | Ctrl+I | 文件属性 |

## 性能

### 优化提示

| 提示 | 描述 | 影响 |
|------|------|------|
| SSD storage | 将图片存储在 SSD | 更快加载 |
| Hardware acceleration | GPU 渲染 | 更流畅缩放/平移 |
| Memory cache | 保留在 RAM | 更快导航 |
| Image preloading | 加载相邻文件 | 即时切换 |

### 资源使用

| 指标 | 典型使用 |
|------|----------|
| Memory | 50-200 MB |
| CPU | 空闲 < 1%，缩放时 5-10% |
| Disk | 加载后最小 |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 图片未加载 | 不支持的格式 | 检查格式支持 |
| 加载慢 | 大文件 | 启用硬件加速 |
| 无动画 | 静态查看器 | 验证 GIF/APNG 支持 |
| 图片模糊 | 缩放滤镜 | 调整缩放设置 |
| 文件关联 | 系统设置 | 设置 qView 为默认 |

## 与其他查看器对比

| 功能 | qView | IrfanView | Preview | feh |
|------|-------|-----------|---------|-----|
| Speed | 快 | 快 | 快 | 最快 |
| Interface | 极简 | 完整 | 简洁 | CLI |
| Editing | 无 | 基本 | 基本 | 无 |
| Format support | 良好 | 优秀 | 良好 | 良好 |
| Platform | 全部 | Windows | macOS | Linux |
| Price | 免费 | 免费 | 免费 | 免费 |

## 总结

qView 提供了一个专注、快速的图片查看体验，没有完整图片编辑器的复杂性。其极简界面和键盘驱动的导航使其非常适合快速图片浏览和审查。

关键实践：

- 使用键盘快捷键高效导航
- 启用硬件加速以获得流畅性能
- 设置为默认图片查看器以便快速访问
- 使用全屏模式进行无干扰查看
- 利用幻灯片功能进行演示


---
