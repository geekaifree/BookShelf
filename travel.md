# 旅行

> 本文档整合了以下源文件：travel.md, mate.md, trip.md, canada.md

---

## 来源：travel.md

## 简介

TREK 是一个开源旅行规划应用，帮助您组织行程、管理日程和追踪费用。它提供了一个简洁的界面用于规划旅行。

### 什么是 TREK？

TREK 是一个自托管旅行规划器，允许您创建详细的旅行日程、管理预订和记录旅行费用。

| 特性 | 描述 |
|------|------|
| 行程规划 | 创建和组织旅行 |
| 日程管理 | 逐日安排 |
| 费用追踪 | 监控旅行成本 |
| 预订管理 | 存储预订确认 |
| 协作 | 与他人分享行程 |

### 为什么要自托管旅行规划器？

| 好处 | 描述 |
|------|------|
| 隐私 | 保持旅行数据私密 |
| 定制化 | 根据需求定制 |
| 离线访问 | 无需网络即可规划 |
| 费用 | 无订阅费 |

## 安装

### 前置要求

| 要求 | 版本 |
|------|------|
| PHP | 8.0 或更高 |
| Composer | 2.0 或更高 |
| 数据库 | MySQL 或 SQLite |
| Web 服务器 | Apache 或 Nginx |

### 安装步骤

```bash
# 克隆仓库
git clone https://github.com/mauriceboe/TREK.git
cd TREK

# 安装依赖
composer install

# 配置环境
cp .env.example .env
php artisan key:generate

# 设置数据库
php artisan migrate

# 创建管理员用户
php artisan db:seed
```

### 环境配置

```env
APP_NAME=TREK
APP_URL=http://localhost:8000
DB_CONNECTION=sqlite
DB_DATABASE=/path/to/database.sqlite
```

### 运行应用

```bash
php artisan serve
```

## 行程管理

### 创建行程

1. 点击 "New Trip"
2. 输入行程详情
3. 添加目的地
4. 设置日期

### 行程属性

| 属性 | 描述 |
|------|------|
| 名称 | 行程标题 |
| 开始日期 | 行程开始 |
| 结束日期 | 行程结束 |
| 目的地 | 要访问的地点 |
| 预算 | 预期费用 |

### 行程状态

| 状态 | 描述 |
|------|------|
| Planning | 规划阶段 |
| Confirmed | 预订已确认 |
| Active | 正在旅行中 |
| Completed | 行程完成 |
| Cancelled | 行程取消 |

## 日程规划

### 每日日程

```
Day 1: Arrival
├── 10:00 - Airport arrival
├── 12:00 - Hotel check-in
├── 14:00 - Lunch at restaurant
├── 16:00 - City tour
└── 19:00 - Dinner

Day 2: Sightseeing
├── 09:00 - Breakfast
├── 10:00 - Museum visit
├── 13:00 - Lunch
├── 15:00 - Park visit
└── 18:00 - Shopping
```

### 活动类型

| 类型 | 描述 |
|------|------|
| 交通 | 航班、火车、大巴 |
| 住宿 | 酒店、旅馆 |
| 餐饮 | 餐厅、咖啡馆 |
| 活动 | 游览、景点 |
| 购物 | 市场、商店 |

### 活动属性

| 属性 | 描述 |
|------|------|
| 时间 | 预定时间 |
| 时长 | 预期长度 |
| 地点 | 活动地点 |
| 费用 | 预期成本 |
| 备注 | 附加详情 |
| 预订号 | 确认号 |

## 预订管理

### 预订类型

| 类型 | 信息 |
|------|------|
| 航班 | 航空公司、航班号、座位 |
| 酒店 | 酒店、房型、日期 |
| 租车 | 公司、车型、日期 |
| 活动 | 提供商、时间、参与人数 |
| 餐厅 | 餐厅、时间、人数 |

### 预订详情

| 字段 | 描述 |
|------|------|
| 确认号 | 预订参考号 |
| 提供商 | 公司名称 |
| 联系方式 | 电话、邮箱 |
| 费用 | 总费用 |
| 取消政策 | 取消条款 |
| 文档 | 附件 |

## 费用追踪

### 费用类别

| 类别 | 示例 |
|------|------|
| 交通 | 航班、火车、出租车 |
| 住宿 | 酒店、旅馆 |
| 餐饮 | 餐厅、杂货 |
| 活动 | 游览、门票 |
| 购物 | 纪念品、礼物 |
| 其他 | 杂项 |

### 添加费用

1. 选择行程
2. 点击 "Add Expense"
3. 输入详情
4. 附加收据（可选）

### 费用汇总

| 类别 | 预算 | 已花 | 剩余 |
|------|------|------|------|
| 交通 | $500 | $450 | $50 |
| 住宿 | $800 | $750 | $50 |
| 餐饮 | $300 | $280 | $20 |
| 活动 | $200 | $150 | $50 |
| **合计** | **$1800** | **$1630** | **$170** |

