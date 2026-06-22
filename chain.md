# 加密货币教程


## 一、核心安全法则

| 法则 | 含义 |
|------|------|
| **零信任** | 保持怀疑，始终保持怀疑 |
| **持续验证** | 对怀疑的点有能力去验证，并养成习惯 |

---

## 二、整体流程概览

加密货币安全涉及三大流程：

```
创建钱包 → 备份钱包 → 使用钱包
```

每个流程都有对应的安全要点，下文逐一展开。

---

## 三、创建钱包

### 3.1 核心概念

钱包的核心是**私钥**（或**助记词**）。

| 类型 | 示例 |
|------|------|
| 私钥 | `0xa164d4767469de4faf09793ceea07d5a2f5d3cef7f6a9658916c581829ff5584` |
| 助记词 | `cruel weekend spike point innocent dizzy alien use evoke shed adjust wrong` |

**关键原则**：私钥即身份。私钥丢失或被盗 = 身份丧失。

### 3.2 钱包分类

| 类型 | 说明 | 特点 |
|------|------|------|
| PC 钱包 | 桌面端应用 | 功能丰富，需注意系统安全 |
| 浏览器扩展钱包 | 如 MetaMask | 便捷，需从官方商店下载 |
| 移动端钱包 | 手机 App | 随身携带，注意应用商店分区 |
| 硬件钱包 | 如 Ledger、Trezor | 离线存储私钥，安全性高 |
| 网页钱包 | 在线使用 | 风险最高，不建议长期使用 |

按联网状态分为：

| 类型 | 说明 |
|------|------|
| 冷钱包 | 不联网，安全性高 |
| 热钱包 | 联网，使用便捷 |

**安全原则**：做好隔离，鸡蛋不要放在一个篮子里。

### 3.3 下载安全

**问题**：许多人找不到正确官网，安装了假钱包。

**验证官网的方法**：

| 方法 | 说明 |
|------|------|
| Google 搜索 | 注意搜索结果中的广告条目不可靠 |
| CoinMarketCap | 行业知名收录平台 |
| 多方验证 | 询问多个可信来源，互相佐证 |

**文件完整性校验**：

| 方式 | 说明 |
|------|------|
| 哈希校验 | 使用 SHA256 验证文件未被篡改 |
| GPG 签名校验 | 使用 GPG 工具验证签名 |

**各平台下载注意事项**：

| 平台 | 注意事项 |
|------|----------|
| PC 钱包 | 下载后做完整性校验 |
| 浏览器扩展 | 查看用户数、评分，如 MetaMask 超千万用户 |
| 移动端 | iPhone 注意 App Store 分区，中国区可能下不到正版 |
| 硬件钱包 | 从官网购买，到手后检查是否被拆封 |
| 网页钱包 | 尽量避免使用，如必须则速战速决 |

### 3.4 助记词标准

助记词遵循 BIP39 标准：

| 规格 | 说明 |
|------|------|
| 单词数量 | 12/15/18/21/24 个（3 的倍数，不超过 24） |
| 常用数量 | 12 位（安全性足够），24 位（如 Ledger） |
| 语言 | 英文、中文、日文、韩文等 |
| 词表 | 固定 2048 个单词 |

**创建时注意事项**：

- 确保身边无人、无摄像头等偷窥风险
- 确认助记词随机性足够
- 如作为冷钱包使用，可考虑断网创建

### 3.5 Keyless 方案

| 类型 | 说明 | 示例 |
|------|------|------|
| Custodial（托管） | 用户不拥有私钥，依托中心化平台 | 中心化交易所 |
| Non-Custodial（非托管） | 用户掌握类似私钥的权力，但非直接私钥 | MPC 方案、Cloud 托管 |

**MPC（安全多方计算）优势**：

- 私钥从不出现，通过多方计算解决单点风险
- 一套方案可通用多链多签
- 结合知名云平台，安全与体验兼顾

**MPC 代表项目**：ZenGo、Fireblocks、Safeheron

---

## 四、备份钱包

### 4.1 备份类型

