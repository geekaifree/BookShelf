# Actual Budget: 使用开源工具进行个人预算管理

## 简介

Actual Budget 是一款开源个人财务应用，帮助你追踪支出、管理预算和规划未来。与基于云端的替代方案不同，Actual Budget 将你的财务数据保存在自己的服务器上，同时提供受信封法启发的强大预算功能。

Actual Budget 注重隐私、简洁和准确。你的财务数据永远不会离开你的控制。

## 为什么使用 Actual Budget？

| 特性 | Actual Budget | 商业替代方案 |
|------|-------------|------------|
| 数据隐私 | 自托管 | 基于云端 |
| 费用 | 免费 | 月费订阅 |
| 开源 | 是 | 否 |
| 离线访问 | 是 | 通常需要网络 |
| 数据导出 | 完全控制 | 有限 |
| 自定义 | 完全访问 | 受限 |

## 核心概念

### 账户

账户代表你现实世界中的金融账户。

| 账户类型 | 描述 | 示例 |
|---------|------|------|
| 支票账户 | 日常交易 | 主要银行账户 |
| 储蓄账户 | 储备资金 | 应急基金 |
| 信用卡 | 债务追踪 | Visa、Mastercard |
| 现金 | 实物货币 | 钱包现金 |
| 投资 | 资产 | 证券账户 |
| 抵押贷款 | 贷款 | 住房抵押贷款 |

### 类别

类别将你的支出分组，遵循信封预算法。

| 类别组 | 示例类别 |
|-------|---------|
| 住房 | 房租、水电费、保险 |
| 食品 | 杂货、外出就餐 |
| 交通 | 油费、公共交通、车贷 |
| 健康 | 医生、药房、健身房 |
| 娱乐 | 流媒体、电影、书籍 |
| 储蓄 | 应急基金、度假 |

### 交易

每笔交易记录资金在账户之间的转移或支出。

| 字段 | 描述 | 示例 |
|------|------|------|
| 日期 | 交易日期 | 2026-06-15 |
| 收款人 | 收款方 | "杂货店" |
| 类别 | 预算类别 | "杂货" |
| 金额 | 交易金额 | -$45.67 |
| 账户 | 来源账户 | "支票账户" |
| 备注 | 附加信息 | "每周杂货" |

## 安装

### Docker 部署

```bash
# 拉取最新镜像
docker pull actualbudget/actual-server

# 创建数据目录
mkdir -p /data/actual-budget

# 使用 Docker 运行
docker run -d \
  --name actual-budget \
  -p 5006:5006 \
  -v /data/actual-budget:/data \
  actualbudget/actual-server
```

### Docker Compose

```yaml
version: '3'
services:
  actual:
    image: actualbudget/actual-server
    container_name: actual-budget
    restart: unless-stopped
    ports:
      - "5006:5006"
    volumes:
      - ./data:/data
```

### 系统要求

| 要求 | 最低 | 推荐 |
|------|------|------|
| 内存 | 512MB | 1GB |
| 存储 | 100MB | 1GB |
| CPU | 1 核 | 2 核 |
| 网络 | 端口 5006 | 带 SSL 的反向代理 |

## 快速上手

### 初始设置

1. 在浏览器中打开 `http://localhost:5006`
2. 创建新的预算文件
3. 设置你的第一个账户
4. 导入交易或手动添加

### 创建预算

| 步骤 | 操作 | 用途 |
|------|------|------|
| 1 | 定义收入来源 | 设置月收入 |
| 2 | 创建类别组 | 组织支出领域 |
| 3 | 添加类别 | 具体支出桶 |
| 4 | 设置预算金额 | 分配月度资金 |
| 5 | 追踪支出 | 记录交易 |

### 预算分配

| 类别 | 月预算 | 备注 |
|------|-------|------|
| 房租/抵押贷款 | $1,500 | 固定支出 |
| 杂货 | $400 | 可变 |
| 水电费 | $150 | 季节性变化 |
| 交通 | $200 | 油费 + 维护 |
| 外出就餐 | $100 | 自由裁量 |
| 储蓄 | $500 | 先付给自己 |

## 功能

### 信封预算法

信封法将你的收入分成每个类别的虚拟"信封"。