## 目的地管理

### 目的地属性

| 属性 | 描述 |
|------|------|
| 名称 | 地点名称 |
| 国家 | 国家 |
| 坐标 | GPS 坐标 |
| 备注 | 当地信息 |
| 景点 | 兴趣点 |

### 兴趣点

| 类型 | 示例 |
|------|------|
| 地标 | 著名建筑、纪念碑 |
| 博物馆 | 艺术、历史博物馆 |
| 公园 | 国家公园、花园 |
| 餐厅 | 推荐餐饮 |
| 酒店 | 推荐住宿 |

## 协作

### 分享行程

| 权限 | 描述 |
|------|------|
| 查看 | 可查看行程详情 |
| 编辑 | 可修改行程 |
| 管理 | 完全控制 |

### 共同规划

| 功能 | 描述 |
|------|------|
| 评论 | 讨论计划 |
| 建议 | 提出变更 |
| 投票 | 对选项投票 |
| 任务 | 分配职责 |

## 日历集成

### 日历同步

```bash
# 导出为 iCal 格式
php artisan trek:export --format=ical --trip=1

# 导出到 Google Calendar
php artisan trek:export --format=google --trip=1
```

### 日历视图

| 视图 | 描述 |
|------|------|
| Daily | 逐日安排 |
| Weekly | 周概览 |
| Monthly | 月概览 |
| Timeline | 行程时间线 |

## 报告

### 行程报告

| 部分 | 内容 |
|------|------|
| 概览 | 行程摘要 |
| 日程 | 逐日计划 |
| 费用 | 成本明细 |
| 预订 | 确认详情 |
| 备注 | 附加信息 |

### 费用报告

| 类别 | 数量 | 总计 |
|------|------|------|
| 交通 | 5 | $450 |
| 住宿 | 7 | $750 |
| 餐饮 | 14 | $280 |
| 活动 | 4 | $150 |
| **合计** | **30** | **$1630** |

## 移动端访问

### 响应式设计

TREK 可通过移动浏览器访问，具有响应式界面。

### 离线支持

| 功能 | 状态 |
|------|------|
| 查看日程 | 离线可用 |
| 添加费用 | 在线时同步 |
| 查看预订 | 离线可用 |

## 数据管理

### 导出选项

| 格式 | 描述 |
|------|------|
| PDF | 可打印日程 |
| CSV | 费用数据 |
| JSON | 完整行程数据 |
| iCal | 日历格式 |

### 导入选项

| 来源 | 描述 |
|------|------|
| CSV | 费用导入 |
| JSON | 行程导入 |
| 其他规划器 | 迁移工具 |

## Web 服务器配置

### Nginx 配置