| 类型 | 说明 | 风险 |
|------|------|------|
| **明文** | 直接记录助记词 | 可考虑乱序或替换单词，但需牢记规律 |
| **带密码** | 助记词 + 密码生成种子 | 密码也需备份，忘记则无法恢复 |
| **多签** | 多人签名授权才能使用 | 避免单点风险，但管理复杂 |
| **SSS** | 秘密共享方案，分片存储 | 恢复需指定数量分片 |

**SSS 参考**：
- Keystone SSS 指南: https://guide.keyst.one/zh/docs/shamir-backup
- Trezor SSS 指南: https://wiki.trezor.io/Shamir_backup

### 4.2 加密与备份位置

**加密建议**：使用 GPG 加密后存储备份。

**备份位置**：

| 位置 | 说明 | 注意事项 |
|------|------|----------|
| **Cloud** | Google、Apple、微软等云服务 | 加密后再上传，GPG 私钥和密码也要备份 |
| **Paper** | 纸质/钢板抄写 | 寿命长于电子设备，存放在安全位置 |
| **Device** | 电脑、U盘、移动硬盘等 | 每年至少检查一次，传输用 AirDrop/USB |
| **Brain** | 脑记 | 存在记忆淡忘/错乱风险，存在意外风险 |

**灾备原则**：

- 避免单点风险
- 重要数据多处备份
- 设有灾备人

**定期验证**：根据安全法则"持续验证"，定期检查备份是否可用。

---

## 五、使用钱包

### 5.1 AML（反洗钱）

持有的加密货币可能存在 AML 风险：

| 风险 | 说明 |
|------|------|
| 资金来源不干净 | 交易对手的币可能涉及非法活动 |
| 链上冻结 | USDT 等可被发行方冻结 |

**USDT 冻结查询**：
- 在 Etherscan USDT 合约的 `isBlackListed` 输入地址查询
- 地址: https://etherscan.io/token/0xdac17f958d2ee523a2206206994597c13d831ec7#readContract

**防御建议**：选择口碑好的平台和个人作为交易对手。

### 5.2 冷钱包使用

**接收**：配合观察钱包（如 imToken、OneKey、Trust Wallet）即可。

**发送流程**：

```
Light App（联网）→ 待签名内容 → 冷钱包（离线签名）→ 签名内容 → Light App → 广播上链
```

传输方式：QRCode、USB、Bluetooth。

**冷钱包风险**：

| 风险 | 说明 |
|------|------|
| 目标地址被替换 | 坏人生成头尾相似的地址进行替换 |
| 无限授权 | 未限制 approve 数量，代币可被转走 |
| 盲签陷阱 | 签名内容不透明，藏有恶意操作 |
| 信息展示不足 | 冷钱包屏幕有限，可能遗漏关键信息 |

**核心原则**：所见即所签。

### 5.3 热钱包使用

热钱包在冷钱包风险基础上，额外存在**助记词/私钥被盗风险**。

**热钱包版本风险**：

| 作恶方式 | 说明 |
|----------|------|
| 助记词上传 | 恶意代码将助记词打包上传到黑客服务器 |
| 替换转账信息 | 后台偷偷替换目标地址和金额 |
| 破坏随机数 | 让生成的助记词容易被破解 |

**安全建议**：对存有重要资产的钱包，不做轻易更新，够用就好。

### 5.4 DeFi 安全

DeFi 安全至少包括七个方面：

| 方面 | 说明 |
|------|------|
| 智能合约安全 | 安全审计的核心切入点 |
| 区块链基础安全 | 共识账本、虚拟机安全 |
| 前端安全 | 防止页面被篡改、注入恶意代码 |
| 通信安全 | HTTPS、防中间人攻击 |
| 人性安全 | 防止内部作恶、社会工程学 |
| 金融安全 | 防止不公平启动、巨鲸攻击、闪电贷攻击等 |
| 合规安全 | AML、KYC、制裁地区限制等 |

#### 智能合约权限风险

**问题**：项目方权限过大可能作恶。

**缓解方案**：

