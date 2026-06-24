# 财务管理

> 本文档整合了以下源文件：accounting.md, hledger.md, ledger.md, finance.md, money.md, money2.md, budget.md

---

## 来源：accounting.md

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


---

## 来源：hledger.md

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


---

## 来源：ledger.md

## 简介

Beancount 是一个将财务数据存储在纯文本文件中的复式记账系统。它使用领域特定语言来定义账户、交易和余额。结合 Fava Web 界面，它提供了完整的会计解决方案。本教程涵盖语法、工作流程和实际用法。

## 为什么选择纯文本记账

| 优势 | 描述 |
|------|------|
| 版本控制 | 使用 Git 跟踪变更 |
| 可移植性 | 文件是人类可读的文本 |
| 自动化 | 可编写脚本生成交易 |
| 透明性 | 所有逻辑在源文件中可见 |
| 可重现性 | 从源文件产生确定性结果 |

## 安装

### 使用 pip

```bash
pip install beancount
pip install fava  # Web UI
```

### 使用 Homebrew（macOS）

```bash
brew install beancount
```

### 验证安装

```bash
bean-check --version
fava --version
```

## 文件结构

典型的 Beancount 项目结构如下：

```
accounting/
  main.beancount       # 根文件，包含其他文件
  accounts.beancount   # 账户定义
  commodities.beancount # 商品定义
  2024/
    2024-01.beancount  # 一月交易
    2024-02.beancount  # 二月交易
```

根文件包含其他文件：

```beancount
option "title" "Personal Finances"
option "operating_currency" "USD"

include "accounts.beancount"
include "commodities.beancount"
include "2024/*.beancount"
```

## 账户类型

Beancount 使用五种标准账户类型。

| 类型 | 前缀 | 正常余额 | 描述 |
|------|------|----------|------|
| Assets | `Assets:` | 借方 | 你拥有的 |
| Liabilities | `Liabilities:` | 贷方 | 你欠的 |
| Income | `Income:` | 贷方 | 收到的钱 |
| Expenses | `Expenses:` | 借方 | 花掉的钱 |
| Equity | `Equity:` | 贷方 | 净资产 |

### 定义账户

```beancount
2024-01-01 open Assets:Checking
2024-01-01 open Assets:Savings
2024-01-01 open Assets:Investments:Stocks
2024-01-01 open Liabilities:CreditCard
2024-01-01 open Liabilities:Mortgage
2024-01-01 open Income:Salary
2024-01-01 open Income:Dividends
2024-01-01 open Expenses:Food
2024-01-01 open Expenses:Rent
2024-01-01 open Expenses:Transport
2024-01-01 open Equity:Opening-Balances
```

## 交易

### 基本交易

```beancount
2024-01-15 * "Grocery Store" "Weekly groceries"
  Expenses:Food          52.30 USD
  Assets:Checking       -52.30 USD
```

交易必须平衡为零。每笔借方都有相等的贷方。

### 交易组件

| 组件 | 描述 | 必填 |
|------|------|------|
| 日期 | `YYYY-MM-DD` 格式 | 是 |
| 标志 | `*`（完成）或 `!`（待处理） | 是 |
| 收款方 | 付款或收款对象 | 否 |
| 描述 | 交易描述 | 是 |
| 分录 | 带金额的账户条目 | 是 |

### 多方交易

```beancount
2024-01-20 * "Restaurant" "Dinner with friends"
  Expenses:Food          80.00 USD
  Expenses:Food          20.00 USD
  Assets:Checking       -60.00 USD
  Liabilities:CreditCard -40.00 USD
```

### 货币转换

```beancount
2024-02-01 * "Exchange" "Convert USD to EUR"
  Assets:EUR             500.00 EUR @ 1.08 USD
  Assets:Checking       -540.00 USD
```

## 商品

### 声明商品

```beancount
2024-01-01 commodity USD
  name: "US Dollar"
  asset-class: "cash"

2024-01-01 commodity AAPL
  name: "Apple Inc."
  asset-class: "equity"
```

### 价格条目

