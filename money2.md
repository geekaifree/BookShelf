# Firefly III 教程：个人财务管理

## 简介

Firefly III 是一个自托管的财务管理应用，帮助追踪收入、支出、预算和财务目标。它提供复式记账法，配以用户友好的界面，用于个人财务管理。

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|---------|---------|
| PHP | 8.1 | 8.2+ |
| 内存 | 256 MB | 512 MB |
| 数据库 | MySQL 8.0 或 PostgreSQL 10 | PostgreSQL 15 |
| Web 服务器 | Apache 或 Nginx | Nginx |
| Node.js | 16 | 18 LTS |
| Composer | 2.x | 最新版 |

## 安装

### Docker Compose

```yaml
version: '3.8'
services:
  firefly:
    image: fireflyiii/core:latest
    ports:
      - "8080:8080"
    volumes:
      - ./upload:/var/www/html/storage/upload
    environment:
      - APP_KEY=SomeRandomStringOf32CharsExactly
      - APP_URL=http://localhost:8080
      - DB_CONNECTION=pgsql
      - DB_HOST=db
      - DB_PORT=5432
      - DB_DATABASE=firefly
      - DB_USERNAME=firefly
      - DB_PASSWORD=firefly
      - TRUSTED_PROXIES=**
    depends_on:
      - db
    restart: unless-stopped

  db:
    image: postgres:15
    volumes:
      - pg-data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=firefly
      - POSTGRES_USER=firefly
      - POSTGRES_PASSWORD=firefly
    restart: unless-stopped

volumes:
  pg-data:
```

### 生成 APP_KEY

```bash
head -c 32 /dev/urandom | base64
```

## 核心概念

| 概念 | 说明 |
|------|------|
| Asset Account（资产账户） | 你的银行账户、钱包、现金 |
| Expense Account（支出账户） | 资金去向（商家、服务商） |
| Revenue Account（收入账户） | 资金来源（雇主） |
| Liability（负债） | 你所欠的债务和贷款 |
| Transaction（交易） | 一笔财务事件 |
| Budget（预算） | 按类别的消费限额 |
| Piggy Bank（储蓄罐） | 储蓄目标追踪器 |
| Rule（规则） | 自动化交易处理 |

## 账户类型

| 类型 | 用途 | 示例 |
|------|------|------|
| 默认资产 | 支票和消费账户 | 银行账户、钱包 |
| 储蓄资产 | 储蓄账户 | 储蓄账户 |
| 现金资产 | 实体现金 | 手头现金 |
| 支出 | 收款方和供应商 | 杂货店、房东 |
| 收入 | 收入来源 | 雇主、自由职业客户 |
| 负债 | 所欠债务 | 房贷、信用卡 |
| 贷款 | 借给他人的钱 | 借给朋友的钱 |

### 创建账户

导航到 **Accounts > Create Account**：

| 字段 | 说明 | 示例 |
|------|------|------|
| 名称 | 账户名称 | "Main Checking" |
| 类型 | 账户类型 | Default Asset |
| 货币 | 账户货币 | USD |
| 期初余额 | 初始余额 | 1000.00 |
| 期初日期 | 余额日期 | 2024-01-01 |

## 交易类型

| 类型 | 说明 | 示例 |
|------|------|------|
| 支出（Withdrawal） | 资金离开账户 | 购买杂货 |
| 存入（Deposit） | 资金进入账户 | 工资支付 |
| 转账（Transfer） | 账户之间转移 | 从支票到储蓄 |
| 拆分（Split） | 多目标交易 | 一笔付款，多个类别 |

### 创建支出

| 字段 | 说明 | 示例 |
|------|------|------|
| 金额 | 交易金额 | 45.50 |
| 来源 | 你的资产账户 | Main Checking |
| 目标 | 支出账户 | Grocery Store |
| 日期 | 交易日期 | 2024-01-15 |
| 类别 | 预算类别 | Groceries |
| 描述 | 交易备注 | "Weekly groceries" |

### 拆分交易

拆分交易将一笔付款分配到多个类别：

| 拆分 | 金额 | 类别 | 预算 |
|------|------|------|------|
| 1 | $30.00 | Groceries | Food |
| 2 | $10.00 | Household | Home |
| 3 | $5.50 | Personal | Fun |
| **合计** | **$45.50** | | |