| 方案 | 说明 | 示例 |
|------|------|------|
| Timelock（时间锁） | 关键操作延迟执行，用户有时间反应 | Compound 的 48 小时时间锁 |
| 多签 | 多人签名才能执行关键操作 | Gnosis Safe |

**注意**：多签和 Timelock 都可能存在"皇帝的新衣"问题——表面合规，实际有后门。

#### 前端安全风险

| 风险类型 | 说明 |
|----------|------|
| 内部作恶 | 开发人员替换合约地址或植入钓鱼脚本 |
| 供应链作恶 | 第三方依赖被植入后门 |
| 远程 JS 作恶 | 引入的外部 JavaScript 文件被篡改 |

**防御机制**：使用 SRI（Subresource Integrity）完整性校验。

```html
<script src="https://example.com/lib.js" integrity="sha384-..." crossorigin="anonymous"></script>
```

参考：https://developer.mozilla.org/zh-CN/docs/Web/Security/Subresource_Integrity

#### 通信安全

**核心规则**：遇到 HTTPS 证书错误，立即停止访问。

**历史案例**：2018 年 MyEtherWallet 遭 BGP 劫持，用户忽略证书错误后私钥被盗。

**项目方应配置 HSTS**（HTTP Strict Transport Security），强制浏览器在证书错误时阻止访问。

### 5.5 NFT 安全

NFT 在 DeFi 安全基础上，额外关注：

| 方面 | 说明 |
|------|------|
| Metadata 安全 | 图片 URI 应使用 IPFS/Arweave 等去中心化存储 |
| 签名安全 | 防止盲签导致 NFT 被盗 |

**Metadata 标准参考**：https://docs.opensea.io/docs/metadata-standards

### 5.6 签名安全

**最大原则**：所见即所签。

**盲签问题**：

MetaMask 弹出的签名窗口显示信息有限（账户、余额、来源网站、签名消息），用户无法判断签名的真实含义。

**历史事件**：2022 年 2 月 OpenSea 集中爆发 NFT 被盗事件，根因是用户盲签。

**防御措施**：

| 措施 | 说明 |
|------|------|
| 拒绝盲签 | 确保了解签名内容的真实含义 |
| 使用 EIP-712 | 结构化签名，显示可读内容 |
| 取消授权 | 使用工具检查并取消不必要的授权 |

**授权检查/取消工具**：

| 工具 | 地址 |
|------|------|
| Token Approvals（Etherscan） | https://etherscan.io/tokenapprovalchecker |
| Revoke.cash | https://revoke.cash/ |
| Rabby 钱包 | https://rabby.io/ |

### 5.7 反常识签名风险

**问题**：不同链的签名机制不同，跨链时容易因惯性思维中招。

**案例**：Solana 上的授权钓鱼

- 恶意合约在用户 Approve 后可转走原生资产（SOL）
- 这在以太坊上不可能（以太坊授权只能钓走 Token，不能钓走 ETH）
- Phantom 钱包在"所见即所签"上存在缺陷

**教训**：跨链时不要用惯性思维，需了解目标链的特殊机制。

### 5.8 高级攻击方式

| 攻击方式 | 说明 |
|----------|------|
| 邮件钓鱼 | 附带恶意文档（Office 宏/0day），植入木马 |
| 钱包替换 | 木马将 MetaMask 替换为有后门的版本 |
| 域名钓鱼 | 使用 Punycode 注册相似域名（如 trezor 的变体） |
| Cloudflare Workers 劫持 | 控制项目方 Cloudflare 账号后注入恶意脚本 |
| XSS/CSRF/Reverse Proxy | 结合多种 Web 攻击技巧 |

**木马常见功能**：

| 功能 | 说明 |
|------|------|
| 凭证采集 | 浏览器密码、SSH 密钥等 |
| 键盘记录 | 采集密码等敏感输入 |
| 截屏/文件采集 | 获取敏感信息 |
| 钱包定向攻击 | 替换钱包应用、篡改转账信息 |

---

## 六、传统隐私保护

### 6.1 操作系统