跟踪投资的市场价格。

```beancount
2024-01-15 price AAPL  185.50 USD
2024-02-15 price AAPL  190.25 USD
2024-03-15 price AAPL  178.00 USD
```

## 指令

### 其他指令

| 指令 | 用途 | 示例 |
|------|------|------|
| `txn` | 替代交易语法 | `txn "Description"` |
| `balance` | 断言账户余额 | `2024-01-31 balance Assets:Checking 1000 USD` |
| `pad` | 插入平衡交易 | `2024-01-01 pad Assets:Checking Equity:Opening-Balances` |
| `note` | 附加元数据 | `2024-01-15 note Assets:Checking "Bank statement"` |
| `document` | 链接到文件 | `2024-01-15 document Assets:Checking "statement.pdf"` |
| `event` | 跟踪生活事件 | `2024-01-01 event "location" "New York"` |
| `custom` | 插件特定数据 | 用于插件的自定义指令 |

## 余额断言

验证账户余额是否与预期值匹配。

```beancount
2024-01-31 balance Assets:Checking  1500.00 USD
2024-01-31 balance Assets:Savings  10000.00 USD
```

如果余额不匹配，Beancount 在验证期间会报告错误。

## 元数据

为交易和账户附加任意键值数据。

```beancount
2024-03-01 * "Amazon" "Office supplies"
  Expenses:Office:Supplies   45.99 USD
  Liabilities:CreditCard    -45.99 USD
  receipt: "receipt_20240301.pdf"
  category: "business"
```

## 标签

使用标签对交易进行分类。

```beancount
2024-04-01 * "Travel Agent" "Flight to Tokyo" #travel #business
  Expenses:Travel:Flights   1200.00 USD
  Assets:Checking          -1200.00 USD
```

### 按标签查询

```bash
bean-query main.beancount "SELECT date, narration, account, amount WHERE '#travel' in tags"
```

## 插件

### 交易插件

自动处理交易。

```beancount
plugin "beancount.plugins.implicit_prices"
plugin "beancount.plugins.auto_accounts"
```

| 插件 | 用途 |
|------|------|
| `implicit_prices` | 从交易生成价格条目 |
| `auto_accounts` | 自动打开交易中使用的账户 |
| `category_tag` | 根据账户名称添加标签 |

## 运行查询

### 命令行查询

```bash
# 检查错误
bean-check main.beancount

# 运行查询
bean-query main.beancount "SELECT date, narration, account, amount"

# 导出为 CSV
bean-query main.beancount "SELECT date, account, amount" > output.csv
```

### 查询示例

```sql
-- 今年所有支出
SELECT date, account, amount
WHERE account ~ 'Expenses' AND date >= 2024-01-01

-- 按支出类别汇总
SELECT account, SUM(amount) as total
WHERE account ~ 'Expenses'
GROUP BY account

-- 超过 $100 的交易
SELECT date, payee, narration, amount
WHERE amount > 100
```

## Fava Web 界面

### 启动 Fava

```bash
fava main.beancount
```

在浏览器中打开 http://localhost:5000。

### Fava 功能

| 功能 | 描述 |
|------|------|
| 利润表 | 收入和支出 |
| 资产负债表 | 资产、负债、净资产 |
| 试算表 | 所有账户余额 |
| 日记账 | 按时间顺序的交易列表 |
| 查询 | 在浏览器中运行 BQL 查询 |
| 导入器 | CSV 和对账单导入 |

## 常用工作流程

### 记录工资存入

```beancount
2024-01-31 * "Employer" "January salary"
  Assets:Checking       5000.00 USD
  Income:Salary        -5000.00 USD
```

### 支付信用卡账单

```beancount
2024-02-01 * "Bank" "Credit card payment"
  Liabilities:CreditCard  1500.00 USD
  Assets:Checking        -1500.00 USD
```

### 记录投资购买

```beancount
2024-03-01 * "Broker" "Buy AAPL shares"
  Assets:Investments:Stocks    10 AAPL @ 185.00 USD
  Assets:Checking            -1850.00 USD
```

