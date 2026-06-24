# 使用 hledger 进行记账

## 简介

hledger 是一个基于复式记账法的纯文本记账工具。它使用简单的文本文件跟踪资金、时间或其他商品。本教程涵盖安装、日记账条目语法、常见工作流和报表。

## 复式记账基础

每笔交易记录账户间的等额借方和贷方：

| 概念 | 描述 | 示例 |
|------|------|------|
| 账户 | 跟踪值的类别 | Assets:Bank:Checking |
| 借方 | 交易的左侧 | 资金进入账户 |
| 贷方 | 交易的右侧 | 资金离开账户 |
| 余额 | 借方减贷方的总和 | 当前账户价值 |

### 账户类型

| 类型 | 正常余额方向 | 示例 |
|------|-------------|------|
| 资产 | 借方 | 现金、银行账户、投资 |
| 负债 | 贷方 | 信用卡、贷款、抵押贷款 |
| 权益 | 贷方 | 所有者权益、留存收益 |
| 收入 | 贷方 | 工资、自由职业收入 |
| 费用 | 借方 | 食品、房租、水电 |

## 安装

### 包管理器

| 平台 | 命令 |
|------|------|
| macOS (Homebrew) | `brew install hledger` |
| Ubuntu/Debian | `apt install hledger` |
| Fedora | `dnf install hledger` |
| Windows (Scoop) | `scoop install hledger` |
| Cabal | `cabal install hledger` |
| Stack | `stack install hledger` |

### 验证安装

```bash
hledger --version
hledger --help
```

## 日记账文件格式

日记账文件是核心数据文件，使用 `.journal` 或 `.hledger` 扩展名。

### 基本交易语法

```
YYYY/MM/DD description
    account1    amount
    account2    amount
```

### 交易示例

```
2026/01/15 Grocery Store
    Expenses:Food:Groceries    $85.50
    Assets:Bank:Checking

2026/01/16 Monthly Salary
    Assets:Bank:Checking       $4,500.00
    Revenue:Salary

2026/01/17 Electric Bill
    Expenses:Utilities:Electric  $120.00
    Liabilities:CreditCard
```

## 账户命名约定

使用冒号创建分层账户名称：

| 结构 | 示例 | 用途 |
|------|------|------|
| 类型:详情 | Assets:Bank | 顶层分组 |
| 类型:详情:子类 | Assets:Bank:Checking | 具体账户 |
| 类型:详情:子类:备注 | Expenses:Food:Groceries:Weekly | 详细跟踪 |

### 推荐的账户层级

```
Assets
  Assets:Bank:Checking
  Assets:Bank:Savings
  Assets:Cash
  Assets:Investments

Liabilities
  Liabilities:CreditCard
  Liabilities:Loans:Student
  Liabilities:Mortgage

Equity
  Equity:OpeningBalances

Revenue
  Revenue:Salary
  Revenue:Freelance

Expenses
  Expenses:Food:Groceries
  Expenses:Food:Dining
  Expenses:Housing:Rent
  Expenses:Utilities:Electric
  Expenses:Transport:Gas
```

## 常见交易模式

### 收入

```
2026/01/15 Paycheck
    Assets:Bank:Checking       $3,000.00
    Revenue:Salary
```

### 现金消费

```
2026/01/15 Coffee Shop
    Expenses:Food:Dining       $5.50
    Assets:Cash
```

### 信用卡消费

```
2026/01/15 Online Purchase
    Expenses:Shopping           $49.99
    Liabilities:CreditCard
```

### 账户间转账

```
2026/01/15 Transfer to Savings
    Assets:Bank:Savings        $500.00
    Assets:Bank:Checking
```

### 信用卡还款

```
2026/01/15 Credit Card Payment
    Liabilities:CreditCard     $1,200.00
    Assets:Bank:Checking
```

## 多币种交易

hledger 支持多种商品：

```
2026/01/15 Currency Exchange
    Assets:Bank:USD            $1,000.00
    Assets:Bank:EUR            @ 920.00 EUR

2026/01/16 Stock Purchase
    Assets:Investments:AAPL    10 AAPL @ $150.00
    Assets:Bank:Checking
```

### 价格记法

| 记法 | 含义 | 示例 |
|------|------|------|
| `@` | 单价 | `10 AAPL @ $150` |
| `@@` | 总价 | `10 AAPL @@ $1500` |

## 基本命令

### 余额报表

