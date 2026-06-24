# SteamGridDB：游戏美化管理

## 简介

SteamGridDB 是一个社区驱动的视频游戏美术数据库，为多个平台的游戏提供自定义封面、横幅、图标和标志。它是启动器、前端和游戏工具使用的游戏美术中央仓库。该平台包含用于编程访问的 API，并支持 Steam、GOG、Epic Games、模拟器和非 Steam 游戏的美术资源。

**核心功能：**

- 海量游戏美术数据库
- 自定义美术上传
- 多种美术类型（网格、英雄图、标志、图标）
- 提供 API 用于编程访问
- 支持模拟器和非 Steam 游戏
- 社区贡献
- 管理工具支持批量操作
- 主题支持

---

## 美术类型

### 网格图片

网格图片是 Steam 库视图中显示的主要封面美术：

| 类型 | 尺寸 | 宽高比 | 使用场景 |
|------|------------|--------------|----------|
| 垂直网格 | 600x900 | 2:3 | 库封面美术 |
| 水平网格 | 460x215 | 约 2:1 | 最近/推荐游戏 |
| 高网格 | 342x482 | 约 5:7 | 替代封面 |

### 英雄图片

英雄图片是游戏页面顶部显示的宽横幅：

| 类型 | 尺寸 | 宽高比 | 使用场景 |
|------|------------|--------------|----------|
| 英雄图 | 1920x620 | 约 3:1 | 游戏页面头部 |
| 标志 | 640x360 | 16:9 | 标志叠加区域 |

### 标志图片

标志是透明的游戏标志：

| 类型 | 尺寸 | 使用场景 |
|------|------------|----------|
| 标志 | 640x360 | 游戏页面标志 |
| 白色标志 | 可变 | 深色背景 |
| 黑色标志 | 可变 | 浅色背景 |

### 图标图片

图标是小型游戏图标：

| 类型 | 尺寸 | 使用场景 |
|------|------------|----------|
| 图标 | 256x256 | 任务栏、快捷方式 |
| 图标（小） | 64x64 | 紧凑视图 |

---

## API 使用

### 认证

从 SteamGridDB 获取 API 密钥：

1. 创建 SteamGridDB 账户
2. 导航到账户设置
3. 生成 API 密钥
4. 在请求中使用

### API 基础 URL

```
https://www.steamgriddb.com/api/v2
```

### 认证头部

```
Authorization: Bearer YOUR_API_KEY
```

### 搜索端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/search/autocomplete/{term}` | GET | 自动补全搜索 |
| `/search/grids` | GET | 搜索网格 |
| `/search/heroes` | GET | 搜索英雄图 |
| `/search/logos` | GET | 搜索标志 |
| `/search/icons` | GET | 搜索图标 |

**搜索示例：**

```bash
curl "https://www.steamgriddb.com/api/v2/search/autocomplete/witcher" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### 游戏端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/games/id/{id}` | GET | 按 ID 获取游戏 |
| `/games/platform/{platform}/{id}` | GET | 按平台 ID 获取 |
| `/games/steam/{appid}` | GET | 按 Steam AppID 获取 |

**示例：**

```bash
curl "https://www.steamgriddb.com/api/v2/games/steam/292030" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### 网格端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/grids/game/{id}` | GET | 获取游戏的网格 |
| `/grids/{id}` | GET | 获取特定网格 |

**查询参数：**

| 参数 | 类型 | 描述 |
|-----------|------|-------------|
| `dimensions` | string | 按尺寸筛选 |
| `mimes` | string | 按 MIME 类型筛选 |
| `types` | string | 按类型筛选 |
| `nsfw` | boolean | 包含 NSFW |
| `humor` | boolean | 包含幽默 |
| `page` | integer | 页码 |

**示例：**

```bash
curl "https://www.steamgriddb.com/api/v2/grids/game/591?dimensions=600x900" \
  -H "Authorization: Bearer YOUR_API_KEY"
```

### 英雄图端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/heroes/game/{id}` | GET | 获取游戏的英雄图 |
| `/heroes/{id}` | GET | 获取特定英雄图 |

### 标志端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/logos/game/{id}` | GET | 获取游戏的标志 |
| `/logos/{id}` | GET | 获取特定标志 |

### 图标端点

| 端点 | 方法 | 描述 |
|----------|--------|-------------|
| `/icons/game/{id}` | GET | 获取游戏的图标 |
| `/icons/{id}` | GET | 获取特定图标 |