### 拆分交易

```beancount
2024-03-15 * "Grocery Store" "Shopping"
  Expenses:Food           40.00 USD
  Expenses:Household      15.00 USD
  Assets:Checking        -55.00 USD
```

## 导入数据

### CSV 导入配置

```python
# importer.py
from beancount.ingest import importer
from beancount.core import data

class MyImporter(importer.ImporterProtocol):
    def identify(self, file):
        return 'bank_name' in file.name

    def extract(self, file, existing_entries=None):
        entries = []
        # 解析 CSV 并创建条目
        return entries
```

## 错误检查

| 错误类型 | 描述 | 解决方案 |
|----------|------|----------|
| 不平衡 | 借方 != 贷方 | 修正金额或添加缺失分录 |
| 余额违规 | 断言余额不匹配 | 验证交易或断言 |
| 未入账 | 转换缺少价格 | 添加价格条目或使用 @ 语法 |
| 重复 | 同日期两条余额断言 | 删除重复项 |

## 总结

Beancount 使用纯文本文件提供了强大的复式记账系统。定义账户、记录交易、断言余额，并使用简洁的领域特定语言查询财务数据。使用 Fava 进行可视化，使用命令行工具进行自动化和报告。将你的财务记录与代码一起进行版本控制。


---

## 来源：finance.md

## 简介

HomeBank 是一款免费、易于使用的个人财务应用程序。它帮助用户管理银行账户、跟踪收入和支出、创建预算和生成财务报告。

| 属性 | 详情 |
|----------|--------|
| 仓库 | HomeBank/homebank |
| 许可证 | GPL-2.0 |
| 语言 | C, GTK |
| 平台 | Windows, macOS, Linux |
| 文件格式 | XML (.xhb) |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install homebank

# Fedora
sudo dnf install homebank