```nginx
server {
    listen 80;
    server_name trek.example.com;
    root /var/www/TREK/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.0-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

## Docker 部署

### Docker Compose

```yaml
version: '3'
services:
  trek:
    image: trek
    ports:
      - "8000:80"
    volumes:
      - ./data:/var/www/html/storage
    environment:
      - DB_CONNECTION=sqlite
      - DB_DATABASE=/var/www/html/storage/database.sqlite

  nginx:
    image: nginx:alpine
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/conf.d/default.conf
```

## 提示和最佳实践

### 规划提示

| 提示 | 描述 |
|------|------|
| 提前开始 | 尽早规划 |
| 保持灵活 | 允许变更 |
| 做功课 | 了解目的地 |
| 设定预算 | 设定合理预算 |
| 备份 | 保留文档副本 |

### 组织提示

| 提示 | 描述 |
|------|------|
| 使用分类 | 组织费用 |
| 添加备注 | 记录重要细节 |
| 附加文件 | 存储确认单 |
| 定期审查 | 按需更新计划 |

## 总结

| 功能 | 用途 |
|------|------|
| 行程 | 组织旅行计划 |
| 日程 | 逐日安排 |
| 预订 | 管理预订 |
| 费用 | 追踪成本 |
| 协作 | 与他人分享 |


---

## 来源：mate.md

## 简介

Travel Mate 是一款开源 Android 应用，旨在成为全面的旅行伴侣。它帮助用户规划行程、发现目的地、管理行程安排，并提供实用的旅行工具，如货币转换、天气预报和清单。该应用支持离线使用，并为全球热门目的地提供城市指南。

**核心功能：**

- 行程规划和行程管理
- 包含景点和信息的城市指南
- 酒店和住宿搜索
- 目的地天气预报
- 实时汇率货币转换器
- 旅行清单
- 离线地图和数据
- 实时行程追踪

---

## 安装

### 系统要求

| 要求 | 最低 | 推荐 |
|-------------|---------|-------------|
| Android 版本 | 5.0（Lollipop） | 8.0+ |
| 内存 | 1 GB | 2 GB |
| 存储 | 50 MB | 200 MB |
| 网络 | 可选 | 推荐 |

### 从源码安装

```bash
git clone https://github.com/project-travel-mate/Travel-Mate.git
cd Travel-Mate
./gradlew assembleDebug
```

APK 将生成在 `app/build/outputs/apk/debug/` 目录下。

### 从 F-Droid 安装

1. 在 Android 设备上打开 F-Droid
2. 搜索"Travel Mate"
3. 点击安装
4. 打开应用

### 所需权限

| 权限 | 用途 |
|------------|---------|
| 网络 | 获取天气、地图、酒店数据 |
| 位置 | 行程追踪、附近地点 |
| 存储 | 保存地图和离线数据 |
| 相机 | 拍摄旅行照片 |

---

## 行程规划

### 创建新行程

1. 打开应用并点击"+"按钮
2. 输入行程名称和日期
3. 选择目的地城市
4. 添加行程描述（可选）
5. 选择封面照片
6. 保存行程

### 行程管理

| 操作 | 描述 |
|--------|-------------|
| 编辑行程 | 修改日期、目的地、描述 |
| 删除行程 | 删除行程及所有相关数据 |
| 分享行程 | 与旅伴分享行程安排 |
| 复制行程 | 为类似行程创建副本 |
| 归档行程 | 将已完成行程移至归档 |

### 行程构建器

为您的行程构建逐日安排：

**添加活动：**
1. 打开行程
2. 选择一天
3. 点击"添加活动"
4. 输入活动详情：
   - 名称
   - 时间
   - 地点
   - 备注
   - 类别（美食、观光、交通等）

**活动类别：**

| 类别 | 图标 | 用途 |
|----------|------|---------|
| 观光 | 相机 | 旅游景点 |
| 美食 | 刀叉 | 餐厅和咖啡馆 |
| 交通 | 汽车 | 地点间移动 |
| 住宿 | 床 | 住宿场所 |
| 购物 | 包 | 购物地点 |
| 活动 | 人 | 游览和活动 |
| 其他 | 星星 | 其他事项 |

---

## 城市指南

### 可用城市

Travel Mate 包含全球数百个城市的指南：

| 地区 | 热门城市 |
|--------|---------------|
| 欧洲 | 巴黎、伦敦、罗马、巴塞罗那、阿姆斯特丹 |
| 亚洲 | 东京、曼谷、新加坡、孟买、首尔 |
| 美洲 | 纽约、里约热内卢、墨西哥城、多伦多 |
| 非洲 | 开罗、开普敦、马拉喀什、内罗毕 |
| 大洋洲 | 悉尼、墨尔本、奥克兰 |

### 城市指南内容

每个城市指南包含：

| 部分 | 信息 |
|---------|-------------|
| 概述 | 城市描述、人口、语言 |
| 景点 | 评分最高的旅游景点 |
| 餐厅 | 热门餐饮选择 |
| 酒店 | 住宿推荐 |
| 购物 | 最佳购物区域和商场 |
| 夜生活 | 酒吧、俱乐部、娱乐 |
| 交通 | 公共交通、出租车、共享单车 |
| 建议 | 当地习俗、安全、小费 |

### 景点详情

每个景点列表包含：

- 名称和描述
- 照片和图片
- 地址和地图位置
- 开放时间
- 门票价格
- 用户评分和评论
- 建议和推荐
- 附近景点

---

## 酒店搜索

### 搜索酒店

1. 打开行程或城市指南
2. 点击"酒店"部分
3. 输入入住和退房日期
4. 设置客人数量和房间数
5. 应用筛选条件（价格、评分、设施）
6. 查看结果

### 酒店筛选

| 筛选 | 选项 |
|--------|---------|
| 价格范围 | 经济、中档、豪华 |
| 星级 | 1-5 星 |
| 客人评分 | 1-10 |
| 设施 | WiFi、泳池、停车场、餐厅 |
| 距离 | 距市中心或景点 |
| 排序 | 价格、评分、距离 |

### 酒店信息

| 详情 | 描述 |
|--------|-------------|
| 名称 | 酒店名称和品牌 |
| 地址 | 含地图的完整地址 |
| 照片 | 室内和室外图片 |
| 评分 | 星级和客人评分 |
| 价格 | 当地货币的每晚价格 |
| 设施 | 可用设施 |
| 评论 | 客人反馈和评论 |
| 联系方式 | 电话、邮箱、网站 |

---

## 天气预报

### 当前天气

查看目的地的实时天气：

| 数据 | 描述 |
|------|-------------|
| 温度 | 当前、最高、最低（摄氏/华氏） |
| 天气状况 | 晴、多云、雨等 |
| 湿度 | 百分比 |
| 风速 | 速度和方向 |
| 紫外线指数 | 日晒程度 |
| 日出/日落 | 每日日出日落时间 |

### 多日预报

通过多日预报提前规划：

| 天 | 温度 | 天气状况 | 降雨概率 |
|-----|-------------|-----------|-------------|
| 今天 | 25°C | 晴 | 10% |
| 明天 | 22°C | 多云 | 30% |
| 第 3 天 | 18°C | 雨 | 80% |
| 第 4 天 | 20°C | 阴 | 40% |
| 第 5 天 | 24°C | 晴 | 5% |

### 天气预警

应用显示天气预警和警告：

- 恶劣天气预警
- 极端温度
- 降水预警
- 空气质量指数

---

## 货币转换器

### 支持的货币

Travel Mate 支持超过 150 种货币的实时汇率：

| 货币 | 代码 | 符号 |
|----------|------|--------|
| 美元 | USD | $ |
| 欧元 | EUR | EUR |
| 英镑 | GBP | GBP |
| 日元 | JPY | JPY |
| 人民币 | CNY | CNY |
| 印度卢比 | INR | INR |
| 澳元 | AUD | AUD |
| 加元 | CAD | CAD |

### 使用转换器

1. 打开货币转换器工具
2. 选择源货币
3. 输入金额
4. 选择目标货币
5. 查看转换金额和汇率

### 功能

| 功能 | 描述 |
|---------|-------------|
| 实时汇率 | 更新的汇率 |
| 离线模式 | 离线使用的缓存汇率 |
| 汇率历史 | 查看汇率趋势 |
| 收藏夹 | 保存常用货币 |
| 快速转换 | 从任何屏幕转换 |

---

## 旅行清单

### 默认清单项目

Travel Mate 提供预建清单：

**证件：**
| 项目 | 优先级 |
|------|----------|
| 护照 | 必需 |
| 签证 | 如需要 |
| 旅行保险 | 必需 |
| 机票 | 必需 |
| 酒店预订 | 高 |
| 身份证 | 高 |
| 证件复印件 | 中 |

**衣物：**
| 项目 | 优先级 |
|------|----------|
| 内衣 | 必需 |
| 袜子 | 必需 |
| 衬衫/上衣 | 必需 |
| 裤子/短裤 | 必需 |
| 外套 | 视天气而定 |
| 舒适鞋 | 必需 |
| 睡衣 | 中 |

**电子产品：**
| 项目 | 优先级 |
|------|----------|
| 手机和充电器 | 必需 |
| 充电宝 | 高 |
| 适配器/转换器 | 必需 |
| 相机 | 可选 |
| 耳机 | 可选 |
| 笔记本电脑/平板 | 可选 |

**健康：**
| 项目 | 优先级 |
|------|----------|
| 药品 | 必需 |
| 急救包 | 高 |
| 防晒霜 | 视天气而定 |
| 驱虫剂 | 视目的地而定 |
| 免洗洗手液 | 中 |

### 自定义清单

为特定行程创建自定义清单：

1. 打开清单部分
2. 点击"创建新清单"
3. 命名清单
4. 添加带类别的项目
5. 设置项目优先级
6. 标记项目为已打包

---

## 地图和导航

### 离线地图

下载地图供离线使用：

1. 打开地图部分
2. 选择目的地区域
3. 点击"下载离线地图"
4. 选择地图详细程度
5. 等待下载完成

### 地图功能

| 功能 | 描述 |
|---------|-------------|
| 兴趣点 | 餐厅、景点、服务 |
| 导航 | 逐向导航 |
| 搜索 | 查找特定地点 |
| 书签 | 保存收藏地点 |
| 图层 | 卫星、地形、交通视图 |
| 离线模式 | 无网络使用 |

### 附近地点

发现当前位置附近的地点：

| 类别 | 示例 |
|----------|----------|
| 美食 | 餐厅、咖啡馆、快餐 |
| 购物 | 商场、市场、商店 |
| 服务 | ATM、药店、医院 |
| 景点 | 博物馆、公园、纪念碑 |
| 交通 | 车站、机场、出租车站 |

---

## 离线功能

### 可离线使用的功能

| 功能 | 离线支持 |
|---------|----------------|
| 行程安排 | 完全访问 |
| 城市指南 | 预下载内容 |
| 货币转换器 | 缓存汇率 |
| 清单 | 完全访问 |
| 地图 | 已下载区域 |
| 天气 | 上次获取的数据 |
| 酒店搜索 | 否（需要网络） |

### 下载离线内容

1. 打开设置
2. 导航到离线内容
3. 选择要下载的城市
4. 选择内容类型：
   - 城市指南文本
   - 景点详情
   - 地图
   - 图片
5. 监控下载进度

---

## 行程追踪

### 实时追踪

追踪您的行程进度：

| 功能 | 描述 |
|---------|-------------|
| 当前位置 | 地图上的 GPS 追踪 |
| 行驶距离 | 总覆盖距离 |
| 时间追踪 | 活动时长 |
| 路线历史 | 行程中的路线 |
| 照片 | 带地理标记的照片时间线 |

### 统计

行程完成后查看行程统计：

| 统计 | 描述 |
|-----------|-------------|
| 到访国家 | 国家数量 |
| 到访城市 | 城市数量 |
| 距离 | 总行驶距离 |
| 活动 | 完成的活动数量 |
| 照片 | 行程中拍摄的照片 |

---

## 配置

### 常规设置

| 设置 | 选项 | 默认值 |
|---------|---------|---------|
| 语言 | 20+ 种语言 | 英语 |
| 单位 | 公制、英制 | 公制 |
| 货币显示 | 符号、代码 | 符号 |
| 主题 | 亮色、暗色、自动 | 自动 |
| 通知 | 开、关 | 开 |

### 数据设置

| 设置 | 选项 | 默认值 |
|---------|---------|---------|
| 自动下载 | 仅 WiFi、始终、从不 | 仅 WiFi |
| 缓存大小 | 100MB、500MB、1GB | 500MB |
| 离线内容 | 选择城市 | 无 |
| 同步 | 手动、自动 | 手动 |

---

## 故障排除

### 常见问题

| 问题 | 解决方案 |
|-------|----------|
| 应用崩溃 | 清除缓存，更新到最新版本 |
| 地图加载失败 | 检查网络连接，重新下载地图 |
| 货币汇率过期 | 手动同步，检查网络 |
| GPS 不工作 | 启用位置权限 |
| 酒店搜索失败 | 验证日期和目的地 |

### 性能建议

1. **定期清除缓存** 以释放存储空间
2. **通过 WiFi 下载地图** 以节省流量
3. **保持应用更新** 以获取最新功能
4. **关闭后台应用** 以获得更好性能
5. **在连接不佳的区域使用离线模式**

---

## 总结

Travel Mate 是一款全面的旅行伴侣，将行程规划、城市指南、实用工具和离线功能整合在一个应用中。它简化了旅行准备，并通过货币转换、天气预报和交互式清单等功能增强了出行体验。该应用免费、开源，即使在没有网络连接的情况下也能工作。


---

## 来源：trip.md

## 简介

AdventureLog 是一款自托管的旅行记录应用程序，帮助您记录和组织您的冒险经历。它提供了一个现代化的界面来记录旅行、添加照片、跟踪位置和分享体验。

## 目录

1. [功能概览](#功能概览)
2. [安装](#安装)
3. [用户设置](#用户设置)
4. [创建冒险](#创建冒险)
5. [旅行管理](#旅行管理)
6. [照片与媒体](#照片与媒体)
7. [地图与位置](#地图与位置)
8. [共享与导出](#共享与导出)

## 功能概览

| 功能 | 说明 |
|------|------|
| 旅行记录 | 记录冒险详情 |
| 照片库 | 附加和组织照片 |
| 地图集成 | 在交互地图上查看位置 |
| 类别 | 按活动类型组织 |
| 标签 | 灵活的标签系统 |
| 天气跟踪 | 记录天气状况 |
| 时间线视图 | 按时间顺序的旅行历史 |
| 多用户 | 支持多用户 |

## 安装

### Docker Compose

```yaml
# docker-compose.yml
services:
  web:
    image: ghcr.io/seanmorley15/adventurelog:latest
    ports:
      - "8000:8000"
    environment:
      - SECRET_KEY=your-secret-key
      - POSTGRES_DB=adventurelog
      - POSTGRES_USER=adventurelog
      - POSTGRES_PASSWORD=adventurelog
      - POSTGRES_HOST=db
    depends_on:
      - db
    volumes:
      - media:/app/media

  db:
    image: postgres:15-alpine
    environment:
      - POSTGRES_DB=adventurelog
      - POSTGRES_USER=adventurelog
      - POSTGRES_PASSWORD=adventurelog
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  media:
  postgres_data:
