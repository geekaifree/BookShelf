# wger：开源健身与营养追踪平台

## 目录

1. [简介](#introduction)
2. [安装](#installation)
3. [训练计划](#workout-plans)
4. [动作数据库](#exercise-database)
5. [营养追踪](#nutrition-tracking)
6. [体重追踪](#weight-tracking)
7. [REST API](#rest-api)
8. [移动端集成](#mobile-integration)
9. [自定义](#customization)
10. [最佳实践](#best-practices)

---

## 简介

wger 是一个开源健身与营养追踪平台，帮助用户管理训练、追踪营养摄入、监控体重，并维护完整的动作数据库。该平台提供 Web 界面和 REST API，可与移动应用及其他工具集成。

### 核心功能

| 功能 | 描述 |
|------|------|
| 训练管理 | 创建和管理训练计划，包含动作、组数和次数 |
| 营养追踪 | 记录饮食，追踪卡路里、宏量和微量营养素 |
| 动作数据库 | 包含详细描述和目标肌群的大量动作 |
| 体重追踪 | 通过图表监控体重变化 |
| REST API | 完整的 API，用于构建移动应用和集成 |
| 多语言 | 支持多种语言 |
| 自托管 | 完全掌控你的数据 |

### 架构概览

wger 使用 Django（Python）构建，数据库为 PostgreSQL。前端结合服务端模板和 JavaScript 实现交互功能。REST API 遵循 Django REST Framework 模式。

```
┌─────────────────────────────────────────────────┐
│                   Frontend                       │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │   Templates  │  │  JavaScript │  │   API   │ │
│  └─────────────┘  └─────────────┘  └─────────┘ │
├─────────────────────────────────────────────────┤
│                   Backend                        │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────┐ │
│  │    Django    │  │    REST     │  │ Database│ │
│  │   Views      │  │  Framework  │  │ (PgSQL) │ │
│  └─────────────┘  └─────────────┘  └─────────┘ │
└─────────────────────────────────────────────────┘
```

---

## 安装

### 前置要求

| 要求 | 版本 | 用途 |
|------|------|------|
| Python | 3.8+ | 运行环境 |
| PostgreSQL | 12+ | 数据库 |
| Node.js | 16+ | 前端资源 |
| pip | 最新版 | Python 包管理器 |
| Git | 最新版 | 版本控制 |

### Docker 安装

最简单的运行方式是使用 Docker：

```bash
# 克隆仓库
git clone https://github.com/wger-project/wger.git
cd wger

# 使用 Docker Compose 启动
docker-compose up -d

# 访问应用
# 在浏览器中打开 http://localhost:8000
```

### 手动安装

```bash
# 创建虚拟环境
python -m venv wger-venv
source wger-venv/bin/activate

# 安装依赖
pip install -r requirements.txt

# 配置数据库
# 编辑 wger/settings.py，填入数据库凭据

# 运行数据库迁移
python manage.py migrate

# 创建管理员用户
python manage.py createsuperuser

# 加载初始数据
python manage.py load-exercise-data

# 启动开发服务器
python manage.py runserver
```

### 配置

`settings.py` 中的关键配置项：

| 设置 | 默认值 | 描述 |
|------|--------|------|
| `DATABASES` | SQLite | 数据库配置 |
| `ALLOWED_REGISTRATION` | True | 允许新用户注册 |
| `WGER_SETTINGS` | dict | 应用特定设置 |
| `EMAIL_BACKEND` | console | 邮件配置 |
| `LANGUAGE_CODE` | en | 默认语言 |

### 生产环境部署

生产环境建议使用 Gunicorn 配合 Nginx：

```nginx
# /etc/nginx/sites-available/wger
server {
    listen 80;
    server_name your-domain.com;

    location /static/ {
        alias /path/to/wger/static/;
    }

    location /media/ {
        alias /path/to/wger/media/;
    }

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

```bash
# 使用 Gunicorn 启动
gunicorn wger.wsgi:application --bind 0.0.0.0:8000 --workers 4
```

---

## 训练计划

### 创建训练计划

wger 中的训练计划将动作组织成结构化的日常训练。每个计划可包含多天，每天可包含多个动作。

**第一步：创建新计划**

导航到"Workouts"，点击"New Workout Plan"，为其取一个描述性名称。

**第二步：添加训练日**

| 日类型 | 描述 | 示例 |
|--------|------|------|
| 推日 | 胸、肩、三头肌 | 卧推、肩上推举 |
| 拉日 | 背、二头肌 | 划船、引体向上 |
| 腿日 | 股四头肌、腘绳肌、小腿 | 深蹲、硬拉 |
| 全身 | 所有主要肌群 | 复合动作 |
| 休息日 | 恢复 | 轻度拉伸、散步 |

**第三步：为每天添加动作**

为每天添加动作时，设置以下参数：

| 参数 | 描述 | 示例 |
|------|------|------|
| 动作 | 从数据库选择 | 杠铃卧推 |
| 组数 | 组数 | 4 |
| 次数 | 每组重复次数 | 8-12 |
| 休息 | 组间休息（秒） | 90 |
| 重量 | 起始重量（kg/lbs） | 60 |
| RPE | 主观疲劳等级 | 8 |

### 训练模板

为常用训练创建可复用模板：

```
训练计划："增肌计划"
├── 第1天：推
│   ├── 卧推：4x8-12，休息90秒
│   ├── 肩上推举：3x10-12，休息60秒
│   ├── 上斜哑铃卧推：3x12，休息60秒
│   ├── 侧平举：4x15，休息45秒
│   └── 三头下压：3x15，休息45秒
├── 第2天：拉
│   ├── 杠铃划船：4x8-12，休息90秒
│   ├── 引体向上：3x8-10，休息90秒
│   ├── 面拉：3x15，休息45秒
│   ├── 杠铃弯举：3x12，休息60秒
│   └── 锤式弯举：3x12，休息45秒
├── 第3天：腿
│   ├── 深蹲：4x8-12，休息120秒
│   ├── 罗马尼亚硬拉：3x10-12，休息90秒
│   ├── 腿举：3x12-15，休息60秒
│   ├── 腿弯举：3x12，休息60秒
│   └── 提踵：4x15，休息45秒
└── 第4天：休息
```

### 渐进超负荷追踪

wger 支持追踪渐进超负荷：

| 周 | 动作 | 组x次 | 重量 | 总容量 |
|----|------|-------|------|--------|
| 1 | 卧推 | 4x10 | 60kg | 2400kg |
| 2 | 卧推 | 4x10 | 62.5kg | 2500kg |
| 3 | 卧推 | 4x10 | 65kg | 2600kg |
| 4 | 卧推 | 4x12 | 60kg | 2880kg |

### 训练安排

设置周期性训练计划：

- **频率**：每周 3-6 天
- **轮换**：自动循环训练日
- **日历集成**：导出到日历应用
- **提醒**：邮件/推送通知

---

## 动作数据库

### 动作分类

动作数据库按肌群和器械组织：

| 肌群 | 示例动作 | 器械 |
|------|----------|------|
| 胸 | 卧推、飞鸟、俯卧撑 | 杠铃、哑铃、器械 |
| 背 | 划船、引体向上、高位下拉 | 杠铃、绳索、自重 |
| 肩 | 推举、平举、耸肩 | 哑铃、绳索、器械 |
| 腿 | 深蹲、弓步蹲、腿举 | 杠铃、器械、自重 |
| 手臂 | 弯举、臂屈伸、双杠 | 哑铃、绳索、杠铃 |
| 核心 | 卷腹、平板支撑、抬腿 | 自重、绳索、器械 |

### 添加自定义动作

用户可以向动作数据库贡献内容：

```
动作数据结构：
- name: 动作名称
- category: chest
- muscles: [pectoralis_major]
- muscles_secondary: [anterior_deltoid, triceps]
- equipment: [barbell, bench]
- description: 详细动作描述
- instructions: 分步指导
- variations: [variation1, variation2]
```

### 动作变体

每个动作可以有多个变体：

| 基础动作 | 变体 | 区别 |
|----------|------|------|
| 卧推 | 上斜卧推 | 侧重上胸 |
| 卧推 | 下斜卧推 | 侧重下胸 |
| 卧推 | 窄握卧推 | 侧重三头肌 |
| 深蹲 | 前蹲 | 侧重股四头肌 |
| 深蹲 | 保加利亚分腿蹲 | 单侧训练 |

### 筛选和搜索

可按以下条件筛选动作：

- **肌群**：主要和次要肌群
- **器械**：可用的健身器械
- **难度**：初级、中级、高级
- **类型**：复合、孤立、有氧

---

## 营养追踪

### 设置营养目标

定义每日营养目标：

| 营养素 | 目标 | 范围 | 用途 |
|--------|------|------|------|
| 卡路里 | 2500 kcal | 2300-2700 | 能量平衡 |
| 蛋白质 | 180g | 160-200g | 肌肉修复 |
| 碳水化合物 | 300g | 250-350g | 能量 |
| 脂肪 | 70g | 60-80g | 激素、吸收 |
| 膳食纤维 | 30g | 25-35g | 消化健康 |

### 记录饮食

全天追踪饮食：

**早餐示例：**

| 食物 | 份量 | 卡路里 | 蛋白质 | 碳水 | 脂肪 |
|------|------|--------|--------|------|------|
| 燕麦 | 100g | 389 | 16.9g | 66.3g | 6.9g |
| 香蕉 | 1根 | 105 | 1.3g | 27g | 0.4g |
| 乳清蛋白 | 30g | 120 | 24g | 3g | 1.5g |
| **合计** | | **614** | **42.2g** | **96.3g** | **8.8g** |

### 营养数据库

营养数据库包含：

- **品牌食品**：厂商产品
- **普通食品**：常见天然食品
- **餐厅菜品**：快餐和餐厅餐食
- **自定义条目**：用户创建的食物

### 饮食计划

创建可复用的饮食计划：

```
饮食计划："增肌饮食"
├── 第1餐：早餐（7:00）
│   ├── 燕麦配浆果
│   ├── 鸡蛋（3个全蛋）
│   └── 橙汁
├── 第2餐：加餐（10:00）
│   ├── 希腊酸奶
│   └── 混合坚果
├── 第3餐：午餐（13:00）
│   ├── 鸡胸肉
│   ├── 糙米
│   └── 西兰花
├── 第4餐：训练前（16:00）
│   ├── 香蕉
│   └── 蛋白奶昔
└── 第5餐：晚餐（19:00）
    ├── 三文鱼
    ├── 红薯
    └── 蔬菜沙拉
```

### 营养报告

生成详细的营养报告：

| 指标 | 每日 | 每周 | 每月 |
|------|------|------|------|
| 平均卡路里 | 2,450 | 17,150 | 73,500 |
| 平均蛋白质 | 175g | 1,225g | 5,250g |
| 目标达成率 | 92% | 88% | 85% |
| 达标天数 | 6/7 | 28/30 | 85% |

---

## 体重追踪

### 记录体重

追踪体重变化：

| 日期 | 体重 | 变化 | 备注 |
|------|------|------|------|
| 2024-01-01 | 80.0kg | - | 起始体重 |
| 2024-01-08 | 79.5kg | -0.5kg | 表现不错 |
| 2024-01-15 | 79.2kg | -0.3kg | 持续稳定 |
| 2024-01-22 | 79.0kg | -0.2kg | 进展放缓 |
| 2024-01-29 | 78.8kg | -0.2kg | 按计划进行 |

### 体重图表

wger 生成可视化图表，显示：

- **每日体重**：单次测量值
- **移动平均**：7天和30天平均值
- **趋势线**：整体方向
- **目标线**：目标体重轨迹

### 身体围度

追踪额外测量数据：

| 测量项 | 起始 | 当前 | 变化 |
|--------|------|------|------|
| 胸围 | 100cm | 102cm | +2cm |
| 腰围 | 85cm | 82cm | -3cm |
| 臂围 | 35cm | 37cm | +2cm |
| 大腿围 | 55cm | 57cm | +2cm |
| 体脂率 | 18% | 15% | -3% |

### 统计分析

系统计算：

- **体重变化率**：每周公斤数
- **热量盈余/缺口**：根据体重变化估算
- **预测**：预计达成目标日期
- **一致性评分**：追踪规律性

---

## REST API

### 认证

```bash
# 获取 API token
curl -X POST https://wger.example.com/api/v2/token \
  -d "username=your_username" \
  -d "password=your_password"

# 响应
{
    "token": "9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b"
}
```

### API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/v2/workout/` | GET/POST | 列出/创建训练 |
| `/api/v2/workout/{id}/` | GET/PUT/DELETE | 管理特定训练 |
| `/api/v2/exercise/` | GET | 列出动作 |
| `/api/v2/nutrition/` | GET/POST | 营养计划 |
| `/api/v2/weight/` | GET/POST | 体重记录 |
| `/api/v2/setting/` | GET/POST | 训练设置 |
| `/api/v2/day/` | GET/POST | 训练日 |
| `/api/v2/set/` | GET/POST | 动作组数 |

### API 调用示例

**获取所有训练：**

```bash
curl -H "Authorization: Token 9944b09199c62bcf9418ad846dd0e4bbdfc6ee4b" \
  https://wger.example.com/api/v2/workout/
```

**创建新训练：**

```bash
curl -X POST \
  -H "Authorization: Token your_token" \
  -H "Content-Type: application/json" \
  -d '{"comment": "My new workout"}' \
  https://wger.example.com/api/v2/workout/
```

**记录体重：**

```bash
curl -X POST \
  -H "Authorization: Token your_token" \
  -H "Content-Type: application/json" \
  -d '{"date": "2024-01-15", "weight": 79.5}' \
  https://wger.example.com/api/v2/weight/
```

### API 响应格式

```json
{
    "count": 42,
    "next": "http://example.com/api/v2/exercise/?page=2",
    "previous": null,
    "results": [
        {
            "id": 1,
            "name": "Barbell Bench Press",
            "category": 10,
            "muscles": [4, 5],
            "equipment": [1, 8]
        }
    ]
}
```

### 速率限制

| 端点类型 | 限制 | 时间窗口 |
|----------|------|----------|
| 读取 | 1000 请求 | 每小时 |
| 写入 | 100 请求 | 每小时 |
| 已认证 | 更高限制 | 每小时 |

---

## 移动端集成

### 官方移动应用

wger 提供以下平台的移动应用：

| 平台 | 功能 | 下载 |
|------|------|------|
| Android | 完整训练追踪，离线模式 | Google Play |
| iOS | 训练记录，体重追踪 | App Store |

### 移动应用功能

- **离线模式**：无网络时也能记录训练
- **同步**：上线后自动同步
- **相机**：拍摄进度照片
- **通知**：训练提醒
- **小组件**：快速记录入口

### 构建自定义移动应用

使用 REST API 构建自定义应用：

```javascript
// React Native 示例
const API_BASE = 'https://wger.example.com/api/v2';

async function getWorkouts(token) {
    const response = await fetch(`${API_BASE}/workout/`, {
        headers: {
            'Authorization': `Token ${token}`,
            'Content-Type': 'application/json'
        }
    });
    return response.json();
}

async function logWeight(token, date, weight) {
    const response = await fetch(`${API_BASE}/weight/`, {
        method: 'POST',
        headers: {
            'Authorization': `Token ${token}`,
            'Content-Type': 'application/json'
        },
        body: JSON.stringify({ date, weight })
    });
    return response.json();
}
```

### 第三方集成

| 集成 | 方向 | 同步数据 |
|------|------|----------|
| Google Fit | 导出 | 训练数据 |
| Apple Health | 导出 | 体重、训练 |
| Fitbit | 导入 | 活动数据 |
| Strava | 导入 | 有氧训练 |

---

## 自定义

### 主题

自定义外观：

```python
# 在 settings.py 中自定义 CSS
WGER_SETTINGS = {
    'theme': 'dark',
    'accent_color': '#4CAF50',
    'logo': '/path/to/logo.png',
    'favicon': '/path/to/favicon.ico'
}
```

### 自定义动作分类

添加组织特定的动作分类：

```python
# 在 Django admin 或通过管理命令
from exercises.models import ExerciseCategory

ExerciseCategory.objects.create(
    name="Functional Training",
    description="Functional movement patterns"
)
```

### 语言配置

| 语言 | 代码 | 状态 |
|------|------|------|
| 英语 | en | 完整 |
| 德语 | de | 完整 |
| 西班牙语 | es | 完整 |
| 法语 | fr | 完整 |
| 葡萄牙语 | pt | 完整 |
| 俄语 | ru | 部分 |

### 用户权限

配置用户角色：

| 角色 | 权限 |
|------|------|
| 用户 | 追踪自己的训练和营养 |
| 教练 | 查看客户训练，创建计划 |
| 管理员 | 完全系统访问 |
| API 用户 | 仅编程访问 |

### 邮件模板

自定义通知邮件：

```html
<!-- templates/emails/workout_reminder.html -->
<h1>训练提醒</h1>
<p>你好 {{ user.username }}，</p>
<p>别忘了今天的 {{ workout.name }} 训练！</p>
<p>动作：</p>
<ul>
{% for exercise in workout.exercises %}
    <li>{{ exercise.name }} - {{ exercise.sets }}x{{ exercise.reps }}</li>
{% endfor %}
</ul>
```

---

## 最佳实践

### 数据备份

定期备份至关重要：

```bash
# 数据库备份
pg_dump wger_db > wger_backup_$(date +%Y%m%d).sql

# 媒体备份
tar -czf wger_media_$(date +%Y%m%d).tar.gz /path/to/media/

# 自动备份脚本
#!/bin/bash
BACKUP_DIR="/backups/wger"
DATE=$(date +%Y%m%d)
pg_dump wger_db | gzip > "$BACKUP_DIR/db_$DATE.sql.gz"
tar -czf "$BACKUP_DIR/media_$DATE.tar.gz" /path/to/media/
```

### 性能优化

| 优化措施 | 实施方式 | 影响 |
|----------|----------|------|
| 缓存 | Redis/Memcached | 高 |
| 数据库索引 | 合理索引 | 中 |
| 静态文件 | CDN 加速 | 中 |
| 查询优化 | select_related/prefetch_related | 高 |

### 安全检查清单

- 生产环境启用 HTTPS
- 设置强密码 SECRET_KEY
- 配置 ALLOWED_HOSTS
- 启用 CSRF 保护
- 设置安全 Cookie 标志
- 定期安全更新
- 数据库静态加密
- API 速率限制

### 常见问题

| 问题 | 解决方案 |
|------|----------|
| 查询慢 | 添加数据库索引 |
| 内存占用高 | 优化 Django 查询 |
| API 错误 | 检查认证 token |
| 同步问题 | 验证网络连接 |

---

## 总结

wger 提供了一个全面的健身与营养追踪平台：

- **灵活的训练管理**：创建和自定义训练计划
- **详细的营养追踪**：监控卡路里和宏量营养素
- **进度监控**：追踪体重和身体围度
- **REST API**：构建自定义集成和移动应用
- **自托管**：完全掌控你的健身数据

该平台适合个人用户、私人教练以及寻求开源健身追踪方案的组织。
