# Windows 激活脚本

## 简介

Microsoft Activation Scripts (MAS) 提供了管理 Windows 和 Office 激活的工具。本指南涵盖合法的激活方法和批量许可选项。

### 免责声明

本指南仅供教育目的。生产环境请始终使用合法的 Microsoft 许可证。

### 什么是激活？

Windows 激活验证您的 Windows 副本是正版且已获得适当许可。

| 类型 | 描述 |
|------|------|
| 零售 | 购买的许可证 |
| OEM | 设备预装 |
| 批量 | 企业许可 |
| 数字 | 绑定到 Microsoft 账户 |

## 激活方法

### 合法激活方法

| 方法 | 描述 | 用例 |
|------|------|------|
| 产品密钥 | 25 位字符代码 | 零售购买 |
| 数字许可证 | 绑定到账户 | 免费升级 |
| KMS | 批量激活 | 企业 |
| MAK | 多次激活 | 企业 |

### 产品密钥激活

```powershell
# 检查当前激活状态
slmgr /xpr

# 安装产品密钥
slmgr /ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX

# 在线激活
slmgr /ato
```

### 数字许可证

数字许可证绑定到您的 Microsoft 账户：

1. 使用 Microsoft 账户登录
2. 进入 设置 > 激活
3. 许可证自动绑定

## Windows 版本

### 版本比较

| 版本 | 特性 | 目标用户 |
|------|------|----------|
| Home | 基本功能 | 消费者 |
| Pro | BitLocker、远程桌面 | 专业人士 |
| Enterprise | 高级安全 | 大型组织 |
| Education | 企业功能 | 学校 |
| Workstation | 服务器级功能 | 工作站 |

### 功能比较

| 功能 | Home | Pro | Enterprise |
|------|------|-----|------------|
| BitLocker | 否 | 是 | 是 |
| 远程桌面 | 仅客户端 | 完整 | 完整 |
| 组策略 | 否 | 是 | 是 |
| Hyper-V | 否 | 是 | 是 |
| Windows Sandbox | 否 | 是 | 是 |
| 分配访问 | 否 | 是 | 是 |

## 批量激活

### KMS 激活

密钥管理服务 (KMS) 在网络内激活计算机：

| 组件 | 描述 |
|------|------|
| KMS 主机 | 激活客户端的服务器 |
| KMS 客户端 | 请求激活的计算机 |
| 激活间隔 | 180 天 |
| 续期间隔 | 7 天 |

### KMS 设置

```powershell
# 安装 KMS 主机密钥
slmgr /ipk XXXXX-XXXXX-XXXXX-XXXXX-XXXXX

# 激活 KMS 主机
slmgr /ato

# 配置 DNS
# KMS 使用 DNS SRV 记录进行发现
```

### MAK 激活

多次激活密钥 (MAK) 逐个激活计算机：

| 特性 | 描述 |
|------|------|
| 一次性激活 | 每次激活减少计数 |
| 永久 | 无需续期 |
| 有限使用次数 | 基于许可协议 |

## 激活故障排除

### 常见错误代码

| 代码 | 描述 | 解决方案 |
|------|------|----------|
| 0xC004F074 | KMS 不可用 | 检查 KMS 主机 |
| 0xC004C003 | 无效产品密钥 | 验证密钥 |
| 0xC004F038 | 软件保护服务 | 重启服务 |
| 0x8007007B | 无效文件名 | 检查激活路径 |

### 诊断命令

```powershell
# 检查激活状态
slmgr /xpr

# 查看详细许可证信息
slmgr /dlv

# 检查产品密钥
wmic path SoftwareLicensingService get OA3xOriginalProductKey

# 重置激活状态
slmgr /rearm
```

### 激活疑难解答

1. 进入 设置 > 系统 > 激活
2. 点击 "疑难解答"
3. 按照屏幕指示操作

## Office 激活

### Office 版本

| 版本 | 描述 |
|------|------|
| Home & Student | 基本应用 |
| Home & Business | 增加 Outlook |
| Professional | 增加 Publisher、Access |
| Microsoft 365 | 订阅制 |

### Office 激活命令

```powershell
# 导航到 Office 安装目录
cd "C:\Program Files\Microsoft Office\Office16"

# 检查 Office 激活状态
cscript ospp.vbs /dstatus

# 安装产品密钥
cscript ospp.vbs /inpkey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX

# 激活 Office
cscript ospp.vbs /act
```

## 命令参考

### slmgr 命令

| 命令 | 描述 |
|------|------|
| `/xpr` | 显示激活状态 |
| `/dlv` | 详细许可证信息 |
| `/ipk` | 安装产品密钥 |
| `/ato` | 在线激活 |
| `/rearm` | 重置激活 |
| `/cpky` | 清除产品密钥 |
| `/upk` | 卸载产品密钥 |

### PowerShell 命令

```powershell
# 获取激活状态
Get-CimInstance -ClassName SoftwareLicensingProduct | 
  Where-Object { $_.PartialProductKey } |
  Select-Object Name, LicenseStatus

# 获取 Windows 版本
(Get-WindowsEdition -Online).Edition

# 获取产品密钥
(Get-WmiObject -Query "select * from SoftwareLicensingService").OA3xOriginalProductKey
```

## 许可模型

### 零售许可证

| 特性 | 描述 |
|------|------|
| 转移 | 可转移到新设备 |
| 支持 | 包含 Microsoft 支持 |
| 更新 | 终身更新 |
| 费用 | 一次性购买 |

### OEM 许可证

| 特性 | 描述 |
|------|------|
| 转移 | 绑定到设备 |
| 支持 | 厂商支持 |
| 更新 | 终身更新 |
| 费用 | 随设备附带 |

### 批量许可证

| 特性 | 描述 |
|------|------|
| 转移 | 组织内部 |
| 支持 | Microsoft 支持 |
| 更新 | 包含 |
| 费用 | 按设备或按用户 |

### 订阅 (Microsoft 365)

| 特性 | 描述 |
|------|------|
| 转移 | 多设备 |
| 支持 | Microsoft 支持 |
| 更新 | 始终最新 |
| 费用 | 月付/年付 |

## 激活状态

### 许可证状态

| 状态 | 含义 |
|------|------|
| Licensed | 完全激活 |
| Notification | 宽限期 |
| Expired | 许可证过期 |
| Unlicensed | 无有效许可证 |

### 宽限期

| 期间 | 时长 |
|------|------|
| 初始宽限 | 30 天 |
| 通知期 | 30 天 |
| 扩展宽限 | 60 天 |
| 非正版宽限 | 30 天 |

## 安全考量

### 产品密钥安全

| 实践 | 描述 |
|------|------|
| 安全存储 | 将密钥保存在安全位置 |
| 不要分享 | 防止未授权使用 |
| 记录 | 记录哪个设备使用哪个密钥 |
| 备份 | 保留数字许可证备份 |

### 企业安全

| 实践 | 描述 |
|------|------|
| KMS 隔离 | 保护 KMS 主机 |
| MAK 管理 | 跟踪 MAK 使用 |
| 定期审计 | 验证激活状态 |
| 网络安全 | 保护激活流量 |

## 总结

| 方法 | 最佳用途 |
|------|----------|
| 产品密钥 | 零售购买 |
| 数字许可证 | 免费升级 |
| KMS | 企业网络 |
| MAK | 企业单独激活 |
| Microsoft 365 | 订阅用户 |