```

### 环境变量

| 变量 | 说明 | 必需 |
|------|------|------|
| `SECRET_KEY` | Django 密钥 | 是 |
| `POSTGRES_DB` | 数据库名称 | 是 |
| `POSTGRES_USER` | 数据库用户 | 是 |
| `POSTGRES_PASSWORD` | 数据库密码 | 是 |
| `POSTGRES_HOST` | 数据库主机 | 是 |

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|------|----------|----------|
| CPU | 1 核 | 2 核 |
| 内存 | 512 MB | 1 GB |
| 存储 | 2 GB | 10 GB+ |
| Docker | 20.10+ | 最新 |

## 用户设置

### 注册

| 步骤 | 操作 |
|------|------|
| 1 | 访问应用 URL |
| 2 | 点击"注册" |
| 3 | 输入用户名和邮箱 |
| 4 | 设置密码 |
| 5 | 完成个人资料 |

### 用户资料

| 字段 | 说明 | 必需 |
|------|------|------|
| 用户名 | 显示名称 | 是 |
| 邮箱 | 联系邮箱 | 是 |
| 简介 | 简短描述 | 否 |
| 头像 | 个人照片 | 否 |
| 位置 | 家乡位置 | 否 |

## 创建冒险

### 冒险字段

| 字段 | 类型 | 说明 |
|------|------|------|
| 标题 | 文本 | 冒险名称 |
| 描述 | 富文本 | 详细笔记 |
| 日期 | 日期选择器 | 发生时间 |
| 位置 | 地图选择器 | 发生地点 |
| 类别 | 选择 | 活动类型 |
| 评分 | 1-5 星 | 体验评分 |
| 天气 | 选择 | 天气状况 |
| 可见性 | 公开/私有 | 共享设置 |

### 活动类别

| 类别 | 图标 | 示例 |
|------|------|------|
| 徒步 | 靴子 | 山间小径、自然漫步 |
| 露营 | 帐篷 | 营地、野外 |
| 旅行 | 飞机 | 度假、公路旅行 |
| 水上 | 船 | 皮划艇、帆船、海滩 |
| 冬季 | 雪花 | 滑雪、单板滑雪 |
| 城市 | 建筑 | 城市探索 |
| 美食 | 餐具 | 餐厅探访 |
| 其他 | 星星 | 杂项 |

### 添加新冒险

| 步骤 | 操作 |
|------|------|
| 1 | 点击"新冒险"按钮 |
| 2 | 填写标题和描述 |
| 3 | 使用日历设置日期 |
| 4 | 在地图上选择位置 |
| 5 | 选择类别和标签 |
| 6 | 如有可用则添加照片 |
| 7 | 设置评分和备注 |
| 8 | 保存冒险 |

### 富文本格式

| 格式 | 语法 | 结果 |
|------|------|------|
| 粗体 | `**text**` | **text** |
| 斜体 | `*text*` | *text* |
| 标题 | `## Heading` | 章节标题 |
| 列表 | `- item` | 项目列表 |
| 链接 | `[text](url)` | 超链接 |

