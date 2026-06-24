# SoftEther VPN 服务器教程

## 简介

SoftEther VPN 是由筑波大学开发的开源、跨平台 VPN 服务器和客户端软件。它支持多种 VPN 协议，提供高性能、灵活性和强大的安全功能。

| 特性 | 描述 |
|---------|-------------|
| 多协议 | 支持 SSL-VPN、L2TP、OpenVPN 和 WireGuard |
| 跨平台 | 支持 Windows、Linux、macOS 和 FreeBSD |
| 高性能 | 针对速度优化，支持 NAT 穿透 |
| 防火墙友好 | 可在防火墙和 NAT 设备后工作 |
| 免费开源 | Apache License 2.0 |

## 架构

### 支持的 VPN 协议

| 协议 | 端口 | 加密 | 备注 |
|----------|------|------------|-------|
| SSL-VPN (HTTPS) | 443 | AES-256、RSA | 内置协议，防火墙友好 |
| L2TP/IPsec | 500、4500 | IPsec ESP | 兼容原生操作系统客户端 |
| OpenVPN | 1194 | OpenSSL | 广泛使用的开源协议 |
| SSTP | 443 | TLS | Windows 原生支持 |
| WireGuard | 51820 | ChaCha20 | 现代轻量级协议 |

### 服务器模式

| 模式 | 描述 | 使用场景 |
|------|-------------|----------|
| VPN Server | 接受来自 VPN 客户端的连接 | 主要服务器部署 |
| VPN Bridge | 通过 VPN 隧道连接网络 | 站点间组网 |
| VPN Client | 连接到 VPN 服务器 | 终端用户访问 |

## 安装

### Linux 安装

```bash
# 下载 SoftEther VPN Server
wget https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.41-9787-beta/softether-vpnserver-v4.41-9787-beta-2022.04.26-linux-x64-64bit.tar.gz

# 解压
tar -xzf softether-vpnserver-*.tar.gz
cd vpnserver

# 编译（Linux 上需要）
make

# 启动服务器
./vpnserver start
```

### Docker 部署

```bash
docker run -d \
  --name=softether-vpn \
  --cap-add=NET_ADMIN \
  -p 443:443 \
  -p 992:992 \
  -p 5555:5555 \
  -p 500:500/udp \
  -p 4500:4500/udp \
  -p 1194:1194/udp \
  -v ./vpn_server.config:/usr/local/vpnserver/vpn_server.config \
  --restart unless-stopped \
  siomiz/softethervpn
```

### 系统要求

| 组件 | 最低要求 | 推荐配置 |
|-----------|---------|-------------|
| CPU | 1 核 | 2+ 核 |
| 内存 | 256 MB | 1 GB+ |
| 网络 | 100 Mbps | 1 Gbps+ |
| 操作系统 | Linux、Windows、macOS | Ubuntu 20.04+ 或 Windows Server 2019+ |

## 初始配置

### 服务器管理器设置

| 步骤 | 操作 |
|------|--------|
| 1 | 启动 SoftEther VPN Server Manager（GUI 或 CLI） |
| 2 | 连接到 localhost:443 或使用 ServerAdminPassword |
| 3 | 设置管理员密码 |
| 4 | 配置虚拟 Hub（默认：DEFAULT） |
| 5 | 启用所需的 VPN 协议 |

### 虚拟 Hub 配置

| 设置 | 描述 |
|---------|-------------|
| Hub 名称 | 虚拟网络的标识符 |
| 密码 | Hub 管理密码 |
| 最大会话数 | 最大并发连接数 |
| 在线/离线 | 启用或禁用 Hub |

### 网络设置

| 设置 | 描述 |
|---------|-------------|
| 本地网桥 | 将 Hub 连接到物理网络适配器 |
| SecureNAT | 虚拟 NAT 和 DHCP 服务器 |
| 级联连接 | 连接到另一个 VPN 服务器 |

## 用户管理

### 用户类型

| 类型 | 描述 |
|------|-------------|
| 个人用户 | 具有凭证的特定用户账户 |
| 用户组 | 具有共享设置的用户集合 |
| 匿名 | 未认证的访问（有限使用） |

### 认证方式

| 方式 | 描述 |
|--------|-------------|
| 密码 | 用户名和密码认证 |
| 证书 | 基于 X.509 证书的认证 |
| RADIUS | 外部 RADIUS 服务器认证 |
| NT Domain | Windows 域认证 |
| LDAP | 目录服务认证 |

### 创建用户

```bash
# 使用 vpncmd
./vpncmd localhost /SERVER /CMD UserCreate username /GROUP:none /REALNAME:"User Name" /NOTE:""
./vpncmd localhost /SERVER /CMD UserPasswordSet username /PASSWORD:strongpassword
```

### 用户权限

| 权限 | 描述 |
|-----------|-------------|
| 无限制带宽 | 不限制流量 |
| 最大带宽 | 限制上传/下载速度 |
| 最大会话数 | 限制并发连接 |
| 时间限制 | 指定时长后断开连接 |
| IP 限制 | 仅允许来自特定 IP 的连接 |

## VPN 协议配置

### SSL-VPN 设置