# Flatpak
flatpak install org.homebank.HomeBank
```

### macOS

```bash
brew install homebank
```

### Windows

从 HomeBank 官方网站下载安装程序。

## 核心概念

| 概念 | 描述 |
|---------|-------------|
| Account（账户） | 银行账户、信用卡或现金钱包 |
| Transaction（交易） | 单次财务操作（收入、支出、转账） |
| Category（类别） | 交易分类（食品、租金、工资） |
| Payee（收款方） | 交易所涉及的个人或实体 |
| Budget（预算） | 一段时间内某个类别的计划金额 |
| Tag（标签） | 用于灵活分组的附加标签 |

## 设置账户

### 创建第一个账户

1. 打开 HomeBank 并选择 账户 > 添加。
2. 输入账户名称、银行名称和货币。
3. 设置初始余额和对账单余额。
4. 选择账户类型。

| 账户类型 | 描述 |
|--------------|-------------|
| Bank（银行） | 标准支票或储蓄账户 |
| Cash（现金） | 现金钱包 |
| Credit Card（信用卡） | 信用卡账户 |
| Asset（资产） | 投资或房产 |
| Liability（负债） | 贷款或债务 |

### 账户属性

| 属性 | 描述 |
|----------|-------------|
| Name（名称） | 账户的显示名称 |
| Bank（银行） | 关联的金融机构 |
| Currency（货币） | 交易使用的货币 |
| Initial Balance（初始余额） | 账户开户时的起始余额 |
| Statement Balance（对账单余额） | 银行对账单上的最新已知余额 |

## 管理交易

### 添加交易

| 字段 | 描述 |
|-------|-------------|
| Date（日期） | 交易日期 |
| Payee（收款方） | 交易对象 |
| Category（类别） | 收入或支出类型 |
| Amount（金额） | 交易金额 |
| Memo（备注） | 可选说明 |
| Tags（标签） | 可选标签 |
| Status（状态） | 已清算、已对账或未对账 |

### 交易状态

| 状态 | 符号 | 描述 |
|--------|--------|-------------|
| None（无） | 空 | 已输入但未验证的交易 |
| Cleared（已清算） | c | 已由银行确认 |
| Reconciled（已对账） | R | 已与银行对账单匹配 |

### 导入交易

HomeBank 可以从各种文件格式导入交易。

| 格式 | 描述 |
|--------|-------------|
| OFX/QFX | 开放金融交换（大多数银行） |
| QIF | Quicken 交换格式 |
| CSV | 逗号分隔值（可自定义） |
| MT940 | SWIFT 标准格式 |

导入方法：文件 > 导入，然后选择下载的银行文件。

### 导入规则

创建规则以自动分类导入的交易。

| 规则字段 | 描述 |
|------------|-------------|
| Payee Pattern（收款方模式） | 收款方字段中要匹配的文本 |
| Category（类别） | 匹配时要分配的类别 |
| Memo（备注） | 要添加的附加文本 |
| Amount Range（金额范围） | 按交易金额过滤 |

## 类别和收款方

### 类别结构

HomeBank 支持两级层次结构的类别。

| 主类别 | 子类别 |
|---------------|---------------|
| Income（收入） | Salary, Bonus, Interest, Refund |
| Housing（住房） | Rent, Mortgage, Repairs, Insurance |
| Food（食品） | Groceries, Restaurants, Coffee |
| Transport（交通） | Gas, Public Transit, Parking, Maintenance |
| Utilities（水电） | Electric, Water, Gas, Internet, Phone |
| Health（健康） | Doctor, Pharmacy, Insurance, Gym |
| Entertainment（娱乐） | Movies, Books, Games, Hobbies |
| Shopping（购物） | Clothing, Electronics, Gifts |

### 管理收款方

创建交易时收款方会自动保存。可以通过收款管理对话框进行编辑或合并。

## 预算

### 创建预算

1. 打开 预算 > 添加。
2. 选择预算周期（每周、每月、每年）。
3. 为每个类别设置金额。
4. 跟踪预算执行情况。

| 预算列 | 描述 |
|---------------|-------------|
| Category（类别） | 费用类别 |
| Planned（计划） | 预算金额 |
| Actual（实际） | 实际花费金额 |
| Difference（差异） | 计划减去实际 |

### 预算技巧

| 技巧 | 说明 |
|-----|-------------|
| 从历史数据开始 | 审查前几个月以设定现实的预算 |
| 包含储蓄 | 将储蓄作为费用列入预算 |
| 每月审查 | 根据实际支出调整预算 |
| 使用类别 | 保持类别一致以实现准确跟踪 |

## 报告和分析

### 可用报告

| 报告 | 描述 |
|--------|-------------|
| Statistics（统计） | 按类别显示收入和费用的条形图 |
| Budget（预算） | 预算金额与实际金额的比较 |
| Balance（余额） | 随时间变化的余额 |
| Car Cost（车辆费用） | 车辆相关费用 |
| Payments（付款） | 即将到期的定期交易 |

### 统计过滤器

| 过滤器 | 描述 |
|--------|-------------|
| Date Range（日期范围） | 选择要分析的期间 |
| Accounts（账户） | 选择要包含的账户 |
| Categories（类别） | 按特定类别过滤 |
| Payees（收款方） | 按特定收款方过滤 |
| Tags（标签） | 按标签过滤 |

## 定期交易

HomeBank 可以安排定期交易以自动化常规付款。

| 设置 | 描述 |
|---------|-------------|
| Payee（收款方） | 定期交易的收款方 |
| Amount（金额） | 固定金额 |
| Frequency（频率） | 每周、每月、每年或自定义 |
| Next Date（下次日期） | 下次到期时间 |
| Auto Insert（自动插入） | 自动添加到账户 |

## 多币种

| 功能 | 描述 |
|---------|-------------|
| Currency List（货币列表） | 定义带汇率的货币 |
| Account Currency（账户货币） | 为每个账户分配货币 |
| Conversion（转换） | 以基础货币查看总计 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 定期导入 | 每周下载并导入银行对账单 |
| 一致使用类别 | 保持支出有条理以获得准确报告 |
| 每月对账 | 将交易与银行对账单匹配 |
| 用标签管理特殊项目 | 单独跟踪度假或装修费用 |
| 备份文件 | 定期保存 .xhb 文件的副本 |

## 键盘快捷键

| 快捷键 | 操作 |
|----------|--------|
| Ctrl+N | 新建交易 |
| Ctrl+I | 导入交易 |
| Ctrl+S | 保存更改 |
| Ctrl+F | 查找交易 |
| Ctrl+R | 生成报告 |

## 结论

HomeBank 是一款简单直接的个人财务应用程序，涵盖了资金管理的基本要素。其简洁的界面和导入功能使跟踪财务变得轻松，没有不必要的复杂性。


---

## 来源：money.md

## 简介

KMyMoney 是一个基于 KDE 平台构建的个人财务管理器。它提供了一套全面的工具，用于管理账户、跟踪收入和支出以及生成财务报告。

| 属性 | 详情 |
|----------|--------|
| 仓库 | KDE/kmymoney |
| 许可证 | GPL-2.0 |
| 语言 | C++, Qt |
| 平台 | Windows, macOS, Linux |
| 文件格式 | XML (.kmy), SQLite, MySQL |

## 安装

### Linux

```bash
# Ubuntu/Debian
sudo apt install kmymoney

