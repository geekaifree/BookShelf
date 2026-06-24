# Beancount：纯文本复式记账

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
