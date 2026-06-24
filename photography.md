# 摄影

> 本文档整合了以下源文件：camera.md, photores.md, raw.md, photography.md, photo.md

---

## 来源：camera.md

## 简介

开源摄影工具提供专业级的功能，无需订阅费用。本指南涵盖了完整的摄影工作流程，从拍摄到最终输出，全部使用免费和开源软件。

## 目录

- [照片编辑器](#照片编辑器)
- [RAW 处理](#raw-处理)
- [数字暗房](#数字暗房)
- [色彩管理](#色彩管理)
- [元数据管理](#元数据管理)
- [全景工具](#全景工具)
- [HDR 处理](#hdr-处理)
- [景深合成](#景深合成)
- [联机拍摄](#联机拍摄)
- [数字资产管理 (DAM)](#数字资产管理-dam)
- [工作流建议](#工作流建议)

---

## 照片编辑器

通用图像编辑应用。

### 主要开源照片编辑器

| 编辑器 | 类型 | 平台 | 许可证 | 最佳用途 |
|--------|------|------|--------|----------|
| GIMP | 光栅编辑器 | 全平台 | GPL | 通用照片编辑 |
| Krita | 绘画/照片 | 全平台 | GPL | 数字绘画、照片艺术 |
| Photopea | 基于 Web | 浏览器 | 专有（免费） | 类 Photoshop 编辑 |
| Pinta | 简单编辑器 | 全平台 | MIT | 基础编辑 |
| Pixelitor | 光栅编辑器 | 全平台 | GPL | 基于 Java 的编辑 |

### GIMP（GNU 图像处理程序）

GIMP 是最广泛使用的开源照片编辑器。

**核心功能：**

| 功能 | 描述 |
|------|------|
| 图层 | 多图层，支持混合模式 |
| 蒙版 | 图层蒙版，非破坏性编辑 |
| 通道 | 单独的颜色通道编辑 |
| 路径 | 用于选区和形状的矢量路径 |
| 滤镜 | 丰富的滤镜库 |
| 脚本 | Script-Fu 和 Python 脚本 |
| 插件 | 大型插件生态系统 |

**常用 GIMP 工具：**

| 工具 | 用途 | 快捷键 |
|------|------|--------|
| 移动 | 移动图层和选区 | M |
| 矩形选区 | 矩形选区 | R |
| 椭圆选区 | 椭圆选区 | E |
| 自由选区 | 自由手绘选区 | F |
| 模糊选区 | 魔棒选区 | U |
| 按颜色选 | 按颜色选择 | Shift+O |
| 画笔 | 用画笔绘画 | P |
| 克隆 | 克隆图章 | C |
| 修复 | 修复画笔 | H |
| 桶填充 | 填充区域 | Shift+B |
| 渐变 | 渐变工具 | G |
| 文字 | 添加文字 | T |

### GIMP vs Photoshop 对比

| 功能 | GIMP | Photoshop |
|------|------|-----------|
| 价格 | 免费 | 订阅制 |
| 图层 | 是 | 是 |
| CMYK | 有限（插件） | 完整支持 |
| RAW 处理 | 通过插件（UFRaw） | 内置（Camera Raw） |
| 非破坏性 | 有限 | 完整支持 |
| 自动化 | Script-Fu、Python | Actions、脚本 |
| 插件生态 | 良好 | 优秀 |
| 行业标准 | 否 | 是 |

---

## RAW 处理

RAW 处理器处理未加工的相机数据，以获得最大质量和灵活性。

### 开源 RAW 处理器

| 处理器 | 类型 | 平台 | 许可证 | 核心功能 |
|--------|------|------|--------|----------|
| darktable | 非破坏性 | 全平台 | GPL | 灯箱 + 暗房 |
| RawTherapee | 非破坏性 | 全平台 | GPL | 高级处理 |
| digiKam | DAM + RAW | 全平台 | GPL | 完整工作流 |
| Filmulator | 胶片模拟 | 全平台 | GPL | 胶片风格渲染 |
| ART（Another RawTherapee） | 分支 | 全平台 | GPL | 简化界面 |

### darktable

darktable 是一个摄影工作流应用和 RAW 显影器。

**模块：**

| 类别 | 模块 | 用途 |
|------|------|------|
| 基础 | 曝光、对比度、白平衡 | 基本调整 |
| 颜色 | 色彩平衡、色彩区域、Velvia | 色彩分级 |
| 色调 | 色调曲线、色阶、区域系统 | 色调调整 |
| 细节 | 锐化、降噪、去边 | 图像细节 |
| 效果 | 暗角、颗粒、光晕 | 创意效果 |
| 校正 | 镜头校正、旋转、裁剪 | 校正 |

**darktable 快捷键：**

| 快捷键 | 操作 |
|--------|------|
| D | 切换到暗房 |
| L | 切换到灯箱 |
| Tab | 切换面板 |
| Ctrl+E | 导出 |
| / | 适合缩放 |
| 空格 | 100% 缩放 |

### RawTherapee

RawTherapee 专注于 RAW 处理，提供精细控制。

**核心功能：**

| 功能 | 描述 |
|------|------|
| 曝光 | 曝光补偿、高光/阴影恢复 |
| 细节 | 微对比度、反卷积锐化 |
| 颜色 | 白平衡、HSV 均衡器、色调 |
| 降噪 | 多种算法（中值、脉冲、噪声） |
| 镜头校正 | 畸变、色差、暗角 |
| 变换 | 旋转、透视校正、裁剪 |

### RAW 处理工作流

| 步骤 | 工具 | 操作 |
|------|------|------|
| 1. 导入 | darktable/digiKam | 从相机复制 |
| 2. 选择 | darktable 灯箱 | 评分和标签 |
| 3. 显影 | darktable/RawTherapee | 处理 RAW 文件 |
| 4. 导出 | darktable/RawTherapee | 导出为 JPEG/TIFF |
| 5. 最终编辑 | GIMP | 修图、合成 |

---

## 数字暗房

数字暗房是你处理和增强照片的地方。

### 非破坏性编辑原则

| 原则 | 描述 |
|------|------|
| 保留原始 | 永不修改原始文件 |
| 调整图层 | 使用图层/蒙版进行编辑 |
| 附属文件 | 将编辑存储在单独的文件中 |
| 版本控制 | 保留多个编辑版本 |
| 按需导出 | 需要时才生成输出文件 |

### 核心调整

| 调整 | 用途 | 使用时机 |
|------|------|----------|
| 白平衡 | 校正色温 | 始终首先检查 |
| 曝光 | 整体亮度 | 曝光不准时 |
| 对比度 | 色调范围 | 曝光校正后 |
| 高光 | 恢复过曝高光 | 高光被裁剪时 |
| 阴影 | 提亮暗部 | 阴影太暗时 |
| 清晰度/结构 | 中间调对比度 | 增加局部对比 |
| 自然饱和度 | 饱和度（保护肤色） | 色彩增强 |
| 饱和度 | 整体色彩强度 | 谨慎使用 |
| 锐度 | 边缘定义 | 缩放后应用 |
| 降噪 | 去除颗粒 | 高 ISO 图像 |

### 调整顺序

推荐的照片调整顺序：

| 顺序 | 调整 | 原因 |
|------|------|------|
| 1 | 白平衡 | 影响所有颜色决策 |
| 2 | 曝光 | 设定整体亮度 |
| 3 | 高光/阴影 | 色调恢复 |
| 4 | 对比度 | 色调范围 |
| 5 | 颜色（自然饱和度/饱和度） | 色彩增强 |
| 6 | 局部调整 | 针对性编辑 |
| 7 | 锐化 | 细节增强 |
| 8 | 降噪 | 清理颗粒 |
| 9 | 镜头校正 | 畸变、色差 |
| 10 | 裁剪/拉直 | 构图 |

---

## 色彩管理

色彩管理确保跨设备的一致颜色。

### 色彩管理概念

| 概念 | 描述 |
|------|------|
| 色彩空间 | 设备能产生的颜色范围 |
| ICC 配置文件 | 设备颜色的数学描述 |
| 色域 | 可重现的总颜色范围 |
| 渲染意图 | 如何处理色域外的颜色 |
| 校准 | 将设备调整到标准 |
| 分析 | 测量设备的颜色特性 |

### 常见色彩空间

| 色彩空间 | 色域 | 使用场景 |
|----------|------|----------|
| sRGB | 最小 | Web、标准显示器 |
| Adobe RGB | 中等 | 摄影、印刷 |
| ProPhoto RGB | 最大 | 专业摄影 |
| DCI-P3 | 中-大 | 视频、Apple 显示器 |

### 色彩管理工具

| 工具 | 用途 | 平台 |
|------|------|------|
| DisplayCAL | 显示器校准 | 全平台 |
| ArgyllCMS | 色彩管理系统 | 全平台 |
| Little CMS | 色彩管理库 | 全平台 |
| GICC | ICC 配置文件支持 | 全平台 |
| darktable | 色彩管理工作流 | 全平台 |

### 显示器校准流程

| 步骤 | 操作 | 工具 |
|------|------|------|
| 1 | 预热显示器（30 分钟） | 手动 |
| 2 | 设置显示器到目标亮度 | 显示器控制 |
| 3 | 设置色温（6500K） | 显示器控制 |
| 4 | 运行校准软件 | DisplayCAL |
| 5 | 用色度计测量 | 硬件传感器 |
| 6 | 生成 ICC 配置文件 | DisplayCAL |
| 7 | 安装配置文件 | 系统设置 |

---

## 元数据管理

元数据存储关于你照片的信息。

### 元数据类型

| 类型 | 标准 | 包含内容 | 可编辑 |
|------|------|----------|--------|
| EXIF | 相机数据 | 相机设置、日期、GPS | 有限 |
| IPTC | 新闻数据 | 标题、描述、关键词 | 是 |
| XMP | Adobe 标准 | 所有类型、可扩展 | 是 |

### 关键元数据字段

| 字段 | 类别 | 用途 |
|------|------|------|
| 标题 | IPTC | 简短描述 |
| 描述 | IPTC | 详细说明 |
| 关键词 | IPTC | 可搜索标签 |
| 作者 | IPTC | 摄影师姓名 |
| 版权 | IPTC | 版权声明 |
| 拍摄日期 | EXIF | 拍摄日期/时间 |
| GPS | EXIF | 位置坐标 |
| 相机 | EXIF | 相机型号 |
| 镜头 | EXIF | 镜头型号 |
| ISO | EXIF | 感光度 |
| 光圈 | EXIF | 光圈值 |
| 快门速度 | EXIF | 曝光时间 |

### 元数据工具

| 工具 | 用途 | 平台 |
|------|------|------|
| ExifTool | 读写所有元数据 | CLI、全平台 |
| digiKam | 元数据管理 | GUI、全平台 |
| darktable | 工作流中的元数据 | GUI、全平台 |
| Exiv2 | EXIF/IPTC/XMP 库 | CLI、全平台 |

### ExifTool 命令

| 命令 | 用途 |
|------|------|
| `exiftool file.jpg` | 读取所有元数据 |
| `exiftool -Title="My Photo" file.jpg` | 设置标题 |
| `exiftool -Keywords="nature" -Keywords="forest" file.jpg` | 添加关键词 |
| `exiftool -AllDates="2024:01:15 10:30:00" file.jpg` | 设置日期 |
| `exiftool -GPSLatitude=40.7128 -GPSLongitude=-74.0060 file.jpg` | 设置 GPS |
| `exiftool -all= file.jpg` | 清除所有元数据 |

---

## 全景工具

从多张照片创建全景图像的工具。

### 全景工作流

| 步骤 | 工具 | 操作 |
|------|------|------|
| 1. 拍摄 | 相机 | 重叠 30-50% |
| 2. 检测控制点 | Hugin | 查找匹配特征 |
| 3. 对齐 | Hugin | 优化定位 |
| 4. 投影 | Hugin | 应用投影 |
| 5. 混合 | Enblend | 无缝拼接 |
| 6. 裁剪 | GIMP | 最终构图 |

### 全景软件

| 软件 | 类型 | 平台 | 许可证 |
|------|------|------|--------|
| Hugin | 完整全景套件 | 全平台 | GPL |
| Enblend | 曝光混合 | 全平台 | GPL |
| PanoTools | 库/插件 | 全平台 | GPL |
| Microsoft ICE | 拼接 | Windows | 免费（专有） |

### 全景拍摄技巧

| 技巧 | 描述 |
|------|------|
| 重叠 | 拍摄之间重叠 30-50% |
| 水平 | 保持相机水平（使用三脚架） |
| 一致曝光 | 使用手动曝光设置 |
| 不变焦 | 保持焦距不变 |
| 绕节点旋转 | 避免视差误差 |
| 拍 RAW | 最大化拼接质量 |

### 全景投影

| 投影 | 最佳用途 | 描述 |
|------|----------|------|
| 直线 | 建筑 | 保持直线 |
| 柱面 | 宽风景 | 360 度水平 |
| 球面 | 完整 360x180 | 完整球体 |
| 墨卡托 | 交互式全景 | Web 浏览 |

---

## HDR 处理

HDR（高动态范围）结合多次曝光以获得更宽的色调范围。

### HDR 工作流

| 步骤 | 工具 | 操作 |
|------|------|------|
| 1. 拍摄 | 相机 | 包围曝光（3-7 张） |
| 2. 对齐 | Hugin/Luminance HDR | 对齐手持拍摄 |
| 3. 合并 | Luminance HDR | 合并曝光 |
| 4. 色调映射 | Luminance HDR | 压缩动态范围 |
| 5. 调整 | GIMP/darktable | 最终处理 |

### HDR 软件

| 软件 | 类型 | 平台 | 许可证 |
|------|------|------|--------|
| Luminance HDR | 完整 HDR 套件 | 全平台 | GPL |
| HDRMerge | RAW 合并 | 全平台 | GPL |
| Hugin | 对齐 + 合并 | 全平台 | GPL |
| GIMP | 通过插件实现 HDR | 全平台 | GPL |

### HDR 拍摄设置

| 设置 | 建议 |
|------|------|
| 曝光数 | 3（最少）、5-7（推荐） |
| 曝光间距 | 拍摄之间 1-2 EV |
| 模式 | 自动包围曝光（AEB） |
| 对焦 | 手动对焦（锁定） |
| 光圈 | 光圈优先（恒定景深） |
| 三脚架 | 推荐以获得最佳效果 |

### 色调映射方法

| 方法 | 效果 | 最佳用途 |
|------|------|----------|
| Mantiuk | 自然、保持对比度 | 风景 |
| Fattal | 艺术、戏剧性 | 创意作品 |
| Drago | 平衡、自然 | 通用 |
| Reinhard | 摄影风格 | 逼真效果 |
| Pattanaik | 视觉适应 | 微妙 HDR |

---

## 景深合成

景深合成结合不同对焦距离的多张图像以获得更大的景深。

### 景深合成工作流

| 步骤 | 工具 | 操作 |
|------|------|------|
| 1. 拍摄 | 相机 | 拍摄对焦系列 |
| 2. 对齐 | Hugin/Enfuse | 对齐图像 |
| 3. 合成 | Enfuse/CombineZP | 合并对焦区域 |
| 4. 清理 | GIMP | 移除伪影 |

### 景深合成软件

| 软件 | 类型 | 平台 | 许可证 |
|------|------|------|--------|
| Enfuse | 对焦/曝光混合 | 全平台 | GPL |
| Hugin | 对齐 + 合成 | 全平台 | GPL |
| CombineZP | 景深合成 | Windows | 免费 |
| Picolay | 景深合成 | Windows | 免费 |

### 景深合成拍摄技巧

| 技巧 | 描述 |
|------|------|
| 三脚架 | 对齐必需 |
| 手动对焦 | 一致控制 |
| 对焦步长 | 小步、有重叠 |
| 光圈 | 使用中等光圈（f/5.6-f/8） |
| 遥控触发 | 避免相机抖动 |
| 一致光线 | 拍摄之间不变 |

---

## 联机拍摄

联机拍摄将相机直接连接到计算机，实现实时拍摄和查看。

### 联机拍摄软件

| 软件 | 平台 | 许可证 | 相机支持 |
|------|------|--------|----------|
| gPhoto2 | Linux/macOS | GPL | 许多 DSLR |
| Entangle | Linux | GPL | 通过 libgphoto2 支持 DSLR |
| Darktable | 全平台 | GPL | 通过 gPhoto2 |
| digiKam | 全平台 | GPL | 通过 gPhoto2 |

### gPhoto2 命令

| 命令 | 用途 |
|------|------|
| `gphoto2 --list-cameras` | 列出支持的相机 |
| `gphoto2 --auto-detect` | 检测连接的相机 |
| `gphoto2 --capture-image` | 拍照 |
| `gphoto2 --capture-tethered` | 连续拍摄模式 |
| `gphoto2 --capture-image-and-download` | 拍摄并下载 |
| `gphoto2 --list-files` | 列出相机上的文件 |
| `gphoto2 --get-all-files` | 下载所有文件 |

### 联机拍摄设置

| 步骤 | 操作 |
|------|------|
| 1 | 通过 USB 连接相机 |
| 2 | 设置相机为联机模式 |
| 3 | 安装 gPhoto2：`sudo apt install gphoto2` |
| 4 | 测试连接：`gphoto2 --auto-detect` |
| 5 | 开始联机拍摄：`gphoto2 --capture-tethered` |

---

## 数字资产管理（DAM）

DAM 系统组织、编目和管理大型照片库。

### 开源 DAM 工具

| 工具 | 类型 | 平台 | 许可证 | 核心功能 |
|------|------|------|--------|----------|
| digiKam | 完整 DAM | 全平台 | GPL | 全面功能 |
| PhotoPrism | Web DAM | 全平台 | AGPL | AI 驱动的组织 |
| Lychee | Web 画廊 | 全平台 | MIT | 简洁优雅 |
| Piwigo | Web 画廊 | 全平台 | GPL | 插件生态 |
| LibrePhotos | Web DAM | 全平台 | MIT | AI 人脸识别 |

### digiKam 功能

| 功能 | 描述 |
|------|------|
| 导入 | 相机、扫描仪、文件系统 |
| 组织 | 标签、评分、标签、相册 |
| 搜索 | 元数据、相似性、时间线 |
| RAW 处理 | 内置 RAW 显影器 |
| 编辑 | 非破坏性编辑 |
| 人脸检测 | 自动人脸识别 |
| 地理位置 | 地图集成、GPS 轨迹 |
| 导出 | Web、邮件、打印、社交媒体 |

### 组织照片库

| 方法 | 描述 | 最佳用途 |
|------|------|----------|
| 基于日期 | YYYY/MM/DD 文件夹 | 按时间浏览 |
| 基于事件 | 每个事件命名文件夹 | 快速访问 |
| 基于项目 | 客户或项目文件夹 | 专业工作 |
| 混合 | 日期 + 标签 + 相册 | 最大灵活性 |

### 标签策略

| 层级 | 示例 | 用途 |
|------|------|------|
| 类别 | 自然、建筑、人物 | 大类分组 |
| 主题 | 山、河、建筑 | 具体主题 |
| 位置 | 国家、城市、地点 | 地理 |
| 质量 | 精选、候选、淘汰 | 筛选 |
| 工作流 | 待处理、已处理、已导出 | 状态跟踪 |

---

## 工作流建议

完整的开源摄影工作流。

### 工作流 1：基础（入门）

| 步骤 | 工具 | 操作 |
|------|------|------|
| 导入 | 文件管理器 | 从相机复制 |
| 浏览 | digiKam | 查看和评分 |
| 编辑 | GIMP | 基础调整 |
| 导出 | GIMP | 保存为 JPEG |
| 分享 | Web | 上传到画廊 |

### 工作流 2：进阶

| 步骤 | 工具 | 操作 |
|------|------|------|
| 导入 | digiKam | 导入并打标签 |
| 筛选 | digiKam | 评分和淘汰 |
| RAW 显影 | darktable | 处理 RAW 文件 |
| 修图 | GIMP | 详细编辑 |
| 编目 | digiKam | 组织和打标签 |
| 导出 | darktable | 导出用于 Web/打印 |

### 工作流 3：专业

| 步骤 | 工具 | 操作 |
|------|------|------|
| 联机 | gPhoto2/Entangle | 拍摄到电脑 |
| 导入 | digiKam | 带元数据导入 |
| 筛选 | digiKam | 评分、标签、淘汰 |
| RAW 显影 | darktable | 非破坏性处理 |
| 批处理 | darktable | 对系列应用样式 |
| 修图 | GIMP | 详细修图 |
| HDR/全景 | Luminance HDR/Hugin | 特殊处理 |
| 色彩校对 | DisplayCAL | 验证颜色准确性 |
| 导出 | darktable | 多种输出尺寸 |
| 归档 | digiKam + 备份 | 长期存储 |

### 软件安装（Ubuntu/Debian）

```bash
# 核心工具
sudo apt install gimp darktable rawtherapee digikam

# 全景和 HDR
sudo apt install hugin luminance-hdr enblend enfuse

# 联机拍摄
sudo apt install gphoto2 entangle

# 元数据
sudo apt install exiftool exiv2

# 色彩管理
sudo apt install displaycal argyll
```

---

## 总结

开源摄影工具提供完整的、专业级的工作流，无需订阅费用。关键要点：

- **darktable + GIMP** 是最流行的开源摄影工作流
- **digiKam** 提供全面的数字资产管理
- **色彩管理** 对一致的输出至关重要
- **非破坏性编辑** 保留你的原始文件
- **元数据** 让你的库可搜索和有组织
- **备份** 用 3-2-1 法则保护你的工作
- **循序渐进**：从基础工具开始，按需增加复杂性


---

## 来源：photores.md

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


---

## 来源：raw.md

## 简介

RawTherapee 是一款免费开源的 RAW 照片处理应用程序。它提供高级工具来开发 RAW 图像，具有非破坏性编辑、专业色彩管理和广泛的校正功能。

## 目录

1. [支持的格式](#支持的格式)
2. [安装](#安装)
3. [界面概览](#界面概览)
4. [曝光与色调](#曝光与色调)
5. [色彩管理](#色彩管理)
6. [细节与降噪](#细节与降噪)
7. [镜头校正](#镜头校正)
8. [批处理](#批处理)

## 支持的格式

### RAW 相机格式

| 制造商 | 格式 | 支持级别 |
|--------|------|----------|
| Canon | CR2, CR3 | 完全 |
| Nikon | NEF, NRW | 完全 |
| Sony | ARW, SR2 | 完全 |
| Fujifilm | RAF | 完全 |
| Olympus | ORF | 完全 |
| Panasonic | RW2 | 完全 |
| Pentax | PEF, DNG | 完全 |
| Adobe | DNG | 完全 |

### 输出格式

| 格式 | 位深 | 质量 | 使用场景 |
|------|------|------|----------|
| TIFF | 8/16/32 位 | 无损 | 打印、编辑 |
| JPEG | 8 位 | 有损 | Web、分享 |
| PNG | 8/16 位 | 无损 | Web、透明度 |

## 安装

### 平台支持

| 平台 | 方式 | 包 |
|------|------|-----|
| Windows | 安装程序 | 网站下载 .exe |
| macOS | DMG | 网站下载 .dmg |
| Linux | 包管理器 | apt, dnf, snap |
| Flatpak | 通用 | flathub |
| 源码 | 编译 | git + cmake |

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 双核 | 四核+ |
| 内存 | 4 GB | 8 GB+ |
| GPU | OpenGL 2.0 | 现代 GPU |
| 显示 | 1280x720 | 1920x1080+ |
| 存储 | 200 MB | 1 GB+ |

## 界面概览

### 主要面板

| 面板 | 位置 | 用途 |
|------|------|------|
| 文件浏览器 | 左侧 | 浏览和组织 |
| 编辑器 | 中央 | 图像编辑 |
| 历史 | 右侧 | 编辑步骤 |
| 处理配置文件 | 右侧 | 预设管理 |
| 导航器 | 右上 | 缩放预览 |
| 直方图 | 右上 | 色调信息 |

### 标签组织

| 标签 | 工具 |
|------|------|
| 曝光 | 亮度、对比度、色调曲线 |
| 细节 | 锐化、降噪 |
| 颜色 | 白平衡、HSV、色彩调色 |
| 变换 | 旋转、裁剪、调整大小 |
| RAW | 去马赛克、色差 |
| 元数据 | EXIF 信息 |

## 曝光与色调

### 曝光工具

| 工具 | 用途 | 范围 |
|------|------|------|
| 曝光补偿 | 整体亮度 | -5 到 +5 EV |
| 高光压缩 | 恢复高光 | 0-100 |
| 阴影压缩 | 提亮阴影 | 0-100 |
| 亮度 | 中间调调整 | -100 到 +100 |
| 对比度 | 色调范围 | -100 到 +100 |

### 色调曲线

| 类型 | 控制 | 使用场景 |
|------|------|----------|
| 参数化 | 区域滑块 | 快速调整 |
| 控制点 | 自定义曲线 | 精确控制 |
| 胶片风格 | S 曲线 | 经典外观 |
| 线性 | 直线 | 无调整 |

### 动态范围压缩

| 设置 | 说明 | 效果 |
|------|------|------|
| 高光压缩 | 减少亮区 | 保留高光细节 |
| 阴影提亮 | 亮化暗区 | 显示阴影细节 |
| 微对比度 | 局部对比度 | 纹理增强 |

### 直方图

| 元素 | 说明 |
|------|------|
| 红色通道 | 红色分布 |
| 绿色通道 | 绿色分布 |
| 蓝色通道 | 蓝色分布 |
| 亮度 | 整体亮度 |
| 裁剪指示器 | 过曝/欠曝区域 |

## 色彩管理

### 白平衡

| 方法 | 说明 | 使用场景 |
|------|------|----------|
| 相机 | 按拍摄设置 | 起点 |
| 自动 | 自动 | 快速修复 |
| 自定义 | 色温/色调 | 精确控制 |
| 取样 | 取样灰区 | 准确 |

### 白平衡预设

| 预设 | 色温 | 典型用途 |
|------|------|----------|
| 日光 | 5500K | 户外阳光 |
| 阴天 | 6500K | 多云天空 |
| 阴影 | 7500K | 开放阴影 |
| 钨丝灯 | 2850K | 室内白炽灯 |
| 荧光灯 | 4000K | 办公照明 |
| 闪光灯 | 5500K | 闪光灯 |

### HSV/HSB 调整

| 通道 | 色相 | 饱和度 | 亮度 |
|------|------|--------|------|
| 红色 | 偏移色相 | 强度 | 亮度 |
| 橙色 | 偏移色相 | 强度 | 亮度 |
| 黄色 | 偏移色相 | 强度 | 亮度 |
| 绿色 | 偏移色相 | 强度 | 亮度 |
| 青色 | 偏移色相 | 强度 | 亮度 |
| 蓝色 | 偏移色相 | 强度 | 亮度 |
| 紫色 | 偏移色相 | 强度 | 亮度 |
| 品红 | 偏移色相 | 强度 | 亮度 |

### 色彩调色

| 方法 | 说明 |
|------|------|
| 色彩平衡 | 阴影/中间调/高光 |
| 分色调 | 双色调色 |
| 胶片模拟 | 模拟胶片风格 |

## 细节与降噪

### 锐化

| 工具 | 说明 | 参数 |
|------|------|------|
| USM 锐化 | 标准锐化 | 半径、数量、阈值 |
| 反卷积 | 边缘恢复 | 半径、迭代 |
| 微对比度 | 局部细节 | 强度 |
| 捕获锐化 | RAW 专用 | 反卷积 |

### 降噪

| 类型 | 工具 | 参数 |
|------|------|------|
| 亮度 | NR 滑块 | 数量、细节 |
| 色度 | NR 滑块 | 数量 |
| 脉冲 | 椒盐噪声 | 阈值 |
| 边缘感知 | 保留边缘 | 阈值 |

### 降噪策略

| ISO 级别 | 亮度 NR | 色度 NR |
|----------|---------|---------|
| 100-400 | 0-10 | 0-15 |
| 400-1600 | 10-30 | 15-40 |
| 1600-6400 | 30-60 | 40-70 |
| 6400+ | 60-100 | 70-100 |

### 色差

| 类型 | 说明 | 校正 |
|------|------|------|
| 红/青 | 色彩边缘 | 自动或手动 |
| 蓝/黄 | 色彩边缘 | 自动或手动 |
| 紫边 | 高光边缘 | 去紫边工具 |

## 镜头校正

### 畸变校正

| 方法 | 说明 |
|------|------|
| 自动 | 基于镜头配置文件 |
| 手动 | 畸变滑块 |
| 配置文件 | Lensfun 数据库 |

### 暗角校正

| 设置 | 说明 | 范围 |
|------|------|------|
| 数量 | 校正强度 | 0-200 |
| 半径 | 影响区域 | 0-100 |
| 强度 | 强度 | -100 到 +100 |

### 镜头配置文件

| 来源 | 覆盖 | 更新 |
|------|------|------|
| 内置 | 常见镜头 | 随更新 |
| Lensfun | 社区数据库 | 持续 |
| 手动 | 任何镜头 | 用户创建 |

## 批处理

### 队列操作

| 操作 | 方法 |
|------|------|
| 添加到队列 | 选择图像 > 队列 |
| 处理队列 | 点击处理 |
| 清除队列 | 右键 > 清除 |

### 处理配置文件

| 配置文件 | 说明 | 扩展名 |
|----------|------|--------|
| 部分 | 选定设置 | .pp3 |
| 完整 | 所有设置 | .pp3 |
| 默认 | 内置预设 | .pp3 |

### 配置文件应用

| 模式 | 说明 |
|------|------|
| 复制/粘贴 | 在图像间传递设置 |
| 应用 | 应用保存的配置文件 |
| 自动 | 应用到所有选定 |

### 批处理设置

| 设置 | 选项 |
|------|------|
| 输出文件夹 | 相同、自定义、子文件夹 |
| 文件名 | 原始、自定义模式 |
| 格式 | TIFF, JPEG, PNG |
| 质量 | 压缩级别 |
| 调整大小 | 尺寸或百分比 |

## 高级功能

### 去马赛克算法

| 算法 | 质量 | 速度 | 最佳用途 |
|------|------|------|----------|
| Amaze | 高 | 中等 | 大多数图像 |
| IGV | 高 | 中等 | 高 ISO |
| DCB | 中等 | 快 | 通用 |
| 无 | 预览 | 最快 | 快速预览 |

### 色彩管理

| 设置 | 说明 |
|------|------|
| 工作色彩空间 | 编辑空间（ProPhoto, Adobe RGB） |
| 输出配置文件 | 导出色彩空间 |
| 显示器配置文件 | 显示校准 |
| 渲染意图 | 色彩映射方法 |

### CIECAM02

| 功能 | 说明 |
|------|------|
| 色彩外观 | 感知色彩模型 |
| 亮度 | 感知亮度 |
| 色度 | 色彩丰富度 |
| 色相 | 色彩角度 |

## 键盘快捷键

| 快捷键 | 操作 |
|--------|------|
| F | 适合窗口 |
| Z | 缩放到 100% |
| B | 前后对比 |
| Ctrl+Z | 撤销 |
| Ctrl+Y | 重做 |
| Tab | 切换面板 |

## 导出设置

### JPEG 导出

| 设置 | 说明 | 推荐 |
|------|------|------|
| 质量 | 压缩 | 90-95% |
| 子采样 | 色度子采样 | 4:4:4（质量） |
| EXIF | 元数据包含 | 按需 |
| 大小 | 输出尺寸 | 原始或自定义 |

### TIFF 导出

| 设置 | 说明 | 推荐 |
|------|------|------|
| 位深 | 色彩精度 | 16 位 |
| 压缩 | 文件压缩 | LZW |
| 色彩空间 | 输出配置文件 | Adobe RGB |

## 总结

RawTherapee 提供专业级的 RAW 照片处理能力，具有非破坏性编辑、高级色彩管理和广泛的校正工具。它对众多相机格式和镜头配置文件的支持使其成为商业 RAW 处理器的全面替代方案。


---

## 来源：photography.md

## The Exposure Triangle

Every photograph is controlled by three interrelated settings. Understanding how they work together is the foundation of photography.

### Aperture

Aperture is the size of the opening in the lens that lets light through, measured in f-stops.

| f-stop | Opening | Light | Depth of Field | Use Case |
|--------|---------|-------|----------------|----------|
| f/1.4 - f/2.8 | Wide | Lots | Very shallow | Portraits, low light |
| f/4 - f/5.6 | Medium | Moderate | Moderate | General purpose |
| f/8 - f/11 | Narrow | Less | Deep | Landscapes, architecture |
| f/16 - f/22 | Very narrow | Little | Very deep | Maximum sharpness, starbursts |

A lower f-number means a wider aperture, more light, and a shallower depth of field (blurry background). A higher f-number means a narrower aperture, less light, and more of the scene in focus.

### Shutter Speed

Shutter speed controls how long the sensor is exposed to light.

| Speed | Effect | Use Case |
|-------|--------|----------|
| 1/1000s - 1/4000s | Freezes motion | Sports, birds in flight |
| 1/125s - 1/500s | Sharp handheld | General, street photography |
| 1/30s - 1/60s | Motion blur risk | Needs steady hands or IS |
| 1s - 30s | Intentional blur | Waterfalls, light trails |
| 30s+ (Bulb) | Long exposure | Night sky, star trails |

As a general rule, your shutter speed should be at least 1/(focal length) to avoid camera shake when handheld. For a 50mm lens, use at least 1/50s.

### ISO

ISO measures sensor sensitivity to light.

| ISO | Noise Level | When to Use |
|-----|-------------|-------------|
| 100-200 | Minimal | Bright daylight, tripod work |
| 400-800 | Low | Overcast days, shade |
| 1600-3200 | Noticeable | Indoor, evening |
| 6400+ | Significant | Night, extreme low light |

Keep ISO as low as possible. Only raise it when you cannot widen aperture or slow shutter speed further.

## Composition Rules

### Rule of Thirds

Divide the frame into a 3x3 grid. Place key subjects along the gridlines or at the four intersection points. Most cameras have a grid overlay option. This creates more dynamic, visually interesting images than centering the subject.

### Leading Lines

Use natural lines in the scene -- roads, rivers, fences, railways, shorelines -- to guide the viewer's eye toward the main subject or deeper into the frame. Diagonal lines add energy; curved lines add elegance.

### Symmetry and Patterns

Symmetrical scenes create a sense of order and calm. Reflections in water, architectural facades, and rows of objects are strong subjects. Breaking a pattern with a single contrasting element creates a powerful focal point.

### Framing

Use natural elements -- doorways, arches, tree branches, windows -- to create a frame within the frame. This draws attention to the subject and adds depth.

### Negative Space

Leaving large areas of empty or simple space around a small subject emphasizes isolation, scale, or importance. This technique works especially well with minimalist compositions.

## Lighting Techniques

### Natural Light

| Time of Day | Quality | Color | Best For |
|-------------|---------|-------|----------|
| Golden hour (sunrise/sunset) | Soft, warm | Orange/amber | Portraits, landscapes |
| Blue hour (just before sunrise/after sunset) | Even, cool | Blue/purple | Cityscapes, moody scenes |
| Midday sun | Harsh, direct | Neutral white | High contrast, shadows |
| Overcast | Soft, diffused | Cool neutral | Portraits, macro |

### Artificial Light

- **On-camera flash**: Avoid direct flash -- it creates harsh shadows. Bounce off ceilings or walls when possible.
- **Off-camera flash**: Gives control over direction and quality. Use a wireless trigger.
- **Continuous LED panels**: Useful for video and for beginners learning light placement.
- **Reflectors**: A simple white or silver reflector fills shadows in portrait work.

## Common Genres

### Portrait Photography

Focus on the eyes -- they should be the sharpest point. Use a wide aperture (f/1.8-f/2.8) for background blur. Position the subject slightly off-center. Natural window light is one of the most flattering light sources.

### Landscape Photography

Use a tripod. Shoot at f/8-f/11 for front-to-back sharpness. Include foreground interest to add depth. The golden hour produces the most dramatic light. Use a graduated ND filter to balance bright skies with darker foregrounds.

### Street Photography

Use a moderate focal length (35mm or 50mm equivalent). Shoot in aperture priority mode at f/5.6-f/8 for zone focusing. Be aware of light and shadow patterns. Anticipate moments rather than react to them.

### Macro Photography

A dedicated macro lens (or extension tubes for a budget option) allows close focusing. Depth of field becomes extremely thin at close range -- use f/8-f/16. A tripod or flash is often necessary. Wind is the enemy of outdoor macro work.

## Post-Processing Basics

Post-processing is a normal part of digital photography. The goal is to realize the image you envisioned, not to fabricate something that was not there.

### Key Adjustments

1. **Exposure**: Correct overall brightness.
2. **White balance**: Adjust color temperature to match the scene or your intent.
3. **Contrast**: Increase separation between lights and darks.
4. **Highlights/Shadows**: Recover detail in bright and dark areas separately.
5. **Clarity/Texture**: Enhance midtone contrast for perceived sharpness.
6. **Vibrance/Saturation**: Adjust color intensity. Vibrance is more subtle and protects skin tones.
7. **Crop and straighten**: Refine composition after the shot.
8. **Sharpening**: Apply as the final step, tailored to output medium (screen vs. print).

### Shoot RAW

RAW files retain all sensor data, giving you far more flexibility in post-processing than JPEGs. Storage is cheap; lost detail is not.

## Recommended Free Tools

| Tool | Platform | Strengths |
|------|----------|-----------|
| darktable | Windows/Mac/Linux | Full RAW editor, non-destructive workflow |
| RawTherapee | Windows/Mac/Linux | Powerful RAW processing, detailed controls |
| GIMP | Windows/Mac/Linux | Pixel editor, layers, masking |
| Snapseed | Android/iOS | Mobile editing, intuitive interface |
| digiKam | Windows/Mac/Linux | Photo management and editing |
| Photopea | Browser | Photoshop-like interface, no install |

## Getting Started Checklist

1. Learn to shoot in aperture priority mode (Av/A) -- it handles most situations well.
2. Review every image and ask what you would change.
3. Study light before studying gear.
4. Shoot one subject in many ways rather than many subjects once.
5. Look at the work of photographers you admire and analyze why their images work.


---

## 来源：photo.md

## 简介

Darktable 是一个开源的摄影工作流程应用和 RAW 处理器。它提供了虚拟灯桌和暗房来管理和编辑照片。本教程涵盖界面、编辑工作流程、模块和实用技巧。

## 界面概览

### 主要视图

| 视图 | 用途 | 核心功能 |
|------|------|----------|
| Lighttable | 图片管理 | 导入、评分、标记、导出 |
| Darkroom | 图片编辑 | 模块、调整、蒙版 |
| Tethering | 相机控制 | 实时取景、拍摄 |
| Map | 地理标记 | 基于 GPS 的组织 |
| Print | 打印布局 | 纸张大小、边距 |
| Slideshow | 演示 | 全屏查看 |

### Lighttable 布局

```
+------------------+------------------+
| 导入面板         | 图片网格         |
| - 文件夹         | - 缩略图         |
| - 收藏           | - 评分           |
| - 标签           | - 颜色标签       |
+------------------+------------------+
| 选中图片信息                         |
| - EXIF、元数据、直方图              |
+--------------------------------------+
```

## 导入照片

### 导入方式

| 方式 | 描述 | 使用场景 |
|------|------|----------|
| 导入文件夹 | 添加图片目录 | 批量导入 |
| 导入图片 | 添加单个文件 | 选择性导入 |
| 相机 | 连线或存储卡导入 | 直接从相机 |
| 胶卷卷 | 添加现有目录 | 重新链接图片 |

### 支持格式

| 格式 | 类型 | 支持级别 |
|------|------|----------|
| RAW | 相机特定 | 完全 |
| JPEG | 标准 | 完全 |
| TIFF | 高质量 | 完全 |
| PNG | Web 格式 | 完全 |
| DNG | Adobe RAW | 完全 |
| HEIF | 现代格式 | 部分 |

## 基本编辑工作流程

### 步骤 1：导入和选择

1. 在 lighttable 中点击"Import"。
2. 选择要导入的文件夹或文件。
3. 查看缩略图并应用评分（1-5 星）。
4. 使用颜色标签进行分类。

### 步骤 2：进入 Darkroom

双击图片进入 darkroom 视图。

### 步骤 3：应用模块

模块按流水线顺序应用。

| 阶段 | 模块 | 用途 |
|------|------|------|
| 输入 | Input profile | 色彩空间转换 |
| 白平衡 | Temperature、tint | 颜色校正 |
| 曝光 | Exposure、highlights、shadows | 亮度调整 |
| 颜色 | Color balance、saturation | 色彩分级 |
| 色调 | Tone curve、levels | 对比度和色调 |
| 细节 | Sharpen、denoise | 锐度和噪点 |
| 效果 | Vignette、grain | 创意效果 |
| 输出 | Output profile | 最终色彩空间 |

### 步骤 4：导出

1. 返回 lighttable。
2. 选择已编辑的图片。
3. 点击"Export"。
4. 选择格式、质量和目标。

## 核心模块

### 曝光模块

| 滑块 | 效果 | 范围 |
|------|------|------|
| Exposure | 整体亮度 | -5 到 +5 EV |
| Highlights | 亮部恢复 | -100 到 +100 |
| Shadows | 暗部提升 | -100 到 +100 |
| Blacks | 最暗色调 | -100 到 +100 |
| Whites | 最亮色调 | -100 到 +100 |

### 白平衡模块

| 滑块 | 效果 | 用途 |
|------|------|------|
| Temperature | 暖/冷 | 校正色偏 |
| Tint | 绿/品红 | 微调平衡 |
| Preset | 相机预设 | 拍摄时、日光等 |

### 色调曲线模块

```
输出
  |        ___
  |      /
  |    /
  |  /
  | /
  |/___________ 输入
```

| 操作 | 曲线形状 | 效果 |
|------|----------|------|
| 增加对比度 | S 曲线 | 更多对比度 |
| 提升暗部 | 左侧抬高 | 更亮的黑色 |
| 压缩亮部 | 右侧降低 | 减少过曝 |
| 平坦效果 | 平坦曲线 | 降低对比度 |

### 色彩平衡模块

| 区域 | 调整 | 用途 |
|------|------|------|
| Shadows | 暗部颜色 | 色彩分级 |
| Midtones | 中间调颜色 | 整体色调 |
| Highlights | 亮部颜色 | 高光着色 |
| Power | 暗部饱和度 | 胶片模拟 |

### 锐化模块

| 滑块 | 效果 | 默认值 |
|------|------|--------|
| Radius | 锐化区域 | 2.0 |
| Amount | 强度 | 0.5 |
| Threshold | 边缘检测 | 0.5 |

### 降噪模块

| 模块 | 用途 | 使用场景 |
|------|------|----------|
| Denoise (profiled) | 相机特定降噪 | 高 ISO 图片 |
| Denoise (non-local means) | 通用降噪 | 中等噪点 |
| Denoise (bilateral) | 保边平滑 | 轻微噪点 |

## 蒙版

### 蒙版类型

| 类型 | 描述 | 使用场景 |
|------|------|----------|
| Drawn | 基于形状的蒙版 | 选择性区域编辑 |
| Parametric | 基于亮度/颜色 | 色调调整 |
| Combined | Drawn + Parametric | 复杂选择 |

### 绘制蒙版形状

| 形状 | 工具 | 应用 |
|------|------|------|
| Circle | 拖拽创建 | 通用区域 |
| Ellipse | 拖拽创建 | 椭圆选择 |
| Path | 点击定义点 | 自定义形状 |
| Brush | 绘制定义 | 自由选择 |
| Gradient | 拖拽创建 | 渐变过渡 |

### 蒙版属性

| 属性 | 效果 |
|------|------|
| Opacity | 蒙版效果强度 |
| Feathering | 边缘柔和度 |
| Size | 区域覆盖 |
| Rotation | 蒙版方向 |

## 局部调整

### 使用混合模式

| 混合模式 | 效果 | 使用场景 |
|----------|------|----------|
| Normal | 直接应用模块 | 默认 |
| Lighten | 变亮效果 | 恢复高光 |
| Darken | 变暗效果 | 增加深度 |
| Overlay | 对比度增强 | 局部对比度 |
| Soft Light | 柔和对比 | 微妙调整 |

### 示例：选择性提亮

1. 添加一个 Exposure 模块实例。
2. 增加曝光（+1.0 EV）。
3. 在主体上创建绘制蒙版。
4. 羽化蒙版边缘。
5. 按需调整不透明度。

## 样式

### 应用样式

| 样式 | 描述 | 应用 |
|------|------|------|
| 内置 | 预定义效果 | 一键应用 |
| 自定义 | 用户创建的样式 | 一致编辑 |
| 预设 | 模块设置 | 快速调整 |

### 创建自定义样式

1. 将图片编辑到所需效果。
2. 在历史面板中点击"Create a style"。
3. 选择要包含的模块。
4. 命名样式。
5. 应用到其他图片。

## 连线拍摄

### 连线拍摄功能

| 功能 | 描述 |
|------|------|
| 实时取景 | 实时相机显示 |
| 拍摄 | 从电脑触发快门 |
| 导入 | 自动导入拍摄的图片 |
| 标记 | 自动应用标签和元数据 |

### 相机支持

| 品牌 | 协议 | 支持 |
|------|------|------|
| Canon | PTP | 良好 |
| Nikon | PTP | 良好 |
| Sony | PTP | 有限 |
| Fuji | PTP | 有限 |

## 地理标记

### 地图模块

| 功能 | 描述 |
|------|------|
| GPS 轨迹导入 | 导入 GPX 文件 |
| 自动地理标记 | 匹配时间戳到轨迹 |
| 手动放置 | 拖拽图片到地图 |
| 位置搜索 | 搜索地点 |

### GPX 工作流程

1. 在拍照期间记录 GPS 轨迹。
2. 从 GPS 设备导出 GPX 文件。
3. 将 GPX 导入 darktable。
4. Darktable 将照片时间戳匹配到 GPS 点。

## 导出设置

### 导出选项

| 设置 | 描述 | 建议 |
|------|------|------|
| Format | 输出文件类型 | JPEG、TIFF、PNG |
| Quality | 压缩级别 | JPEG 用 90-95% |
| Dimensions | 调整输出大小 | 原始或自定义 |
| Profile | 色彩空间 | Web 用 sRGB，打印用 AdobeRGB |
| Sharpen | 输出锐化 | 用于屏幕或打印 |

### 导出预设

| 预设 | 格式 | 质量 | 大小 | 用途 |
|------|------|------|------|------|
| Web | JPEG | 90% | 2048px | 在线分享 |
| Print | TIFF | 100% | 原始分辨率 | 打印 |
| Archive | DNG | 100% | 原始 | 长期存储 |
| Social | JPEG | 85% | 1080px | 社交媒体 |

## 键盘快捷键

### 导航

| 按键 | 操作 |
|------|------|
| `L` | 切换 lighttable/darkroom |
| `F` | 全屏 |
| `Tab` | 切换面板 |
| `Space` | 下一张图片 |
| `Backspace` | 上一张图片 |

### 编辑

| 按键 | 操作 |
|------|------|
| `E` | 曝光模块 |
| `W` | 白平衡 |
| `T` | 色调曲线 |
| `B` | 切换模块开/关 |
| `Ctrl+Z` | 撤销 |
| `Ctrl+Shift+Z` | 重做 |

### 评分

| 按键 | 操作 |
|------|------|
| `1-5` | 设置星级 |
| `R` | 切换拒绝标记 |
| `F1-F5` | 颜色标签 |

## 性能技巧

| 技巧 | 描述 |
|------|------|
| 使用 mipmap 缓存 | 预生成缩略图 |
| 启用 OpenCL | 模块 GPU 加速 |
| 磁盘缓存 | 数据库用快速 SSD |
| 禁用未使用模块 | 减少处理负载 |

### 启用 OpenCL

1. 前往 Settings > Processing。
2. 启用"Activate OpenCL support"。
3. 选择你的 GPU 设备。

## 数据库管理

### 图库数据库

| 操作 | 命令 | 用途 |
|------|------|------|
| 备份 | 复制 `library.db` | 保护目录 |
| 优化 | Settings > Maintenance | 清理数据库 |
| 迁移 | 导出/导入 | 移到新系统 |

## 总结

Darktable 提供了专业级的 RAW 照片编辑，具有基于模块的处理流水线。将照片导入 lighttable，在 darkroom 中使用曝光、颜色、色调和细节模块进行编辑，然后导出用于 Web 或打印。蒙版系统实现了精确的局部调整，样式允许在收藏中保持一致的编辑。


---