| 系统 | 建议 |
|------|------|
| Windows 10+ | 安全性足够，及时更新 |
| macOS | 安全性足够，及时更新 |
| Linux | 适合高级用户，如 Ubuntu、Tails、Whonix |

**安全措施**：

| 措施 | 说明 |
|------|------|
| 系统更新 | 有安全更新立即安装 |
| 杀毒软件 | 卡巴斯基、BitDefender 等 |
| 磁盘加密 | Windows: BitLocker；macOS: FileVault |
| BIOS/固件密码 | 防止物理接触后的攻击 |

### 6.2 手机

| 平台 | 建议 |
|------|------|
| iPhone | 安全性较高，建议使用 |
| Android | 安全性逐步改善，注意版本碎片化 |

**注意事项**：

- 不要越狱/Root
- 不从非官方市场下载 App
- 云同步需确保账号安全

### 6.3 网络

| 建议 | 说明 |
|------|------|
| 不连陌生 Wi-Fi | 优先使用 4G/5G |
| HTTPS 优先 | 遇到证书错误立即停止 |
| 敏感设备独立网络 | 高安全需求时考虑 |

### 6.4 浏览器

| 建议 | 说明 |
|------|------|
| 及时更新 | 有更新就安装 |
| 谨慎安装扩展 | 来自官方商店，查看口碑和用户量 |
| 浏览器隔离 | 重要操作用一个浏览器，日常用另一个 |
| 隐私扩展 | uBlock Origin、HTTPS Everywhere、ClearURLs 等 |

### 6.5 密码管理器

**推荐工具**：1Password、Bitwarden

| 工具 | 特点 |
|------|------|
| 1Password | 闭源，安全审计报告公开，支持 2FA |
| Bitwarden | 全开源（含服务端），可自行验证 |

**注意事项**：

- 千万别忘记主密码
- 确保注册邮箱安全
- 做好 2FA 备份

### 6.6 双因素认证（2FA）

| 工具 | 说明 |
|------|------|
| Google Authenticator | 最常用 |
| Microsoft Authenticator | 微软出品 |
| 1Password | 自带 2FA 功能 |

**注意**：2FA 丢失很麻烦，务必做好备份。

### 6.7 邮箱

| 类型 | 推荐 |
|------|------|
| 主流邮箱 | Gmail、Outlook、QQ 邮箱 |
| 隐私邮箱 | ProtonMail、Tutanota（用于敏感服务注册） |

**安全提醒**：

- 警惕邮件中的钓鱼链接和附件
- 长期不活跃的免费邮箱可能被回收

### 6.8 SIM 卡

**风险**：SIM Port Attack（SIM 卡转移攻击）

攻击者通过社会工程学获取用户隐私，到运营商骗取新 SIM 卡，进而接管用户账号。

**防御措施**：

| 措施 | 说明 |
|------|------|
| 启用 2FA | 使用独立 2FA 工具，不依赖短信验证码 |
| SIM 卡 PIN 码 | 设置 SIM 卡密码，防止手机丢失后被使用 |

### 6.9 GPG

**概念区分**：

| 名称 | 说明 |
|------|------|
| PGP | 商用加密软件，在赛门铁克麾下 |
| OpenPGP | 加密标准，衍生自 PGP |
| GPG (GnuPG) | 基于 OpenPGP 的开源加密软件 |

**用途**：

- 文件加密（备份钱包时使用）
- 签名验证（验证下载文件完整性）

**入门参考**：https://www.ruanyifeng.com/blog/2013/07/gpg.html

### 6.10 隔离环境

**核心思想**：零信任思维，被黑时损失仅限于被黑目标。

| 隔离方式 | 说明 |
|----------|------|
| 密码隔离 | 不同账号使用不同密码 |
| 钱包隔离 | 不同用途使用不同钱包 |
| 设备隔离 | 敏感操作与日常操作分开 |
| 虚拟机 | 使用 VMware、Parallels 等 |

---

## 七、人性安全

### 7.1 Telegram 风险