## 预算

### 预算结构

| 组件 | 说明 |
|------|------|
| 预算名称 | 消费类别名称 |
| 预算金额 | 每月或每周限额 |
| 自动预算 | 自动补充设置 |
| 预算限制 | 警报阈值金额 |

### 设置预算

| 预算 | 每月金额 | 自动预算规则 |
|------|---------|-------------|
| 杂货 | $500 | 每月 1 号补充 |
| 交通 | $200 | 每月 1 号补充 |
| 娱乐 | $100 | 每月 1 号补充 |
| 水电 | $300 | 每月 1 号补充 |
| 服装 | $75 | 每季度 1 号补充 |

### 预算监控

导航到 **Budgets** 查看消费指标：

| 指标 | 说明 |
|------|------|
| 已花费 | 当前周期已用金额 |
| 剩余 | 剩余预算余额 |
| 超支 | 超出预算的金额 |
| 周期 | 当前预算周期日期 |

## 类别和标签

| 类别 | 用途 |
|------|------|
| 杂货 | 食品购物 |
| 房租 | 住房付款 |
| 水电 | 电、水、气 |
| 保险 | 健康、汽车、房屋 |
| 餐饮 | 餐厅和外卖 |
| 娱乐 | 电影、游戏、爱好 |
| 交通 | 油费、公共交通 |
| 医疗 | 医疗费用 |

## 规则引擎

规则根据条件自动处理交易。

### 规则组件

| 组件 | 说明 |
|------|------|
| 触发器 | 何时激活（创建、更新或存储时） |
| 条件 | 在交易数据中匹配什么 |
| 操作 | 对交易进行什么更改 |

### 规则示例

| 规则名称 | 条件 | 操作 |
|---------|------|------|
| 自动分类 Amazon | 描述包含 "AMAZON" | 设置类别为 "Shopping" |
| 标记订阅 | 描述包含 "NETFLIX" | 添加标签 "subscription" |
| 预算分配 | 金额大于 100 | 设置预算为 "Large Purchases" |
| 自动确认 | 来源是 "Savings Account" | 标记为已确认 |

### 规则条件

| 条件 | 操作符 | 示例值 |
|------|--------|--------|
| 描述 | 包含 | "AMAZON" |
| 金额 | 大于 | 100.00 |
| 账户 | 精确是 | "Main Checking" |
| 类别 | 为空 | （无） |
| 日期 | 早于 | 2024-01-01 |
| 标签 | 包含 | "recurring" |

### 规则操作

| 操作 | 值 | 说明 |
|------|-----|------|
| 设置类别 | "Groceries" | 分配类别 |
| 添加标签 | "tax-deductible" | 添加标签 |
| 设置预算 | "Monthly" | 分配预算 |
| 设置描述 | "Updated text" | 更改描述 |
| 追加描述 | " extra info" | 添加到现有文本 |
| 清除标签 | （无） | 删除所有标签 |
| 标记为已确认 | （无） | 自动确认交易 |

## 储蓄罐（储蓄目标）

| 字段 | 说明 | 示例 |
|------|------|------|
| 名称 | 目标名称 | "Vacation Fund" |
| 目标金额 | 目标数额 | 2000.00 |
| 目标日期 | 截止日期 | 2024-12-31 |
| 账户 | 关联资产账户 | Savings Account |

### 储蓄罐操作

| 操作 | 说明 |
|------|------|
| 添加资金 | 向储蓄目标存款 |
| 取出资金 | 从储蓄目标取款 |
| 设置金额 | 设置确切的已存金额 |
| 查看进度 | 查看完成百分比 |

## 周期性交易

| 频率 | 说明 |
|------|------|
| 每天 | 每天 |
| 每周 | 每周 |
| 每月 | 每月 |
| 每季度 | 每 3 个月 |
| 每年 | 每年 |
| 自定义 | 特定天数间隔 |

### 设置周期性交易

