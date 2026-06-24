# GnuCash：个人和小型企业会计

## 简介

GnuCash 是一款免费、开源的会计应用程序，适用于个人和小型企业。它实现了复式记账，并提供全面的财务管理工具。

| 属性 | 详情 |
|----------|--------|
| 仓库 | Gnucash/gnucash |
| 许可证 | GPL-2.0 |
| 语言 | C, C++, Scheme |
| 平台 | Windows, macOS, Linux |
| 文件格式 | XML, SQLite, MySQL/PostgreSQL |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install gnucash

# Fedora
sudo dnf install gnucash

# Flatpak
flatpak install org.gnucash.GnuCash
```

### macOS

```bash
brew install gnucash
```

### Windows

从 GnuCash 官方网站下载安装程序。

## 核心会计概念

GnuCash 基于复式记账原则构建，每笔交易至少影响两个账户。

| 概念 | 描述 |
|---------|-------------|
| Account（账户） | 跟踪特定类型资产、负债、收入或支出的记录 |
| Transaction（交易） | 借记一个账户并贷记另一个账户的财务事件 |
| Double Entry（复式记账） | 每笔交易都有相等的借方和贷方 |
| Balance（余额） | 账户中的净金额 |
| Reconciliation（对账） | 将记录与银行对账单匹配的过程 |

### 账户类型

| 账户类型 | 类别 | 描述 |
|--------------|----------|-------------|
| Asset（资产） | 资产负债表 | 您拥有的（现金、银行账户、投资） |
| Liability（负债） | 资产负债表 | 您欠的（贷款、信用卡） |
| Equity（权益） | 资产负债表 | 净资产（资产减去负债） |
| Income（收入） | 利润表 | 收到的钱（工资、销售收入） |
| Expense（费用） | 利润表 | 花出的钱（租金、食品、水电费） |

## 设置账簿

### 第 1 步：创建新文件

1. 打开 GnuCash。
2. 选择 文件 > 新建文件。
3. 选择您的货币和会计期间。

### 第 2 步：设置账户结构

| 账户 | 类型 | 描述 |
|---------|------|-------------|
| Assets:Bank:Checking | 资产 | 主要支票账户 |
| Assets:Bank:Savings | 资产 | 储蓄账户 |
| Assets:Cash | 资产 | 手头现金 |
| Liabilities:Credit Card | 负债 | 信用卡余额 |
| Liabilities:Mortgage | 负债 | 住房抵押贷款 |
| Equity:Opening Balance | 权益 | 期初权益 |
| Income:Salary | 收入 | 工作收入 |
| Income:Interest | 收入 | 银行利息 |
| Expenses:Food | 费用 | 食品杂货和餐饮 |
| Expenses:Rent | 费用 | 住房费用 |
| Expenses:Utilities | 费用 | 电费、水费、燃气费 |

### 第 3 步：输入期初余额

记录每个账户在会计起始日期的起始余额。

## 录入交易

### 基本交易录入

| 字段 | 描述 |
|-------|-------------|
| Date（日期） | 交易日期 |
| Description（描述） | 交易的简要说明 |
| Account（账户） | 被借记或贷记的账户 |
| Deposit/Credit（存款/贷方） | 添加到账户的金额 |
| Withdrawal/Debit（取款/借方） | 从账户中取出的金额 |

### 拆分交易

GnuCash 支持拆分交易，即单笔交易影响多个账户。

示例：一张扣除税款的工资单。

| 账户 | 借方 | 贷方 |
|---------|-------|--------|
| Assets:Bank:Checking | $3,000 | |
| Expenses:Taxes:Federal | $800 | |
| Expenses:Taxes:State | $200 | |
| Income:Salary | | $4,000 |

## 定期交易

GnuCash 可以自动创建经常性交易。

| 设置 | 描述 |
|---------|-------------|
| Frequency（频率） | 每日、每周、每月、每年 |
| Start Date（开始日期） | 计划开始时间 |
| End Date（结束日期） | 计划结束时间（或永不结束） |
| Reminders（提醒） | 创建交易前的提前通知 |

## 对账

对账账户可确保您的记录与银行对账单匹配。

| 状态 | 描述 |
|--------|-------------|
| Cleared (c)（已清算） | 交易与对账单匹配 |
| Reconciled (y)（已对账） | 正式对账完成 |
| Void（作废） | 交易已被作废 |
| Unreconciled (n)（未对账） | 尚未检查 |

## 财务报告

GnuCash 包含许多内置的财务报告。

| 报告 | 描述 |
|--------|-------------|
| Balance Sheet（资产负债表） | 资产、负债和权益的快照 |
| Income Statement（利润表） | 一段时间内的收入和费用 |
| Cash Flow（现金流量） | 现金流入和流出 |
| Account Summary（账户摘要） | 所有账户余额的摘要 |
| Budget Report（预算报告） | 实际金额与预算金额对比 |
| Tax Report（税务报告） | 按税务类别分类的收入和费用 |

## 预算

GnuCash 包含预算功能，用于规划和跟踪收入和费用。

| 预算功能 | 描述 |
|----------------|-------------|
| Create Budget（创建预算） | 为一个期间设置新预算 |
| Budget Amounts（预算金额） | 输入预期的收入和费用金额 |
| Budget Report（预算报告） | 比较实际金额与预算金额 |
| Rollover（结转） | 结转未使用的预算金额 |

## 多币种支持

| 功能 | 描述 |
|---------|-------------|
| Trading Accounts（交易账户） | 跟踪货币兑换的损益 |
| Exchange Rates（汇率） | 定义和更新汇率 |
| Currency Accounts（货币账户） | 为每个账户设置不同的货币 |

## 有效使用的技巧

| 技巧 | 说明 |
|-----|-------------|
| 定期录入 | 每天录入交易以保持最新 |
| 使用定期交易 | 自动化经常性条目 |
| 每月对账 | 每月将记录与银行对账单进行比较 |
| 备份文件 | 定期备份数据文件 |
| 使用子账户 | 按层次组织账户 |
| 设置报告 | 保存自定义报告配置 |

## 数据存储选项

| 存储 | 优点 | 缺点 |
|---------|------|------|
| XML 文件 | 简单、便携 | 大数据集较慢 |
| SQLite | 快速、单用户 | 不适合网络访问 |
| MySQL/PostgreSQL | 多用户访问 | 需要数据库服务器设置 |

## 结论

GnuCash 是一款成熟且功能强大的会计应用程序，免费提供专业级复式记账。它非常适合管理个人财务的个人和需要基本会计功能的小型企业。