| 风险 | 说明 |
|------|------|
| 假客服私聊 | 任意私聊是 Telegram 机制，无需好友 |
| 群克隆 | 拉你进群，除你之外全是仿冒账号 |
| 钓鱼 Bot | 定制化 Bot 服务进行诈骗 |

### 7.2 Discord 风险

**核心风险**：Discord Token

- Discord Token 是 HTTP 请求头中的 authorization 字段
- 拿到 Token 即可几乎完全控制目标账号
- **2FA 对此攻击无效**

**防御措施**：

- 不急不贪、多方验证
- 如中招，立即更改 Discord 密码（Token 会刷新）

### 7.3 来自"官方"的钓鱼

| 手法 | 说明 |
|------|------|
| 域名后缀不同 | 如 trezor.us 代替 trezor.io |
| Punycode | 使用 Unicode 相似字符，如特殊字符代替正常字母 |
| 邮件伪造 | SPF 配置问题导致的邮件伪造 |
| 内部人作恶 | 项目方人员安全意识差 |

### 7.4 Web3 隐私问题

将各种 Web3 项目玩一遍后，碎片信息可拼出完整画像：

- 收藏哪些 NFT
- 加入哪些社群
- 在哪些白名单里
- 绑定了哪些 Web2 账号
- 活跃时间段

**建议**：谨慎对待新事物，保持隔离身份的好习惯。

---

## 八、电脑中毒应急处理

### 常见投毒手法

| 手法 | 说明 |
|------|------|
| 假会议软件 | 假装投资人/记者/HR，诱导安装 |
| Telegram Safeguard | 诱导黏贴恶意代码运行 |
| Cloudflare 验证 | 诱导黏贴恶意代码运行 |

### 中毒后处理步骤

| 步骤 | 操作 |
|------|------|
| 1. 转移资金 | 钱包内资金立即安全转移 |
| 2. 更改密码 | 所有重要账号改密码、改 2FA，排查未知登录 |
| 3. 查杀病毒 | 使用 AVG/Bitdefender/Kaspersky/Malwarebytes |
| 4. 重置系统 | 如不放心，备份重要文件后重置电脑 |

**注意**：Mac 电脑同样可能中毒，不限于 Windows。

---

## 九、被盗应急处理

### 9.1 止损

| 阶段 | 操作 |
|------|------|
| 眼前阶段 | 抢着转移剩余资产，联系冻结，联系中心化平台风控 |
| 控制后阶段 | 防止二次、三次伤害 |

### 9.2 保护现场

| 操作 | 说明 |
|------|------|
| 断网不关机 | 联网设备立即断网，保持电源供电 |
| 等待取证 | 除非自己有能力，否则等待专业安全人员 |

### 9.3 分析原因

**事故报告要素**：

| 要素 | 内容 |
|------|------|
| 概要 1 | 什么人、什么时间、什么事、总损失 |
| 概要 2 | 钱包地址、黑客地址、币种、数量（表格形式） |
| 过程描述 | 事故过程细节，输出黑客画像 |

### 9.4 追踪溯源

| 类型 | 内容 |
|------|------|
| 链上情报 | 资金走向分析、交易所/混币平台监控 |
| 链下情报 | IP、设备信息、邮箱、行为信息 |

### 9.5 需要掌握的能力

- 智能合约安全分析及取证
- 链上资金转移分析及取证
- Web/服务器/系统安全分析及取证
- 恶意代码分析及取证
- 人员安全分析及取证

---

## 十、常见误区

| 误区 | 真相 |
|------|------|
| **Code Is Law** | 被黑或跑路时，受害者最终依赖真法律 |
| **Not Your Keys, Not Your Coins** | 拿到私钥却驾驭不好，币反而更危险；大平台有时更安全 |
| **In Blockchain We Trust** | 不是所有区块链都安全，人性是最大突破点 |
| **密码学安全 = 安全** | 密码学安全不等于系统安全，攻击面远不止密码学 |
| **被黑很丢人** | 被黑是 100% 普遍现象，丢人的是傲慢 |
| **立即更新总是对的** | 更新可能引入新问题；重要钱包不做轻易更新 |

