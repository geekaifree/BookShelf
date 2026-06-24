# GIMP 教程：图像编辑

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