---

## 自定义美术

### 上传美术

1. 创建 SteamGridDB 账户
2. 导航到游戏页面
3. 点击对应美术类型的"上传"
4. 选择图片文件
5. 添加元数据（尺寸、风格等）
6. 提交审核

### 美术指南

| 指南 | 描述 |
|-----------|-------------|
| 文件格式 | PNG、JPEG、WebP |
| 最大文件大小 | 10 MB |
| 质量 | 高质量，无伪影 |
| 水印 | 不允许 |
| NSFW | 适当标记 |
| 原创性 | 注明原始作者 |

### 美术风格

| 风格 | 描述 |
|-------|-------------|
| 官方 | 开发商/发行商美术 |
| 自定义 | 社区创作美术 |
| 替代 | 替代设计 |
| 模糊 | 模糊背景 |
| 白色 | 亮色主题优化 |
| 暗色 | 暗色主题优化 |

---

## 平台支持

### 支持的平台

| 平台 | 平台 ID | 游戏数 |
|----------|-------------|-------|
| Steam | steam | 50,000+ |
| GOG | gog | 5,000+ |
| Epic Games | egsg | 1,000+ |
| Origin | origin | 1,000+ |
| Uplay | uplay | 500+ |
| Battle.net | battlenet | 100+ |
| Bethesda | bethesda | 50+ |
| EA Desktop | ea | 500+ |
| Riot Games | riotgames | 10+ |
| Oculus | oculus | 100+ |

### 模拟器支持

| 模拟器 | 平台 ID | 系统 |
|----------|-------------|---------|
| RetroArch | retroarch | 多平台 |
| Dolphin | dolphin | GameCube、Wii |
| PCSX2 | ps2 | PlayStation 2 |
| RPCS3 | ps3 | PlayStation 3 |
| Cemu | cemu | Wii U |
| Yuzu | yuzu | Nintendo Switch |
| Ryujinx | ryujinx | Nintendo Switch |
| PPSSPP | psp | PSP |
| DeSmuME | nds | Nintendo DS |
| mGBA | gba | Game Boy Advance |
| Snes9x | snes | SNES |
| mupen64plus | n64 | Nintendo 64 |
| DuckStation | psx | PlayStation 1 |
| Xemu | xbox | Xbox |
| XQEMU | xbox | Xbox |

---

## 管理工具

### SteamGridDB Manager

用于管理游戏美术的桌面应用：

| 功能 | 描述 |
|---------|-------------|
| 自动检测 | 检测已安装游戏 |
| 批量下载 | 为所有游戏下载美术 |
| 自动应用 | 自动应用美术 |
| 自定义美术 | 上传自定义美术 |
| 备份 | 备份当前美术 |

### 安装

```bash
# 从 GitHub releases 下载
# 支持 Windows、macOS、Linux
```

### 配置

| 设置 | 描述 |
|---------|-------------|
| Steam 路径 | Steam 安装路径 |
| API 密钥 | SteamGridDB API 密钥 |
| 自动应用 | 游戏检测时应用美术 |
| 美术类型 | 偏好的美术风格 |

---

## 非 Steam 游戏

### 添加非 Steam 游戏

1. 将游戏作为非 Steam 游戏添加到 Steam
2. 在 SteamGridDB 上找到游戏
3. 下载美术
4. 在 Steam 中应用美术

### 查找美术

| 方法 | 步骤 |
|--------|-------|
| 网站 | 在 steamgriddb.com 搜索 |
| API | 使用搜索 API |
| 管理器 | 自动检测并应用 |

### 常见非 Steam 游戏

| 游戏类型 | 示例 |
|-----------|----------|
| 模拟 | 复古游戏、主机游戏 |
| 无 DRM | GOG 游戏、itch.io 游戏 |
| 其他启动器 | Epic、Origin、Uplay 游戏 |
| 自制 | 自定义游戏、模组 |

---

## 主题

### 使用自定义主题

应用自定义主题改变外观：

| 主题类型 | 描述 |
|------------|-------------|
| 颜色 | 配色方案更改 |
| 布局 | 布局修改 |
| 字体 | 字体更改 |
| 完整 | 完整主题更换 |

### 流行的主题管理器