## 旅行管理

### 组织冒险

| 方法 | 说明 |
|------|------|
| 类别 | 按类型自动分组 |
| 标签 | 自定义标签用于过滤 |
| 集合 | 将相关冒险分组 |
| 时间线 | 按时间顺序视图 |

### 编辑冒险

| 操作 | 方法 |
|------|------|
| 编辑 | 点击冒险 > 编辑 |
| 删除 | 冒险菜单 > 删除 |
| 复制 | 冒险菜单 > 复制 |
| 归档 | 冒险菜单 > 归档 |

### 过滤与搜索

| 过滤器 | 选项 |
|--------|------|
| 按类别 | 选择活动类型 |
| 按日期范围 | 开始和结束日期 |
| 按位置 | 基于地图的过滤 |
| 按标签 | 选择特定标签 |
| 按评分 | 最低星级 |
| 文本搜索 | 标题和描述 |

## 照片与媒体

### 照片上传

| 功能 | 详情 |
|------|------|
| 最大文件大小 | 可配置 |
| 支持格式 | JPEG, PNG, WebP |
| 多张上传 | 是，批量上传 |
| 拖放 | 支持 |
| 画廊视图 | 网格显示 |

### 照片管理

| 操作 | 方法 |
|------|------|
| 上传 | 拖放或文件选择器 |
| 重新排序 | 拖动到新位置 |
| 删除 | 点击照片上的 X |
| 设为封面 | 选择为主图 |
| 添加说明 | 编辑照片详情 |