```bash
# 显示所有账户余额
hledger balance

# 显示特定账户余额
hledger balance assets

# 限制显示深度
hledger balance --depth 2

# 月度余额报表
hledger balance --monthly
```

### 收益表

```bash
# 收入和支出
hledger incomestatement

# 月度收益表
hledger incomestatement --monthly

# 特定期间
hledger incomestatement --period "last quarter"
```

### 资产负债表

```bash
# 资产、负债、权益
hledger balancesheet

# 带日期
hledger balancesheet --end 2026/01/31
```

### 明细账报表

```bash
# 所有交易
hledger register

# 按账户筛选
hledger register expenses:food

# 月度汇总
hledger register --monthly expenses
```

## 筛选和查询

### 日期筛选

| 语法 | 示例 | 描述 |
|------|------|------|
| `date:YYYY` | `date:2026` | 整年 |
| `date:YYYY/MM` | `date:2026/01` | 特定月份 |
| `date:YYYY/MM/DD` | `date:2026/01/15` | 特定日期 |
| `date:>YYYY` | `date:>2025/12/31` | 日期之后 |
| `date:<YYYY` | `date:<2026/02/01` | 日期之前 |
| 范围 | `date:2026-01-01..2026-06-30` | 日期范围 |

### 账户筛选

```bash
# 按账户名称筛选
hledger balance food

# 排除账户
hledger balance not:income

# 正则匹配
hledger balance expenses:~food|transport
```

### 金额筛选

```bash
# 超过 $100 的交易
hledger register "amt:>100"

# 低于 $50 的交易
hledger register "amt:<50"
```

## 期间表达式

| 表达式 | 含义 |
|--------|------|
| `this month` | 当前日历月 |
| `last month` | 上一日历月 |
| `this year` | 当前日历年 |
| `last year` | 上一日历年 |
| `this quarter` | 当前季度 |
| `last 3 months` | 过去 3 个月 |
| `2026/1..2026/6` | 2026 年 1 月至 6 月 |

```bash
# 过去 3 个月的报表
hledger balance --period "last 3 months"

# 年初至今
hledger incomestatement --period "this year"
```

## CSV 导入

hledger 可以从 CSV 文件导入交易。

### CSV 规则文件

创建 `bank.csv.rules`：

```
# Skip header line
skip 1

# Column mapping
fields date, description, amount

# Account assignment
account1 Assets:Bank:Checking
account2 Expenses:Unknown

# Description-based rules
if Groceries
    account2 Expenses:Food:Groceries

if Electric
    account2 Expenses:Utilities:Electric
```

### 执行导入

```bash
hledger import bank.csv --rules-file bank.csv.rules
```

## 预算管理

hledger 支持使用周期交易进行预算跟踪：

```
~ monthly
    (budget:food:groceries)      $400.00
    (budget:utilities:electric)  $150.00
    (budget:transport)           $200.00
```

### 预算报表

```bash
# 显示预算与实际对比
hledger balance --budget

# 月度预算报表
hledger balance --budget --monthly

# 特定预算账户
hledger balance --budget food
```

## 输出格式

| 格式 | 参数 | 使用场景 |
|------|------|----------|
| 文本 | （默认） | 终端查看 |
| CSV | `-O csv` | 电子表格导入 |
| HTML | `-O html` | 网页查看 |
| JSON | `-O json` | 程序化使用 |
| SQL | `-O sql` | 数据库导入 |

```bash
# 导出为 CSV
hledger balance -O csv > balances.csv

# 导出为 HTML
hledger incomestatement -O html > report.html
```

## 配置文件

创建 `~/.hledger.conf` 设置默认值：

```
# Default journal file
--file ~/finance/2026.journal

# Default output format
--output-format html

# Default date format
--date-format %Y-%m-%d
```

## 常见工作流

### 月度对账

| 步骤 | 命令 | 目的 |
|------|------|------|
| 1 | `hledger balance assets:bank:checking` | 检查记录的余额 |
| 2 | 与银行对账单对比 | 验证准确性 |
| 3 | 添加缺失交易 | 完善记录 |
| 4 | `hledger check` | 验证分录平衡 |

### 年终报表

| 报表 | 命令 | 目的 |
|------|------|------|
| 年度收入 | `hledger incomestatement -p 2026` | 总收入和支出 |
| 净资产 | `hledger balancesheet -e 2027/01/01` | 资产与负债 |
| 支出分类 | `hledger balance expenses -p 2026` | 消费类别 |