| 设置 | 值 |
|---------|-------|
| 端口 | 443 (HTTPS) |
| 证书 | 服务器 SSL 证书 |
| 加密 | AES-256-GCM |
| 客户端 | SoftEther VPN Client 或 SSTP |

### L2TP/IPsec 设置

| 设置 | 值 |
|---------|-------|
| 端口 | 500 (IKE)、4500 (NAT-T) |
| 预共享密钥 | IPsec 预共享密钥 |
| 加密 | AES-256 配合 SHA-256 |
| 客户端 | 原生操作系统 VPN 客户端 |

### OpenVPN 兼容性

| 设置 | 值 |
|---------|-------|
| 端口 | 1194 (UDP) |
| 协议 | UDP 或 TCP |
| 加密 | AES-256-CBC |
| 客户端 | 使用导出配置的 OpenVPN 客户端 |

## SecureNAT

### SecureNAT 功能

| 功能 | 描述 |
|---------|-------------|
| 虚拟 NAT | VPN 客户端的 NAT 转换 |
| 虚拟 DHCP | 自动 IP 地址分配 |
| DNS 中继 | VPN 客户端的 DNS 解析 |
| 无需驱动 | 无需管理员权限即可工作 |

### SecureNAT 配置

| 设置 | 描述 |
|---------|-------------|
| 虚拟 IP 范围 | 分配给客户端的 IP 地址（如 192.168.30.0/24） |
| NAT 网关 | NAT 的网关 IP（如 192.168.30.1） |
| DHCP 范围 | DHCP 地址池的起始和结束地址 |
| DNS 服务器 | VPN 客户端的 DNS 服务器 |
| 租约时间 | DHCP 租约时长 |

## 级联 VPN 连接

### 站点间 VPN

| 组件 | 位置 A | 位置 B |
|-----------|-----------|-----------|
| 服务器 | 带 Hub 的 VPN Server | 带 Hub 的 VPN Server |
| 网桥 | 到局域网的本地网桥 | 到局域网的本地网桥 |
| 级联 | 连接到远程 Hub | 接受级联连接 |

### 配置步骤

| 步骤 | 操作 |
|------|--------|
| 1 | 在两台服务器上创建匹配的用户账户 |
| 2 | 在服务器 A 上创建到服务器 B 的级联连接 |
| 3 | 在两台服务器上配置本地网桥 |
| 4 | 如需要则启用 IP 路由 |
| 5 | 测试局域网之间的连通性 |

## 安全

### 加密选项

| 算法 | 密钥长度 | 使用场景 |
|-----------|----------|----------|
| AES | 128、192、256 位 | 主要加密标准 |
| Camellia | 128、192、256 位 | AES 的替代方案 |
| RSA | 2048、4096 位 | 密钥交换和证书 |
| SHA | 256、384、512 位 | 哈希和完整性 |

### 安全最佳实践

| 实践 | 描述 |
|----------|-------------|
| 强密码 | 为管理员和用户账户使用复杂密码 |
| 证书认证 | 尽可能使用证书替代密码 |
| 禁用未使用协议 | 仅启用需要的协议 |
| IP 限制 | 将管理员访问限制在特定 IP 地址 |
| 日志记录 | 启用全面的日志记录 |
| 更新 | 保持服务器软件更新 |

## 监控和日志

### 日志类型

| 日志 | 内容 |
|-----|---------|
| 安全日志 | 认证事件、访问尝试 |
| 服务器日志 | 服务器启动/停止、配置更改 |
| 连接日志 | VPN 会话的建立和终止 |
| 数据包日志 | 网络流量捕获 |

### 监控指标

| 指标 | 描述 |
|--------|-------------|
| 活跃会话 | 当前连接的客户端数量 |
| 吞吐量 | 每秒的网络流量（字节） |
| 总流量 | 累计传输数据量 |
| 会话时长 | 每个客户端的连接时间 |

## 客户端配置

### 原生客户端设置

| 设置 | L2TP/IPsec | OpenVPN |
|---------|-----------|---------|
| 服务器地址 | VPN 服务器 IP 或主机名 | VPN 服务器 IP 或主机名 |
| 端口 | 默认（自动） | 1194 |
| 认证 | 预共享密钥 + 用户凭证 | 证书 + 用户凭证 |
| 协议 | UDP | UDP 或 TCP |

## 故障排除

### 常见问题

| 问题 | 原因 | 解决方案 |
|-------|-------|----------|
| 连接被拒绝 | 服务器未运行或端口被阻止 | 启动服务器并检查防火墙 |
| 认证失败 | 凭证错误 | 验证用户名和密码 |
| VPN 无法上网 | NAT/路由配置错误 | 启用 SecureNAT 或配置路由 |
| 性能缓慢 | 加密开销或带宽限制 | 检查服务器资源和网络 |
| L2TP 无法连接 | IPsec 端口被阻止 | 打开 UDP 端口 500 和 4500 |

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 协议 | 支持 SSL-VPN、L2TP、OpenVPN、SSTP 和 WireGuard |
| 部署 | 在 Linux、Windows、macOS 上运行，支持 Docker |
| 用户 | 灵活的密码、证书和 LDAP 认证 |
| 网络 | SecureNAT 便于设置，本地网桥用于高级配置 |
| 安全 | AES-256 加密配合基于证书的认证 |
| 使用场景 | 远程访问、站点间和桥接组网 |