### 照片存储

| 选项 | 配置 |
|------|------|
| 本地存储 | 默认，media 卷 |
| 外部存储 | S3 兼容存储 |
| 备份 | 定期文件备份 |

## 地图与位置

### 地图功能

| 功能 | 说明 |
|------|------|
| 交互地图 | 平移、缩放、点击 |
| 标记放置 | 点击设置位置 |
| 位置搜索 | 按地名搜索 |
| 聚合视图 | 分组附近标记 |
| 卫星视图 | 切换地图图层 |

### 位置数据

| 字段 | 说明 |
|------|------|
| 纬度 | GPS 坐标 |
| 经度 | GPS 坐标 |
| 地名 | 人类可读位置 |
| 国家 | 自动检测 |
| 地区 | 省/州 |

### 地图集成

| 提供商 | 特点 |
|--------|------|
| OpenStreetMap | 免费、社区驱动 |
| Mapbox | 样式化地图 |
| Google Maps | 熟悉界面 |

## 共享与导出

### 可见性设置

| 设置 | 说明 |
|------|------|
| 私有 | 仅您可见 |
| 公开 | 任何有链接的人 |
| 共享 | 特定用户 |

### 共享选项

| 方法 | 说明 |
|------|------|
| 直接链接 | 共享冒险 URL |
| 公开资料 | 共享所有公开冒险 |
| 社交媒体 | 分享到平台 |

