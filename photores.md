# 使用 Awesome Open Source Photography 摄影工具

## 简介

awesome-OpenSourcePhotography 合集精选了面向摄影师的最佳开源工具。本教程提供了一个结构化的指南，涵盖用于编辑、处理、管理和分享照片的软件。

## 工具分类

| 分类 | 用途 | 示例 |
|------|------|------|
| RAW 处理器 | 处理 RAW 文件 | darktable, RawTherapee |
| 光栅编辑器 | 像素级编辑 | GIMP, Krita |
| RAW 库 | 读取相机 RAW | LibRaw, rawpy |
| 照片管理器 | 组织和策展 | digiKam, Shotwell |
| 全景工具 | 拼接多张图片 | Hugin |
| HDR 处理器 | 高动态范围 | Luminance HDR |
| 色彩管理 | ICC 配置文件 | ArgyllCMS |
| 元数据工具 | EXIF/IPTC 编辑 | ExifTool |
| 联机拍摄 | 相机控制 | Entangle, gPhoto2 |
| 发布 | 创建相册 | Lychee, Piwigo |

## RAW 处理器

### 对比

| 功能 | darktable | RawTherapee |
|------|-----------|-------------|
| 界面 | 胶片条 + 暗房 | 标签面板 |
| 破坏性编辑 | 非破坏性 | 非破坏性 |
| 联机拍摄 | 是 | 否 |
| DAM 功能 | 是 | 有限 |
| GPU 加速 | OpenCL | 部分 |
| 插件支持 | Lua 脚本 | 否 |
| 平台 | Linux, macOS, Windows | Linux, macOS, Windows |
| 许可证 | GPL-3.0 | GPL-3.0 |

### darktable 模块

| 模块分类 | 模块 | 用途 |
|----------|------|------|
| 基本 | exposure, contrast, brightness | 全局调整 |
| 色调 | levels, curve, zone system | 色调控制 |
| 颜色 | white balance, color balance | 颜色校正 |
| 细节 | sharpen, denoise, blur | 锐度和噪点 |
| 校正 | lens, perspective, crop | 几何校正 |
| 效果 | vignette, grain, bloom | 创意效果 |

### RawTherapee 工具

| 工具 | 标签 | 功能 |
|------|------|------|
| Exposure | Exposure | 亮度、对比度、高光 |
| Shadows/Highlights | Exposure | 恢复阴影和高光 |
| White Balance | Color | 色温和色调 |
| Noise Reduction | Detail | 亮度和色度噪点 |
| Sharpening | Detail | 边缘增强 |
| Lens Corrections | Transform | 畸变、暗角 |
| Tone Curve | Advanced | 自定义色调映射 |

## 光栅编辑器

### 对比

| 功能 | GIMP | Krita |
|------|------|-------|
| 主要用途 | 照片编辑 | 数字绘画 |
| CMYK 支持 | 有限 | 完全 |
| 非破坏性 | 通过图层 | 通过图层和蒙版 |
| 色彩管理 | 完全 ICC | 完全 ICC |
| 插件生态 | 丰富 | 发展中 |
| 平台 | 所有主流 | 所有主流 |
| 许可证 | GPL-3.0 | GPL-3.0 |

### GIMP 基本工具

| 工具 | 用途 | 快捷键 |
|------|------|--------|
| Move | 重新定位图层 | M |
| Crop | 裁剪图像 | Shift+C |
| Scale | 调整图像大小 | Shift+T |
| Rotate | 旋转图像 | Shift+R |
| Color Balance | 调整色调 | - |
| Levels | 调整色调范围 | - |
| Curves | 精细色调控制 | - |
| Clone | 去除瑕疵 | C |
| Heal | 平滑修复 | H |
| Dodge/Burn | 加亮/加深区域 | Shift+D |

### Krita 摄影功能

| 功能 | 描述 | 用途 |
|------|------|------|
| Transform Masks | 非破坏性变换 | 无损调整大小 |
| Filter Layers | 将滤镜作为图层 | 不修改像素的调整 |
| Color Space | CMYK 和 Lab 支持 | 印刷准备 |
| HDR Painting | 高位深编辑 | HDR 照片处理 |

## 照片管理

### digiKam 功能

| 功能 | 描述 | 优势 |
|------|------|------|
| Database | SQLite 或 MySQL | 快速搜索 |
| Tags | 分层关键词 | 组织 |
| Ratings | 星级评分 | 策展 |
| Face Detection | 自动识别 | 人物分类 |
| Geo-tagging | 地图集成 | 位置组织 |
| Batch Processing | 应用到多个文件 | 效率 |
| Versioning | 跟踪编辑历史 | 非破坏性工作流 |
| Import | 相机/存储卡导入 | 工作流开始 |

### Shotwell 功能

| 功能 | 描述 | 最适合 |
|------|------|--------|
| Auto-import | 监视文件夹 | 简单组织 |
| Events | 基于日期的分组 | 按时间浏览 |
| Basic editing | 裁剪、旋转、增强 | 快速调整 |
| Publishing | 直接上传 | 社交分享 |
| RAW support | 通过 rawpy | 基本 RAW 处理 |

## 全景工具

### Hugin 工作流

| 步骤 | 操作 | 工具 |
|------|------|------|
| 1 | 加载图片 | Hugin 主界面 |
| 2 | 对齐控制点 | 自动或手动 |
| 3 | 设置投影 | Panini, equirectangular 等 |
| 4 | 优化 | 最小化拼接误差 |
| 5 | 裁剪和混合 | 最终调整 |
| 6 | 导出 | TIFF, JPEG, PNG |

