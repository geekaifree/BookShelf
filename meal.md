# 使用 Mealie 进行膳食规划

## 简介

Mealie 是一个自托管的膳食规划和食谱管理应用。它提供了组织食谱、规划膳食和生成购物清单的工具。

### 什么是 Mealie？

Mealie 是一个食谱管理系统，帮助您收集、组织和规划个人食谱收藏中的膳食。

| 特性 | 描述 |
|------|------|
| 食谱管理 | 存储和组织食谱 |
| 膳食规划 | 每周/每月膳食计划 |
| 购物清单 | 从计划自动生成 |
| 食谱抓取 | 从网站导入 |
| 多用户 | 家庭支持 |

### 与其他方案的比较

| 特性 | Mealie | Paprika | Tandoor |
|------|--------|---------|---------|
| 自托管 | 是 | 否 | 是 |
| 网页抓取 | 是 | 是 | 是 |
| 膳食规划 | 是 | 是 | 是 |
| 购物清单 | 是 | 是 | 是 |
| API | 是 | 否 | 是 |

## 安装

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2 核 |
| 内存 | 512 MB | 1 GB |
| 存储 | 1 GB | 5 GB |
| Docker | 20.10+ | 最新版 |

### Docker 安装

```yaml
version: '3'
services:
  mealie:
    image: hkotel/mealie:latest
    container_name: mealie
    ports:
      - "9925:9000"
    volumes:
      - mealie_data:/app/data
    environment:
      - ALLOW_SIGNUP=true
      - TZ=America/New_York
    restart: unless-stopped

volumes:
  mealie_data:
```

### 手动安装

```bash
# 克隆仓库
git clone https://github.com/mealie-recipes/mealie.git
cd mealie

# 安装后端
cd backend
pip install -r requirements.txt

# 安装前端
cd ../frontend
npm install
npm run build

# 运行应用
cd ../backend
uvicorn app:app --host 0.0.0.0 --port 9000
```

### 环境变量

```env
ALLOW_SIGNUP=true
API_PORT=9000
TZ=America/New_York
DEFAULT_GROUP=Home
DB_TYPE=sqlite
```

## 食谱管理

### 添加食谱

1. 点击 "Create Recipe"
2. 输入食谱详情
3. 添加食材
4. 添加步骤
5. 保存食谱

### 食谱属性

| 属性 | 描述 |
|------|------|
| 名称 | 食谱标题 |
| 描述 | 简要概述 |
| 准备时间 | 准备时间 |
| 烹饪时间 | 烹饪时间 |
| 份量 | 份数 |
| 分类 | 食谱分类 |
| 标签 | 食谱标签 |

### 导入食谱

| 方式 | 描述 |
|------|------|
| URL | 从网站抓取 |
| 文件 | 从文件导入 |
| 手动 | 手动输入 |
| 批量导入 | 导入多个 |

### URL 导入

```bash
# 通过 API
curl -X POST https://mealie.example.com/api/recipes/create-url \
  -H "Authorization: Bearer TOKEN" \
  -d '{"url": "https://example.com/recipe"}'
```

### 支持的导入格式

| 格式 | 描述 |
|------|------|
| JSON | Mealie 格式 |
| CSV | 电子表格格式 |
| Paprika | Paprika 导出 |
| Copy Me That | Copy Me That 导出 |

## 食谱结构

### 食材

```yaml
- name: Flour
  quantity: 2
  unit: cups
  notes: All-purpose

- name: Sugar
  quantity: 1
  unit: cup
  notes: Granulated
```

### 步骤

```yaml
- step: 1
  text: Preheat oven to 350°F

- step: 2
  text: Mix dry ingredients in bowl

- step: 3
  text: Add wet ingredients and mix
```

### 营养信息

| 字段 | 单位 |
|------|------|
| 热量 | kcal |
| 蛋白质 | g |
| 碳水化合物 | g |
| 脂肪 | g |
| 纤维 | g |
| 糖 | g |

## 膳食规划

### 创建膳食计划

1. 进入 Meal Planner
2. 选择日期范围
3. 将食谱添加到各天
4. 生成购物清单

### 膳食类型

| 类型 | 描述 |
|------|------|
| 早餐 | 早晨膳食 |
| 午餐 | 中午膳食 |
| 晚餐 | 晚间膳食 |
| 零食 | 两餐之间 |

### 周计划示例

| 天 | 早餐 | 午餐 | 晚餐 |
|----|------|------|------|
| 周一 | 燕麦粥 | 三明治 | 意面 |
| 周二 | 鸡蛋 | 沙拉 | 炒菜 |
| 周三 | 奶昔 | 汤 | 墨西哥卷饼 |
| 周四 | 吐司 | 卷饼 | 咖喱 |
| 周五 | 煎饼 | 碗饭 | 披萨 |

### 膳食计划设置

| 设置 | 描述 |
|------|------|
| 开始日 | 一周开始日 |
| 膳食时段 | 每天餐数 |
| 自动规划 | 自动建议 |
| 购物清单 | 自动生成清单 |

## 购物清单

### 自动生成清单

购物清单从膳食计划自动创建：

| 功能 | 描述 |
|------|------|
| 合并 | 合并重复食材 |
| 分类 | 按商店区域分组 |
| 勾选 | 标记已购买 |
| 备注 | 添加自定义项目 |

### 购物清单分类