### 导出格式

| 格式 | 内容 | 使用场景 |
|------|------|----------|
| JSON | 所有数据 | 备份、迁移 |
| GPX | 位置数据 | GPS 设备 |
| PDF | 格式化报告 | 打印、分享 |
| CSV | 表格数据 | 电子表格 |

### 备份与恢复

| 组件 | 位置 | 方法 |
|------|------|------|
| 数据库 | PostgreSQL 卷 | pg_dump |
| 媒体文件 | Media 卷 | 文件同步 |
| 配置 | 环境变量 | 单独记录 |

## 高级功能

### API 访问

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/adventures` | GET | 列出冒险 |
| `/api/adventures/:id` | GET | 获取冒险 |
| `/api/adventures` | POST | 创建冒险 |
| `/api/adventures/:id` | PUT | 更新冒险 |
| `/api/adventures/:id` | DELETE | 删除冒险 |

### 统计

| 指标 | 说明 |
|------|------|
| 总冒险数 | 所有旅行计数 |
| 按类别 | 按类型分类 |
| 按位置 | 访问的国家/地区 |
| 时间线 | 随时间的活动 |
| 距离 | 总距离（如已跟踪） |

### 集成选项

| 集成 | 用途 |
|------|------|
| Strava | 导入活动数据 |
| Google Fit | 健康数据 |
| Weather API | 自动填充天气 |
| Photo EXIF | 提取位置数据 |

## 总结

AdventureLog 提供了一个自托管的解决方案来记录和组织旅行体验。其直观的界面、照片管理、地图集成和灵活的组织功能使其适合个人旅行记录以及与朋友和家人分享冒险经历。


---

## 来源：canada.md

**来源：** https://github.com/brandonhimpfen/awesome-canada-travel

＃＃ 概述

本教程涵盖了 [brandonhimpfen/awesome-canada-travel](https://github.com/brandonhimpfen/awesome-canada-travel) 项目的关键资源和工具。

## 很棒的加拿大旅行

> 加拿大旅行的**资源、应用程序、社区、指南和工具**的精选列表 - 对于**独行旅行者**、**数字游牧民族**和**独立探险家**特别有帮助。

## 🇨🇦 一般旅行信息

- [Destination Canada](https://www.destinationcanada.com/) – 加拿大官方旅游营销机构。
- [Travel.gc.ca](https://travel.gc.ca/) – 加拿大政府旅行信息和建议。
- [Canada.ca Immigration](https://www.canada.ca/en/services/immigration-citizenship.html) – 签证、电子旅行许可和边境服务的官方网站。

## 🧳 独自旅行者资源

- [SoloTraveler.org](https://www.solotraveler.org) – 为加拿大和世界各地的单身旅行者提供提示、安全指南和目的地建议。
- [布兰登为独行旅行者策划的短名单](https://trips.solotraveler.org/) – 每月更新的无或低单人补充旅游列表。
- [独行旅行者的基本语言短语](https://www.solotraveler.org/essential-travel-phrases/) – 用于英语和法语交流的常见旅行短语。

## 🌎 加拿大的数字游牧民族

- [数字游牧者网络](https://www.digitalnomadsnetwork.org) – 一个由远程工作者和游牧者组成的社区，提供加拿大特定的内容。
- [在加拿大工作 (IRCC)](https://www.canada.ca/en/immigration-refugees-citizenship/services/work-canada.html) – 有关数字工作签证和远程工作合法性的信息。
- [Nomad List – 加拿大](https://nomadlist.com/canada) – 加拿大城市数字游牧者的排名、生活成本和评论。

## 🏘️ 住宿和共享居住

- [爱彼迎加拿大](https://www.airbnb.ca/)
- [TrustedHousesitters](https://www.trustedhousesitters.com/) – 非常适合在加拿大城市长期住宿。
- [Couchsurfing](https://www.couchsurfing.com/) – 结识当地人并免费住宿。
- [HomeExchange Canada](https://www.homeexchange.com/) – 与加拿大人跨省交换房屋。

## 🚆 交通

- [Via Rail](https://www.viarail.ca/) – 横跨加拿大的国家客运列车服务。
- [Rideshare Canada](https://www.ridesharing.com/) – 跨省的长途拼车列表。
- [Rome2Rio](https://www.rome2rio.com/) – 比较任意两个加拿大目的地之间的旅行选择。

## 🏞️ 著名景点

- **班夫和贾斯珀国家公园** – [加拿大公园](https://parks.canada.ca/)
- **魁北克市** – 一座迷人的法语城墙城市。
- **不列颠哥伦比亚省托菲诺** – 温哥华岛上的冲浪小镇，非常适合慢行。
- **新斯科舍省布雷顿角** – 风景优美的驾车路线、盖尔文化和徒步旅行。

## 🛠️ 工具和应用程序

- [公交应用程序](https://transitapp.com/) – 实时公共交通时刻表。
- [AllTrails](https://www.alltrails.com/canada) – 徒步旅行和自行车路线地图。
- [XE 货币](https://www.xe.com/) – 为旅行者提供的货币转换。
- [WeatherCAN](https://weather.gc.ca/) – 加拿大环境部官方天气预报。

## 📚 旅行指南和博客

- [加拿大孤独星球](https://www.lonelyplanet.com/canada)
- [独行旅行者旅行指南](https://www.solotraveler.org/travel-guides) – 为独行冒险家精心策划的旅行指南。
- [Nomadic Matt – 加拿大部分](https://www.nomadicmatt.com/travel-guides/canada-travel-tips/) – 预算提示和建议行程。

## 💬 在线社区

- [r/solotravel](https://reddit.com/r/solotravel)
- [r/CanadaTravel](https://reddit.com/r/CanadaTravel)
- [旅游博主网络（Facebook群组）](https://www.facebook.com/groups/travelbloggersnetwork)
- [数字游牧民族网络 (LinkedIn)](https://www.linkedin.com/groups/14396393/)

## 关键资源

|资源 |链接 |
|----------|------|
|目的地加拿大 | [https://www.destinationcanada.com/](https://www.destinationcanada.com/) |
| Travel.gc.ca | [https://travel.gc.ca/](https://travel.gc.ca/) |
|加拿大.ca 移民 | [https://www.canada.ca/en/services/immigration-citizenship.html](https://www.canada.ca/en/services/immigration-citizenship.html) |
| SoloTraveler.org | [https://www.solotraveler.org](https://www.solotraveler.org) |
|布兰登为独行旅行者精心策划的旅行清单| [https://trips.solotraveler.org/](https://trips.solotraveler.org/) |
|独自旅行者的基本语言短语| [https://www.solotraveler.org/essential-travel-phrases/](https://www.solotraveler.org/essential-travel-phrases/) |
|数字游牧民族网络| [https://www.digitalnomadsnetwork.org](https://www.digitalnomadsnetwork.org) |
|在加拿大工作 (IRCC) | [https://www.canada.ca/en/immigration-refugees-citizenship/services/work-canada.html](https://www.canada.ca/en/immigration-refugees-citizenship/services/work-canada.html) |
|游牧名单 - 加拿大 | [https://nomadlist.com/canada](https://nomadlist.com/canada) |
| Airbnb 加拿大 | [https://www.airbnb.ca/](https://www.airbnb.ca/) |
|值得信赖的房屋保姆 | [https://www.trustedhousesitters.com/](https://www.trustedhousesitters.com/) |
|沙发冲浪 | [https://www.couchsurfing.com/](https://www.couchsurfing.com/) |
|加拿大主页交换 | [https://www.homeexchange.com/](https://www.homeexchange.com/) |
|通过铁路 | [https://www.viarail.ca/](https://www.viarail.ca/) |
|加拿大乘车共享 | [https://www.ridesharing.com/](https://www.ridesharing.com/) |
|罗马2里约| [https://www.rome2rio.com/](https://www.rome2rio.com/) |
|加拿大公园| [https://parks.canada.ca/](https://parks.canada.ca/) |
|交通应用 | [https://transitapp.com/](https://transitapp.com/) |
|所有路线 | [https://www.alltrails.com/canada](https://www.alltrails.com/canada) |
| XE 货币 | [https://www.xe.com/](https://www.xe.com/) |
|天气CAN | [https://weather.gc.ca/](https://weather.gc.ca/) |
|加拿大孤独星球| [https://www.lonelyplanet.com/canada](https://www.lonelyplanet.com/canada) |
|独自旅行者旅行指南| [https://www.solotraveler.org/travel-guides](https://www.solotraveler.org/travel-guides) |
|游牧马特 – 加拿大部分 | [https://www.nomadicmatt.com/travel-guides/canada-travel-tips/](https://www.nomadicmatt.com/travel-guides/canada-travel-tips/) |
| r/独自旅行 | [https://reddit.com/r/solotravel](https://reddit.com/r/solotravel) |
| r/加拿大旅游 | [https://reddit.com/r/CanadaTravel](https://reddit.com/r/CanadaTravel) |
|旅游博主网络（Facebook 群组）| [https://www.facebook.com/groups/travelbloggersnetwork](https://www.facebook.com/groups/travelbloggersnetwork) |
|数字游牧民族网络 (LinkedIn) | [https://www.linkedin.com/groups/14396393/](https://www.linkedin.com/groups/14396393/) |
|独自旅行清单| [https://www.solotraveler.org/checklists/](https://www.solotraveler.org/checklists/) |
|旅行者的医学短语| [https://www.solotraveler.org/medical-travel-phrases/](https://www.solotraveler.org/medical-travel-phrases/) |



---