### 投影类型

| 投影 | 用途 | 畸变 |
|------|------|------|
| Rectilinear | 建筑 | 保持直线 |
| Cylindrical | 宽幅全景 | 边缘最小 |
| Spherical | 360 度视图 | 均匀分布 |
| Equirectangular | VR 环境 | 完整球面映射 |

## HDR 处理

### Luminance HDR 工作流

| 步骤 | 操作 | 设置 |
|------|------|------|
| 1 | 加载包围曝光图片 | 3-7 张曝光 |
| 2 | 对齐图片 | 自动或手动 |
| 3 | 选择 HDR 算法 | Mantiuk, Fattal, Drago |
| 4 | 色调映射 | 调整参数 |
| 5 | 微调 | 对比度、饱和度 |
| 6 | 导出 | 8 位或 16 位 |

### HDR 算法

| 算法 | 特点 | 最适合 |
|------|------|--------|
| Mantiuk 2006 | 高细节 | 自然场景 |
| Mantiuk 2008 | 均衡 | 通用 |
| Fattal | 戏剧性 | 高对比度场景 |
| Drago | 微妙 | 建筑 |
| Reinhard | 自然 | 人像 |

## 元数据工具

### ExifTool 命令

| 命令 | 用途 |
|------|------|
| `exiftool file.jpg` | 查看所有元数据 |
| `exiftool -AllDates file.jpg` | 查看日期信息 |
| `exiftool -Copyright="Name" file.jpg` | 设置版权 |
| `exiftool -GPSLatitude=40.7128 file.jpg` | 设置 GPS 坐标 |
| `exiftool -all= file.jpg` | 移除所有元数据 |
| `exiftool -r -TagsFromFile src.jpg dst.jpg` | 复制元数据 |

### 元数据字段

| 字段 | 描述 | 用途 |
|------|------|------|
| EXIF | 相机设置 | 技术参考 |
| IPTC | 内容描述 | 发布工作流 |
| XMP | 扩展元数据 | 现代标准 |
| GPS | 位置数据 | 地理标记 |
| Copyright | 所有权 | 法律保护 |

## 色彩管理

### ArgyllCMS 工作流

| 步骤 | 命令 | 用途 |
|------|------|------|
| 1 | `scanin` | 读取色块 |
| 2 | `colprof` | 生成 ICC 配置文件 |
| 3 | `dispwin` | 安装显示器配置文件 |
| 4 | `targen` | 生成测试目标 |

### ICC 配置文件类型

| 类型 | 用途 | 设备 |
|------|------|------|
| Input | 扫描仪/相机 | 采集设备 |
| Display | 显示器校准 | 屏幕 |
| Output | 打印机配置文件 | 打印机 |
| Device Link | 直接转换 | 工作流 |

## 联机拍摄

### gPhoto2 命令

| 命令 | 用途 |
|------|------|
| `gphoto2 --auto-detect` | 查找连接的相机 |
| `gphoto2 --capture-image` | 拍摄照片 |
| `gphoto2 --capture-tethered` | 连续拍摄 |
| `gphoto2 --list-files` | 显示相机文件 |
| `gphoto2 --get-all-files` | 下载所有照片 |

### Entangle 功能

| 功能 | 描述 |
|------|------|
| Live view | 实时相机预览 |
| Remote capture | 从电脑触发 |
| Auto download | 拍摄时传输 |
| Tethered control | 从 UI 控制相机设置 |

## 在线相册

### Lychee vs Piwigo

| 功能 | Lychee | Piwigo |
|------|--------|--------|
| 安装 | PHP + MySQL | PHP + MySQL |
| 界面 | 现代、简洁 | 传统 |
| 相册 | 扁平结构 | 分层 |
| 分享 | 公开/私密链接 | 用户权限 |
| 插件 | 有限 | 丰富 |
| 移动端 | 响应式 | 响应式 + 应用 |

## 工作流建议

### 专业工作流

| 阶段 | 工具 | 用途 |
|------|------|------|
| 导入 | digiKam, gPhoto2 | 传输和组织 |
| 筛选 | digiKam | 评分和选择 |
| RAW 处理 | darktable | 主要调整 |
| 编辑 | GIMP | 修图、合成 |
| 颜色 | ArgyllCMS | 显示器校准 |
| 元数据 | ExifTool | 版权、关键词 |
| 输出 | darktable, GIMP | 导出使用 |
| 存档 | digiKam | 长期存储 |

### 爱好者工作流

| 阶段 | 工具 | 用途 |
|------|------|------|
| 导入 | Shotwell | 简单传输 |
| 组织 | Shotwell | 基本组织 |
| 处理 | RawTherapee | RAW 处理 |
| 编辑 | GIMP | 快速编辑 |
| 分享 | Lychee | 在线相册 |

## 总结

开源摄影生态系统为摄影工作流的每个阶段提供了专业级工具。从 RAW 处理到在线发布，这些工具提供了与商业替代品相当的功能。

关键建议：

- 根据界面偏好选择 darktable 或 RawTherapee 进行 RAW 处理
- 结合 digiKam 进行组织，GIMP 进行精细编辑
- 使用 ArgyllCMS 校准显示器以获得准确颜色
- 使用 ExifTool 管理元数据和保护版权
- 设置 Piwigo 或 Lychee 进行自托管照片分享