| 概念 | 描述 |
|------|------|
| 可用 | 已分配但未花费 |
| 已花费 | 已使用的金额 |
| 剩余 | 可用减去已花费 |
| 超支 | 花费超过可用 |
| 结转 | 未用资金转入下月 |

### 交易管理

| 功能 | 描述 |
|------|------|
| 手动输入 | 手动添加交易 |
| CSV 导入 | 导入银行对账单 |
| OFX 导入 | Open Financial Exchange 格式 |
| QIF 导入 | Quicken Interchange Format |
| 规则 | 自动分类交易 |
| 拆分 | 将一笔交易分配到多个类别 |

### 导入规则

规则自动分类和处理交易。

| 规则类型 | 示例 | 操作 |
|---------|------|------|
| 收款人包含 | "WALMART" | 设置类别为"杂货" |
| 金额大于 | $500 | 标记待审核 |
| 收款人匹配 | "NETFLIX" | 设置类别为"娱乐" |
| 日期范围 | 每月 1 号 | 设置为"房租" |

### 报表

| 报表 | 用途 | 洞察 |
|------|------|------|
| 净资产 | 追踪财富变化 | 财务健康趋势 |
| 支出 | 类别分解 | 资金去向 |
| 现金流 | 收入 vs 支出 | 月度结余 |
| 预算 | 计划 vs 实际 | 遵守情况追踪 |

## 服务器管理

### 备份策略

```bash
# 备份数据目录
cp -r /data/actual-budget /backup/actual-budget-$(date +%Y%m%d)

# 自动备份脚本
#!/bin/bash
BACKUP_DIR="/backup/actual-budget"
DATE=$(date +%Y%m%d)
tar -czf "$BACKUP_DIR/backup-$DATE.tar.gz" /data/actual-budget

# 仅保留最近 30 个备份
ls -t "$BACKUP_DIR"/backup-*.tar.gz | tail -n +31 | xargs rm -f
```

### 更新流程

```bash
# 拉取最新镜像
docker pull actualbudget/actual-server

# 停止并删除旧容器
docker stop actual-budget
docker rm actual-budget

# 启动新容器
docker run -d \
  --name actual-budget \
  -p 5006:5006 \
  -v /data/actual-budget:/data \
  actualbudget/actual-server
```

### 使用 Nginx 反向代理

```nginx
server {
    listen 443 ssl;
    server_name budget.yourdomain.com;

    ssl_certificate /etc/letsencrypt/live/budget.yourdomain.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/budget.yourdomain.com/privkey.pem;

    location / {
        proxy_pass http://localhost:5006;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

## 高级功能

### 自定义报表

创建自定义报表以追踪特定财务目标。

| 报表类型 | 配置 | 使用场景 |
|---------|------|---------|
| 类别趋势 | 按月折线图 | 追踪消费习惯 |
| 收款人分析 | 前 N 名收款人柱状图 | 识别最大支出 |
| 储蓄目标 | 目标进度 | 追踪目标完成 |
| 收入增长 | 月收入对比 | 职业发展 |

### 多币种支持

适用于处理多种货币的用户。

| 功能 | 描述 |
|------|------|
| 货币设置 | 每账户设置默认货币 |
| 汇率 | 手动或自动转换 |
| 多币种交易 | 处理外币购买 |
| 报表 | 以基础货币合并报表 |

## 安全考量

| 措施 | 实现 | 优先级 |
|------|------|-------|
| HTTPS | 使用 SSL 证书 | 关键 |
| 认证 | 强密码 | 关键 |
| 备份 | 定期自动备份 | 关键 |
| 网络 | 在私有网络上运行 | 高 |
| 更新 | 保持软件最新 | 高 |
| 访问控制 | 限制访问人员 | 高 |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|---------|---------|
| 无法连接 | 端口未开放 | 检查防火墙设置 |
| 性能缓慢 | 数据库过大 | 归档旧数据 |
| 导入错误 | 格式错误 | 验证 CSV/OFX 格式 |
| 同步问题 | 浏览器缓存 | 清除缓存并重新加载 |
| 缺少交易 | 导入过滤器 | 检查导入规则 |

## 更多资源

| 资源 | URL |
|------|-----|
| 官方网站 | actualbudget.org |
| GitHub | github.com/ActualBudget/actual |
| 文档 | actualbudget.org/docs |
| 社区论坛 | community.actualbudget.org |
