# SteamGridDB 游戏封面教程

## 简介

SteamGridDB 是一个自定义游戏封面的数据库和社区，包括横幅、海报、Logo 和图标。它主要用于自定义 Steam、Playnite 和 GOG Galaxy 等启动器中游戏库的视觉外观。

| 特性 | 描述 |
|---------|-------------|
| 封面数据库 | 大量的自定义游戏封面收藏 |
| 多种格式 | 横幅、海报、Logo、Hero 和图标 |
| 社区贡献 | 用户上传的封面，带有质量评分 |
| API 访问 | 通过 API 编程式访问封面数据库 |
| 启动器集成 | 与 Steam、Playnite、GOG Galaxy 等配合使用 |

## 封面类型

### Steam 封面分类

| 分类 | 尺寸 | 使用场景 |
|----------|-----------|----------|
| Grid (横向) | 460x215 | 库网格视图横幅 |
| Grid (纵向) | 342x482 | 库网格视图海报 |
| Hero | 1920x620 | 库页面背景 |
| Logo | 可变 | Hero 上的游戏 Logo 叠加 |
| Icon | 可变 | 小型游戏图标 |

### 封面尺寸

| 类型 | 宽度 | 高度 | 宽高比 |
|------|-------|--------|-------------|
| 横向 Grid | 460 | 215 | ~2.14:1 |
| 纵向 Grid | 342 | 482 | ~0.71:1 |
| Hero | 1920 | 620 | ~3.1:1 |
| Logo | 可变 | 可变 | 透明 PNG |
| Icon | 256 | 256 | 1:1 |

## 使用 SteamGridDB

### Web 界面

| 区域 | 描述 |
|---------|-------------|
| 搜索 | 按标题查找游戏 |
| 游戏页面 | 查看特定游戏的所有封面 |
| 上传 | 向数据库提交新封面 |
| 评分 | 对封面质量进行评分（1-5 星） |
| 筛选器 | 按风格、尺寸和类型筛选 |

### 搜索封面

| 步骤 | 操作 |
|------|--------|
| 1 | 访问 SteamGridDB 网站 |
| 2 | 在搜索栏中输入游戏标题 |
| 3 | 从结果中选择游戏 |
| 4 | 选择封面类型（Grid、Hero、Logo、Icon） |
| 5 | 浏览可用的封面选项 |
| 6 | 下载首选封面 |

## API 访问

### API 概述

| 特性 | 描述 |
|---------|-------------|
| Base URL | https://www.steamgriddb.com/api/v2 |
| 认证 | 需要 API 密钥（从账户设置中获取） |
| 速率限制 | 基于账户类型的请求限制 |
| 格式 | JSON 响应 |

### API 端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/games/steam/{appid}` | GET | 通过 Steam App ID 获取游戏 |
| `/games/name/{name}` | GET | 按名称搜索游戏 |
| `/grids/game/{id}` | GET | 获取游戏的 Grid 封面 |
| `/heroes/game/{id}` | GET | 获取游戏的 Hero 封面 |
| `/logos/game/{id}` | GET | 获取游戏的 Logo |
| `/icons/game/{id}` | GET | 获取游戏的 Icon |

### API 认证

```bash
# 在请求头中使用 API 密钥
curl -H "Authorization: Bearer YOUR_API_KEY" \
  https://www.steamgriddb.com/api/v2/games/steam/730
```

### 示例：获取游戏封面

```python
import requests

API_KEY = "your_api_key"
BASE_URL = "https://www.steamgriddb.com/api/v2"

headers = {"Authorization": f"Bearer {API_KEY}"}

# 搜索游戏
response = requests.get(f"{BASE_URL}/games/name/Half-Life", headers=headers)
games = response.json()["data"]

# 获取第一个结果的 Grid 封面
game_id = games[0]["id"]
grids = requests.get(f"{BASE_URL}/grids/game/{game_id}", headers=headers)

for grid in grids.json()["data"]:
    print(grid["url"], grid["width"], grid["height"])
```

## Steam 集成

### 自定义 Steam 游戏库