| 管理器 | 平台 | 功能 |
|---------|----------|----------|
| Millennium | Steam | CSS 主题 |
| SFP | Steam | 皮肤支持 |
| 自定义 CSS | 手动 | 直接 CSS 编辑 |

---

## 批量操作

### 批量下载

为多个游戏下载美术：

**使用 API：**

```python
import requests

API_KEY = "YOUR_API_KEY"
BASE_URL = "https://www.steamgriddb.com/api/v2"

headers = {"Authorization": f"Bearer {API_KEY}"}

# 获取游戏 ID
game_ids = [292030, 1091500, 1245620]

for game_id in game_ids:
    # 获取网格
    response = requests.get(
        f"{BASE_URL}/grids/game/{game_id}",
        headers=headers
    )
    grids = response.json()["data"]
    
    # 下载第一个网格
    if grids:
        grid_url = grids[0]["url"]
        print(f"Downloading grid for game {game_id}")
```

### 批量应用

在 Steam 中为多个游戏应用美术：

1. 打开 SteamGridDB Manager
2. 选择要更新的游戏
3. 选择要应用的美术类型
4. 点击"全部应用"
5. 重启 Steam

---

## 集成

### 第三方工具

| 工具 | 描述 | 平台 |
|------|-------------|----------|
| Playnite | 游戏库管理器 | Windows |
| LaunchBox | 游戏前端 | Windows |
| EmulationStation | 模拟器前端 | 多平台 |
| Pegasus | 游戏前端 | 多平台 |
| Attract-Mode | 模拟器前端 | 多平台 |
| Steam ROM Manager | Steam 库工具 | 多平台 |

### API 集成示例

**Python：**

```python
import requests

class SteamGridDB:
    def __init__(self, api_key):
        self.base_url = "https://www.steamgriddb.com/api/v2"
        self.headers = {"Authorization": f"Bearer {api_key}"}
    
    def search(self, term):
        response = requests.get(
            f"{self.base_url}/search/autocomplete/{term}",
            headers=self.headers
        )
        return response.json()
    
    def get_grids(self, game_id):
        response = requests.get(
            f"{self.base_url}/grids/game/{game_id}",
            headers=self.headers
        )
        return response.json()
    
    def get_heroes(self, game_id):
        response = requests.get(
            f"{self.base_url}/heroes/game/{game_id}",
            headers=self.headers
        )
        return response.json()
```

**JavaScript：**

```javascript
const axios = require('axios');

class SteamGridDB {
    constructor(apiKey) {
        this.baseUrl = 'https://www.steamgriddb.com/api/v2';
        this.headers = { Authorization: `Bearer ${apiKey}` };
    }

    async search(term) {
        const response = await axios.get(
            `${this.baseUrl}/search/autocomplete/${term}`,
            { headers: this.headers }
        );
        return response.data;
    }

    async getGrids(gameId) {
        const response = await axios.get(
            `${this.baseUrl}/grids/game/${gameId}`,
            { headers: this.headers }
        );
        return response.data;
    }
}
```

---

## 速率限制

| 端点类型 | 限制 | 周期 |
|---------------|-------|--------|
| 搜索 | 100 请求 | 每分钟 |
| 游戏 | 100 请求 | 每分钟 |
| 网格/英雄图/标志/图标 | 100 请求 | 每分钟 |
| 上传 | 10 请求 | 每分钟 |

---

## 故障排除

### 常见问题

| 问题 | 解决方案 |
|-------|----------|
| API 密钥无效 | 在账户设置中重新生成密钥 |
| 未找到美术 | 检查游戏名称，尝试不同搜索 |
| 上传被拒 | 检查文件大小、格式、指南 |
| 速率限制 | 等待后重试，实现退避 |
| 美术不显示 | 重启 Steam，清除缓存 |

### 错误代码

| 代码 | 描述 | 解决方案 |
|------|-------------|----------|
| 401 | 未授权 | 检查 API 密钥 |
| 404 | 未找到 | 验证游戏/美术 ID |
| 429 | 速率限制 | 等待后重试 |
| 500 | 服务器错误 | 稍后重试 |

---

## 总结

SteamGridDB 是视频游戏美术的权威数据库，服务于终端用户和开发者。其全面的 API、对多平台和模拟器的支持以及活跃的社区使其成为任何想要自定义游戏库视觉外观的人的必备资源。该平台持续增长，社区定期添加新游戏和美术资源。