| 分类 | 示例 |
|------|------|
| 生鲜 | 水果、蔬菜 |
| 乳制品 | 牛奶、奶酪、鸡蛋 |
| 肉类 | 鸡肉、牛肉、鱼 |
| 食品柜 | 面粉、糖、香料 |
| 冷冻 | 冷冻蔬菜 |
| 烘焙 | 面包、卷饼 |

### 管理清单

| 操作 | 描述 |
|------|------|
| 创建 | 新购物清单 |
| 编辑 | 修改项目 |
| 勾选 | 标记已购买 |
| 分享 | 与家庭分享 |
| 打印 | 打印清单 |

## 分类和标签

### 分类

| 用途 | 示例 |
|------|------|
| 膳食类型 | 早餐、午餐、晚餐 |
| 菜系 | 意式、墨西哥、亚洲 |
| 饮食 | 素食、纯素、无麸质 |
| 菜式 | 前菜、主菜、甜点 |

### 标签

| 用途 | 示例 |
|------|------|
| 难度 | 简单、中等、困难 |
| 时间 | 快速、慢炖 |
| 场合 | 节日、工作日 |
| 方法 | 烤、烘、炸 |

### 组织食谱

| 方式 | 描述 |
|------|------|
| 搜索 | 全文搜索 |
| 过滤 | 按分类、标签 |
| 排序 | 按名称、日期、评分 |
| 收藏 | 固定收藏食谱 |

## 多用户支持

### 家庭管理

| 功能 | 描述 |
|------|------|
| 群组 | 家庭群组 |
| 成员 | 添加家庭成员 |
| 权限 | 控制访问级别 |
| 共享计划 | 协作规划 |

### 用户角色

| 角色 | 权限 |
|------|------|
| Admin | 完全访问 |
| User | 创建、编辑自己的 |
| Guest | 仅查看 |

## API 访问

### REST API

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/recipes` | GET | 列出食谱 |
| `/api/recipes/{slug}` | GET | 获取食谱 |
| `/api/recipes` | POST | 创建食谱 |
| `/api/meal-plans` | GET | 获取膳食计划 |
| `/api/shopping-lists` | GET | 获取购物清单 |

### API 身份验证

```bash
# 获取 API 令牌
curl -X POST https://mealie.example.com/api/auth/token \
  -d "username=user&password=pass"
```

### API 使用

```bash
# 列出食谱
curl -H "Authorization: Bearer TOKEN" \
  https://mealie.example.com/api/recipes

# 创建食谱
curl -X POST https://mealie.example.com/api/recipes \
  -H "Authorization: Bearer TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "New Recipe", "description": "A great recipe"}'
```

## 食谱抓取

### 支持的网站

Mealie 支持从大多数使用 Schema.org Recipe 标记的食谱网站抓取。

### 抓取流程

1. 复制食谱 URL
2. 点击 "Import from URL"
3. 粘贴 URL
4. 审查导入的数据
5. 保存食谱

### 抓取配置

| 设置 | 描述 |
|------|------|
| 超时 | 请求超时 |
| User agent | 浏览器标识 |
| 代理 | 代理服务器 |

## 数据管理

### 备份和恢复

```bash
# 备份
docker exec mealie python -m app.utils.backup

# 恢复
docker exec mealie python -m app.utils.restore backup.zip
```

### 导出选项

| 格式 | 描述 |
|------|------|
| JSON | 完整食谱数据 |
| PDF | 可打印食谱 |
| 购物清单 | 导出清单 |

### 导入选项

| 来源 | 格式 |
|------|------|
| Mealie | JSON |
| Paprika | Paprika 导出 |
| 其他 | CSV、JSON |

## 自定义

### 主题

| 设置 | 选项 |
|------|------|
| 主题 | 亮色、暗色、系统 |
| 颜色 | 主色调 |
| 字体 | 字体族 |

### 语言

Mealie 支持多种语言：

| 语言 | 状态 |
|------|------|
| 英语 | 完全 |
| 德语 | 完全 |
| 法语 | 完全 |
| 西班牙语 | 完全 |
| 其他 | 部分 |

## Web 服务器配置

### Nginx 反向代理

```nginx
server {
    listen 80;
    server_name recipes.example.com;

    location / {
        proxy_pass http://localhost:9925;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### 使用 Let's Encrypt 配置 SSL

```bash
sudo apt install certbot python3-certbot-nginx
sudo certbot --nginx -d recipes.example.com
```

## 移动端访问

### 响应式设计

Mealie 在移动浏览器上具有良好的响应式设计。

### Progressive Web App

Mealie 可以作为 PWA 安装到移动设备上。

## 提示和最佳实践

### 食谱组织

| 提示 | 描述 |
|------|------|
| 使用分类 | 按膳食类型组织 |
| 添加标签 | 便于筛选 |
| 评分食谱 | 追踪收藏 |
| 添加备注 | 记录修改 |

### 膳食规划提示

| 提示 | 描述 |
|------|------|
| 每周规划 | 一次规划一周 |
| 利用剩菜 | 规划剩饭菜 |
| 营养均衡 | 包含多样性 |
| 检查食品柜 | 使用现有食材 |

## 总结

| 功能 | 用途 |
|------|------|
| 食谱 | 存储和组织 |
| 膳食计划 | 每周规划 |
| 购物清单 | 自动生成 |
| 导入 | 从网站抓取 |
| 多用户 | 家庭支持 |