| 步骤 | 操作 |
|------|--------|
| 1 | 在 SteamGridDB 上找到封面 |
| 2 | 下载所需的图片 |
| 3 | 打开 Steam 并进入游戏库 |
| 4 | 右键点击游戏 |
| 5 | 选择管理 > 设置自定义封面 |
| 6 | 选择下载的图片 |

### Steam 封面类型

| Steam 设置 | 封面类型 | 显示位置 |
|--------------|-------------|------------------|
| Capsule | 横向 Grid | 库网格视图 |
| Vertical Capsule | 纵向 Grid | 库网格视图（新版） |
| Hero | Hero | 游戏详情页背景 |
| Logo | Logo | 叠加在 Hero 上 |
| Icon | Icon | 游戏列表和桌面 |

## Playnite 集成

### 自动封面下载

Playnite 可以自动从 SteamGridDB 获取封面。

| 步骤 | 操作 |
|------|--------|
| 1 | 为 Playnite 安装 SteamGridDB 插件 |
| 2 | 在插件设置中配置 API 密钥 |
| 3 | 选择要更新的游戏 |
| 4 | 运行所选游戏的封面下载 |

### 插件配置

| 设置 | 描述 |
|---------|-------------|
| API 密钥 | SteamGridDB API 认证密钥 |
| 封面类型 | 选择要下载的类型（Grid、Hero、Logo、Icon） |
| 风格偏好 | 偏好官方或自定义封面 |
| 尺寸 | 首选图片尺寸 |
| 覆盖 | 是否替换现有封面 |

## 上传封面

### 封面指南

| 指南 | 描述 |
|-----------|-------------|
| 质量 | 高分辨率，无压缩伪影 |
| 准确性 | 正确的游戏，无错误归属的封面 |
| 格式 | 透明图推荐 PNG，JPG 可接受 |
| 尺寸 | 遵循封面类型的标准尺寸 |
| 原创性 | 尽可能注明原作者 |

### 上传流程

| 步骤 | 操作 |
|------|--------|
| 1 | 创建 SteamGridDB 账户 |
| 2 | 导航到游戏页面 |
| 3 | 选择要上传的封面类型 |
| 4 | 选择图片文件 |
| 5 | 添加标签和风格信息 |
| 6 | 提交审核 |

### 封面风格

| 风格 | 描述 |
|-------|-------------|
| Official | 开发商/发行商提供的封面 |
| Alternate | 粉丝制作的替代设计 |
| Animated | GIF 或 APNG 动画封面 |
| Blurred | 模糊背景版本 |
| White | 简洁的白色/透明设计 |
| Material | Google Material Design 风格 |
| N64 | Nintendo 64 包装盒风格 |
| NSFW | 不适合工作场合的内容 |

## 社区功能

### 评分系统

| 评分 | 含义 |
|--------|---------|
| 5 星 | 优秀质量，完美可用 |
| 4 星 | 良好质量，有小问题 |
| 3 星 | 一般质量，可接受 |
| 2 星 | 低于平均，有明显问题 |
| 1 星 | 质量差，有严重问题 |

### 用户贡献

| 功能 | 描述 |
|---------|-------------|
| 上传封面 | 向数据库提交新封面 |
| 评价现有 | 对封面质量进行评分 |
| 报告问题 | 标记错误或有问题的封面 |
| 请求游戏 | 请求缺失游戏的封面 |

## 工具和实用程序

### 第三方工具

| 工具 | 描述 |
|------|-------------|
| SGDBoop | Steam 一键封面应用 |
| SteamGridDB Manager | 批量封面管理工具 |
| BoilR | 多启动器封面管理器 |

### SGDBoop 使用

| 步骤 | 操作 |
|------|--------|
| 1 | 在系统上安装 SGDBoop |
| 2 | 将其与 steamgriddb:// URL 关联 |
| 3 | 在 SteamGridDB 网站上点击 Boop 按钮 |
| 4 | 封面自动应用到 Steam |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 数据库 | 多种格式的游戏封面大量收藏 |
| 格式 | Grid、Hero、Logo 和 Icon，具有特定尺寸 |
| 集成 | 与 Steam、Playnite、GOG Galaxy 和其他启动器配合使用 |
| API | RESTful API 编程式访问封面 |
| 社区 | 用户上传封面，带评分系统 |
| 工具 | SGDBoop 和 BoilR 实现一键封面应用 |