| 字段 | 说明 | 示例 |
|------|------|------|
| 类型 | 交易类型 | Withdrawal |
| 金额 | 固定金额 | 1500.00 |
| 首次日期 | 开始日期 | 2024-01-01 |
| 重复频率 | 频率 | Monthly |
| 来源 | 来源账户 | Main Checking |
| 目标 | 目标账户 | Landlord |

## 数据导入

### 支持的导入格式

| 格式 | 来源 | 说明 |
|------|------|------|
| CSV | 大多数银行 | 通用格式 |
| CAMT.053 | 欧洲银行 | 基于 XML 的标准 |
| MT940 | SWIFT 网络 | 银行标准 |
| Spectre CSV | Salt Edge | 基于 API 的连接 |

### CSV 导入列映射

| CSV 列 | 映射到 | 示例 |
|--------|--------|------|
| Date | 交易日期 | "2024-01-15" |
| Description | 交易备注 | "AMAZON.COM" |
| Amount | 交易金额 | "-45.99" |
| Account | 来源或目标 | "Main Checking" |

## 报表

### 报表类型

| 报表 | 用途 | 显示数据 |
|------|------|---------|
| 收入 vs 支出 | 现金流分析 | 每月收入和支出 |
| 类别 | 消费明细 | 按类别 |
| 预算 | 预算表现 | 预算 vs 实际消费 |
| 账户 | 账户余额 | 余额随时间变化 |
| 净资产 | 总资产 | 净资产趋势 |
| 标签 | 基于标签的分析 | 按标签分组 |

## API 访问

### 认证

在 **Options > Profile > OAuth > Personal Access Tokens** 创建个人访问令牌。

### 常用 API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| `/api/v1/about` | GET | 系统信息 |
| `/api/v1/accounts` | GET / POST | 管理账户 |
| `/api/v1/transactions` | GET / POST | 管理交易 |
| `/api/v1/budgets` | GET / POST | 管理预算 |
| `/api/v1/categories` | GET / POST | 管理类别 |
| `/api/v1/rules` | GET / POST | 管理规则 |
| `/api/v1/piggy-banks` | GET / POST | 管理储蓄罐 |

### API 示例

```bash
curl -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  http://localhost:8080/api/v1/transactions
```

## 数据导入器

一个用于自动导入银行对账单的独立工具。

| 功能 | 说明 |
|------|------|
| Nordigen | 欧洲银行连接 |
| Spectre | 国际银行连接 |
| CSV 上传 | 手动文件上传 |
| 自动导入 | 计划定期导入 |

## 安全

| 措施 | 配置 |
|------|------|
| HTTPS | 使用 SSL 的反向代理 |
| 两步验证 | 在用户配置中启用 |
| API 令牌 | 个人访问令牌 |
| Recaptcha | 可选登录保护 |
| IP 限制 | Web 服务器配置 |
| 速率限制 | 基于代理的限制 |

## 备份

| 组件 | 方法 | 频率 |
|------|------|------|
| 数据库 | pg_dump 或 mysqldump | 每日 |
| 上传文件 | 文件复制 | 每日 |
| 环境 | 配置文件备份 | 每周 |
| .env | 安全复制 | 更改时 |

### 备份脚本

```bash
#!/bin/bash
DATE=$(date +%Y%m%d)
BACKUP_DIR="/var/backups/firefly"

pg_dump -U firefly firefly | gzip > "$BACKUP_DIR/db-$DATE.sql.gz"
tar -czf "$BACKUP_DIR/uploads-$DATE.tar.gz" /var/www/html/storage/upload
find "$BACKUP_DIR" -mtime +30 -delete
```

## 故障排除

| 问题 | 原因 | 解决方案 |
|------|------|---------|
| 500 错误 | APP_KEY 错误 | 生成新的 32 字符密钥 |
| 导入失败 | CSV 格式不匹配 | 检查列映射 |
| Cron 未运行 | Cron 设置错误 | 验证 cron 配置 |
| 报表缓慢 | 数据库性能 | 添加索引，优化查询 |
| 登录循环 | Cookie 或 APP_URL 问题 | 验证 APP_URL 设置 |

## 总结

Firefly III 是一个全面的个人财务管理器，具有复式记账、预算和自动化功能。其规则引擎、API 访问和导入能力使其成为追踪和管理个人财务的强大工具，同时拥有完全的数据所有权。