# Fedora
sudo dnf install kmymoney

# Flatpak
flatpak install org.kde.kmymoney
```

### macOS

```bash
brew install kmymoney
```

### Windows

从 KDE 下载页面下载安装程序。

## 核心概念

| 概念 | 描述 |
|---------|-------------|
| Account（账户） | 财务账户（银行、信用卡、现金、投资） |
| Transaction（交易） | 资金在账户间转移的记录 |
| Category（类别） | 收入和支出的分类 |
| Payee（收款方） | 与您交易的个人或组织 |
| Schedule（计划） | 定期交易模板 |
| Institution（机构） | 金融机构（银行、券商） |

### 账户类型

| 类型 | 描述 |
|------|-------------|
| Checking（支票） | 日常银行账户 |
| Savings（储蓄） | 带利息的银行账户 |
| Credit Card（信用卡） | 循环信用账户 |
| Cash（现金） | 现金钱包 |
| Investment（投资） | 券商或退休账户 |
| Loan（贷款） | 抵押贷款、汽车贷款或个人贷款 |
| Asset（资产） | 房产或贵重物品 |
| Liability（负债） | 债务和义务 |

## 入门

### 第 1 步：创建新文件

1. 启动 KMyMoney。
2. 选择 文件 > 新建。
3. 选择文件名和位置。
4. 设置基础货币。

### 第 2 步：配置机构

添加您的金融机构以按提供商组织账户。

| 字段 | 描述 |
|-------|-------------|
| Name（名称） | 机构名称 |
| BIC | 银行识别码 |
| Routing Number（路由号码） | 银行路由号码（美国） |

### 第 3 步：创建账户

| 字段 | 描述 |
|-------|-------------|
| Name（名称） | 账户名称 |
| Type（类型） | 上述列表中的账户类型 |
| Institution（机构） | 关联的金融机构 |
| Currency（货币） | 账户货币 |
| Opening Balance（期初余额） | 起始余额 |

## 管理交易

### 录入交易

| 字段 | 描述 |
|-------|-------------|
| Date（日期） | 交易日期 |
| Payee（收款方） | 交易对象 |
| Category（类别） | 收入或支出类别 |
| Amount（金额） | 交易金额 |
| Memo（备注） | 可选说明 |
| Number（编号） | 支票或参考编号 |
| Status（状态） | 已清算、已对账或未标记 |

### 交易状态

| 状态 | 图标 | 描述 |
|--------|------|-------------|
| Not Marked（未标记） | 空 | 新录入 |
| Cleared（已清算） | C | 已由银行确认 |
| Reconciled（已对账） | R | 已与对账单匹配 |
| Void（作废） | V | 已取消的交易 |

### 拆分交易

拆分交易允许将单笔交易分配到多个类别。

| 类别 | 金额 |
|----------|--------|
| Groceries | $50.00 |
| Household | $25.00 |
| Personal Care | $15.00 |
| **总计** | **$90.00** |

## 网上银行

KMyMoney 支持从金融机构导入交易。

| 导入格式 | 描述 |
|---------------|-------------|
| OFX/QFX | 开放金融交换 |
| QIF | Quicken 交换格式 |
| CSV | 逗号分隔值 |
| MT940 | SWIFT 标准 |
| CAMT.053 | SEPA 信用转账 |

### 设置网上银行

1. 进入机构设置。
2. 输入您的网上银行凭据。
3. 配置连接参数。
4. 下载交易。

## 定期交易

定期交易可以安排以自动化常规付款。

| 设置 | 描述 |
|---------|-------------|
| Name（名称） | 计划名称 |
| Frequency（频率） | 每周、双周、每月、每年 |
| Start Date（开始日期） | 计划开始时间 |
| End Date（结束日期） | 结束时间（或永不结束） |
| Next Due（下次到期） | 下次发生日期 |
| Auto Enter（自动录入） | 到期时自动入账 |
| Remind（提醒） | 到期日前显示提醒 |

## 投资跟踪

KMyMoney 提供基本的投资组合管理。

| 功能 | 描述 |
|---------|-------------|
| Securities（证券） | 跟踪股票、债券、共同基金 |
| Prices（价格） | 下载或手动输入价格 |
| Performance（表现） | 跟踪投资回报 |
| Dividends（股息） | 记录股息收入 |
| Capital Gains（资本收益） | 计算已实现收益 |

### 添加证券

| 字段 | 描述 |
|-------|-------------|
| Name（名称） | 证券名称 |
| Symbol（代码） | 股票代码 |
| Type（类型） | 股票、债券、共同基金等 |
| Market（市场） | 交易的交易所 |

## 预算

### 创建预算

1. 进入 工具 > 预算。
2. 为财年创建新预算。
3. 为每个月设置类别金额。
4. 跟踪实际支出与预算支出。

| 预算视图 | 描述 |
|-------------|-------------|
| Monthly（月度） | 按月查看预算 |
| Yearly（年度） | 年度概览 |
| Category（类别） | 按类别分解预算 |

## 报告

KMyMoney 包含各种财务报告。

| 报告 | 描述 |
|--------|-------------|
| Net Worth（净资产） | 随时间变化的资产减负债 |
| Income/Expenses（收入/费用） | 现金流量报告 |
| Balance Sheet（资产负债表） | 某一时间点的财务快照 |
| Category Report（类别报告） | 按类别显示支出 |
| Payee Report（收款方报告） | 按收款方显示支出 |
| Tax Report（税务报告） | 税务相关交易 |
| Investment Performance（投资表现） | 投资回报 |

### 自定义报告

| 设置 | 描述 |
|---------|-------------|
| Date Range（日期范围） | 要包含的期间 |
| Accounts（账户） | 要包含哪些账户 |
| Categories（类别） | 按类别过滤 |
| Chart Type（图表类型） | 折线图、柱状图或饼图 |

## 技巧和最佳实践

| 技巧 | 说明 |
|-----|-------------|
| 每天录入交易 | 保持记录准确和最新 |
| 一致使用类别 | 使报告更有意义 |
| 每月对账 | 及早发现错误 |
| 安排定期付款 | 自动化常规交易 |
| 备份文件 | 防止数据丢失 |
| 使用子类别 | 按层次组织类别 |
| 设置收款方 | 通过自动完成加快交易录入 |

## 数据管理

| 操作 | 描述 |
|-----------|-------------|
| Backup（备份） | 文件 > 备份创建压缩存档 |
| Restore（恢复） | 文件 > 恢复从备份中恢复 |
| Export（导出） | 将数据导出为 QIF 或 CSV |
| Encrypt（加密） | 为数据文件设置密码保护 |

## 结论

KMyMoney 是一个强大的个人财务管理器，将复式记账与用户友好的功能相结合。它非常适合希望对财务数据进行详细控制并偏好桌面应用程序的个人。


---

## 来源：money2.md

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


---

## 来源：budget.md

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


---
