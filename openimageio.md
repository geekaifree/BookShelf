# OpenImageIO：VFX 图像 I/O 库

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