---

## 十一、安全法则与原则汇总

### 两大法则

| 法则 | 含义 |
|------|------|
| 零信任 | 保持怀疑，始终保持怀疑 |
| 持续验证 | 有能力验证怀疑的点，养成习惯 |

### 安全原则

| 原则 | 说明 |
|------|------|
| 多源验证 | 网络知识参考至少两个来源，互相佐证 |
| 隔离 | 鸡蛋不放在一个篮子里 |
| 谨慎更新 | 重要资产钱包不做轻易更新 |
| 所见即所签 | 签名内容与预期一致 |
| 及时更新系统 | 系统安全更新立即安装 |
| 不乱下载 | 杜绝大多数风险 |

---

## 十二、推荐资源

### 官方网站

| 项目 | 地址 |
|------|------|
| SlowMist | https://www.slowmist.com |
| CoinMarketCap | https://coinmarketcap.com/ |
| MetaMask | https://metamask.io/ |
| imToken | https://token.im/ |
| Trust Wallet | https://trustwallet.com/ |
| OneKey | https://onekey.so/ |
| Rabby | https://rabby.io/ |
| Ledger | https://www.ledger.com/ |
| Trezor | https://trezor.io/ |
| Keystone | https://keyst.one/ |
| Gnosis Safe | https://gnosis-safe.io/ |
| ZenGo | https://zengo.com/ |
| Fireblocks | https://www.fireblocks.com/ |
| Safeheron | https://www.safeheron.com/ |
| Phantom | https://phantom.app/ |
| EdgeWallet | https://edge.app/ |
| MyEtherWallet | https://www.myetherwallet.com/ |
| OpenSea | https://opensea.io/ |
| Revoke.cash | https://revoke.cash/ |
| Compound | https://compound.finance/ |
| SushiSwap | https://www.sushi.com/ |
| Tornado Cash | https://tornado.cash/ |
| Binance | https://www.binance.com/ |
| Coinbase | https://coinbase.com |

### 安全工具

| 工具 | 地址 | 用途 |
|------|------|------|
| Scam Sniffer | https://www.scamsniffer.io/ | 钓鱼检测 |
| Wallet Guard | https://www.walletguard.app/ | 钱包安全扩展 |
| Pocket Universe | https://www.pocketuniverse.app/ | 交易安全 |
| 1Password | https://1password.com/ | 密码管理 |
| Bitwarden | https://bitwarden.com/ | 密码管理（开源） |
| Google Authenticator | https://support.google.com/accounts/answer/1066447 | 2FA |
| Microsoft Authenticator | https://www.microsoft.com/en-us/security/mobile-authenticator-app | 2FA |

### 杀毒软件

| 软件 | 地址 |
|------|------|
| AVG | https://www.avg.com/ |
| Bitdefender | https://www.bitdefender.com/ |
| Kaspersky | https://www.kaspersky.com.cn/ |
| Malwarebytes | https://www.malwarebytes.com/ |

### 隐私工具

| 工具 | 地址 | 用途 |
|------|------|------|
| GPG | https://gnupg.org/ | 加密/签名 |
| GPG Suite | https://gpgtools.org/ | macOS GPG |
| Gpg4win | https://www.gpg4win.org/ | Windows GPG |
| ProtonMail | https://protonmail.com/ | 隐私邮箱 |
| Tutanota | https://tutanota.com/ | 隐私邮箱 |
| EFF SSD | https://ssd.eff.org/ | 监控自卫指南 |
| Privacy Guide | https://www.privacytools.io/ | 隐私工具集 |

### 虚拟机

| 工具 | 地址 |
|------|------|
| VMware Workstation | https://www.vmware.com/products/workstation-pro.html |
| Parallels | https://www.parallels.com/ |

### 被黑档案库

| 资源 | 地址 |
|------|------|
| SlowMist Hacked | https://hacked.slowmist.io/ |
| 区块链作恶思维导图 | https://github.com/slowmist/Knowledge-Base/blob/master/mindmaps/evil_blockchain.png |
