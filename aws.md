# AWS 实用指南 (OG-AWS)

基于真实经验和社区知识的 Amazon Web Services 实用指南。

---

## EC2 - 弹性计算云

### 实例类型

| 系列 | 用途 | 示例 | 存储 | 网络 |
|--------|----------|----------|---------|---------|
| T | 突发性能，通用型 | t3.micro, t3.large | EBS | 低-中 |
| M | 通用型 | m5.large, m6i.xlarge | EBS | 中-高 |
| C | 计算优化型 | c5.large, c6i.xlarge | EBS | 高 |
| R | 内存优化型 | r5.large, r6i.xlarge | EBS | 高 |
| I | 存储优化型 | i3.large, i4i.xlarge | NVMe SSD | 高 |
| G | GPU 实例 | g4dn.xlarge | EBS/NVMe | 高 |
| P | GPU（机器学习训练） | p4d.24xlarge | NVMe SSD | 极高 |

### 定价模型

| 模型 | 折扣 | 承诺期 | 灵活性 | 适用场景 |
|-------|----------|------------|-------------|----------|
| 按需实例 | 0% | 无 | 完全灵活 | 短期、不可预测的工作负载 |
| 预留实例（1年） | 30-40% | 1年 | 有限 | 稳定的工作负载 |
| 预留实例（3年） | 50-60% | 3年 | 有限 | 长期可预测的工作负载 |
| Savings Plans | 40-66% | 1-3年 | 中等 | 灵活的计算使用 |
| Spot 实例 | 60-90% | 无 | 可中断 | 容错、灵活的工作负载 |
| 专用主机 | 不定 | 无 | 完全灵活 | 许可证、合规性需求 |

### Spot 实例

Spot 实例可提供显著的成本节省，但可能在 2 分钟警告后被中断。

**最佳实践：**
- 使用 Spot Fleet 来分散多种实例类型
- 在应用程序中实现中断处理逻辑
- 设置最高价格以控制成本
- 用于无状态、容错的工作负载

**中断处理：**
```python
import requests

def check_interruption():
    try:
        response = requests.get(
            'http://169.254.169.254/latest/meta-data/spot/instance-action',
            timeout=1
        )
        if response.status_code == 200:
            handle_graceful_shutdown()
    except requests.exceptions.RequestException:
        pass
```

### 实例选择指南

| 工作负载 | 推荐类型 | 原因 |
|----------|------------------|-----------|
| Web 服务器（低流量） | t3.micro/small | 突发性能，性价比高 |
| Web 服务器（高流量） | m5.large+ | 稳定的性能 |
| 批处理 | c5/c6i | 计算优化 |
| 内存缓存 | r5/r6i | 内存优化 |
| 机器学习训练 | p4d/g4dn | GPU 加速 |
| 高 I/O 数据库 | i4i | NVMe SSD 存储 |

---

## S3 - 简单存储服务

### 存储类

| 存储类 | 可用性 | 持久性 | 检索费用 | 用途 |
|---------------|--------------|------------|----------------|----------|
| S3 Standard | 99.99% | 99.999999999% | 无 | 频繁访问 |
| S3 Intelligent-Tiering | 99.9% | 99.999999999% | 无 | 访问模式未知 |
| S3 Standard-IA | 99.9% | 99.999999999% | 按 GB 计费 | 低频访问 |
| S3 One Zone-IA | 99.5% | 99.999999999% | 按 GB 计费 | 低频、非关键数据 |
| S3 Glacier Instant | 99.9% | 99.999999999% | 按 GB 计费 | 归档，即时访问 |
| S3 Glacier Flexible | 99.99% | 99.999999999% | 按 GB 计费 | 归档，分钟-小时级检索 |
| S3 Glacier Deep Archive | 99.99% | 99.999999999% | 按 GB 计费 | 长期归档 |

### 生命周期策略

自动在存储类之间转换以优化成本。

```json
{
  "Rules": [
    {
      "ID": "Move to IA after 30 days",
      "Status": "Enabled",
      "Filter": { "Prefix": "logs/" },
      "Transitions": [
        { "Days": 30, "StorageClass": "STANDARD_IA" },
        { "Days": 90, "StorageClass": "GLACIER" }
      ],
      "Expiration": { "Days": 365 }
    }
  ]
}
```

### 版本控制

**要点：**
- 一旦启用，无法禁用（只能暂停）
- 支持 MFA Delete 以增强安全性
- 每个版本单独计费
- 使用生命周期规则管理旧版本

```bash
# 启用版本控制
aws s3api put-bucket-versioning --bucket my-bucket --versioning-configuration Status=Enabled

# 列出版本
aws s3api list-object-versions --bucket my-bucket
```

### S3 安全

**阻止公共访问设置：**
- BlockPublicAcls：阻止新的公共 ACL
- IgnorePublicAcls：忽略现有的公共 ACL
- BlockPublicPolicy：阻止新的公共存储桶策略
- RestrictPublicBuckets：限制公共存储桶访问

---

## RDS - 关系数据库服务

### 引擎对比

| 引擎 | 用途 | Multi-AZ | 只读副本 | 最大存储 |
|--------|----------|----------|---------------|-------------|
| MySQL | Web 应用、CMS | 支持 | 最多 15 个 | 64 TB |
| PostgreSQL | 复杂查询、GIS | 支持 | 最多 15 个 | 64 TB |
| MariaDB | MySQL 兼容 | 支持 | 最多 15 个 | 64 TB |
| Oracle | 企业应用 | 支持 | 最多 15 个 | 64 TB |
| SQL Server | .NET 应用 | 支持 | 最多 5 个 | 64 TB |
| Aurora MySQL | MySQL 兼容 | 支持 | 最多 15 个 | 128 TB |
| Aurora PostgreSQL | PostgreSQL 兼容 | 支持 | 最多 15 个 | 128 TB |

### 扩展

**垂直扩展：**
- 更改实例类型（需要停机）
- 独立扩展存储（最短停机时间）
- Aurora 支持自动扩展

**水平扩展：**
- 只读副本适用于读密集型工作负载
- 每个源最多 15 个只读副本
- 支持跨区域只读副本
- Multi-AZ 自动故障转移

### 备份

**自动备份：**
- 保留期：1-35 天
- 备份窗口期间的每日快照
- 每 5 分钟的事务日志
- 时间点恢复

**最佳实践：**
- 启用具有足够保留期的自动备份
- 定期测试恢复流程
- 使用跨区域快照进行灾难恢复

---

## Lambda - 无服务器函数

### 触发器

| 触发器 | 用途 | 最大事件大小 |
|---------|----------|----------------|
| API Gateway | REST/HTTP API | 10 MB |
| S3 | 对象事件 | - |
| DynamoDB | 流处理 | - |
| SQS | 消息处理 | 256 KB |
| SNS | 通知 | 256 KB |
| CloudWatch Events | 定时任务 | - |
| CloudWatch Logs | 日志处理 | - |

### 限制

| 资源 | 限制 | 备注 |
|----------|-------|-------|
| 内存 | 128 MB - 10,240 MB | 1 MB 递增 |
| 超时 | 15 分钟 | 默认 3 秒 |
| 包大小 | 250 MB（解压后） | 50 MB（压缩） |
| 环境变量 | 4 KB | 所有变量总计 |
| 并发执行数 | 1,000（默认） | 可申请提升 |
| 临时存储 | 512 MB - 10,240 MB | /tmp 目录 |

### 最佳实践

**性能：**
- 使用预配置并发减少冷启动
- 使用轻量级运行时（Node.js、Python）
- 复用连接和 SDK 客户端
- 保持函数包体积小

**连接复用：**
```python
import boto3

# Initialize outside handler - reused across invocations
dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('my-table')

def lambda_handler(event, context):
    response = table.get_item(Key={'id': event['id']})
    return response['Item']
```

---

## VPC - 虚拟私有云

### 子网

| 类型 | 互联网访问 | 用途 |
|------|-----------------|----------|
| 公有子网 | 通过 Internet Gateway | Web 服务器、负载均衡器 |
| 私有子网 | 通过 NAT Gateway | 应用服务器、数据库 |
| 隔离子网 | 无 | 敏感工作负载、合规性需求 |

### 安全组 vs NACL

| 特性 | 安全组 | NACL |
|---------|-----------------|-------|
| 层级 | 实例级别 | 子网级别 |
| 状态 | 有状态 | 无状态 |
| 规则 | 仅允许 | 允许和拒绝 |
| 默认 | 拒绝所有入站 | 允许所有 |
| 评估方式 | 评估所有规则 | 按顺序评估规则 |

**安全组示例：**
```bash
aws ec2 create-security-group --group-name web-sg --description "Web server"
aws ec2 authorize-security-group-ingress --group-id sg-12345678   --protocol tcp --port 80 --cidr 0.0.0.0/0
```

### VPC 对等连接

**限制：**
- 不支持传递性对等连接
- CIDR 块不能重叠
- 必须在同一区域（跨区域对等连接除外）

---

## IAM - 身份与访问管理

### 用户 vs 角色

| 特性 | 用户 | 角色 |
|---------|-------|-------|
| 凭证 | 长期访问密钥 | 临时凭证 |
| 用途 | 个人用户 | 应用程序、服务 |
| 密码 | 支持（控制台访问） | 不支持 |
| 访问密钥 | 支持（API 访问） | 不支持（通过 AssumeRole 获取） |
| 最佳实践 | 尽量减少使用 | 应用程序首选 |

### 最佳实践

1. **最小权限原则** - 仅授予必要的权限
2. **为应用程序使用角色** - EC2 实例配置文件、Lambda 执行角色
3. **启用 MFA** - 根账户必须启用，建议所有用户启用
4. **轮换凭证** - 每 90 天轮换访问密钥，使用 Secrets Manager

**策略示例：**
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:ListBucket"],
      "Resource": ["arn:aws:s3:::my-bucket", "arn:aws:s3:::my-bucket/*"]
    }
  ]
}
```

---

## CloudWatch - 监控与可观测性

### 组件

| 组件 | 用途 | 数据保留 |
|-----------|---------|----------------|
| 指标 | 数值数据点 | 15 个月 |
| 日志 | 基于文本的日志 | 无限制（可配置） |
| 告警 | 阈值监控 | 不适用 |
| 事件 | 事件驱动自动化 | 不适用 |
| 仪表板 | 可视化 | 不适用 |

### 关键指标

| 服务 | 指标 | 阈值 |
|---------|---------|------------|
| EC2 | CPUUtilization, NetworkIn/Out | CPU >80% |
| RDS | CPUUtilization, FreeStorageSpace | CPU >80%, 存储 <20% |
| Lambda | Duration, Errors, Throttles | <超时时间, 错误率 <1% |
| ALB | RequestCount, TargetResponseTime | 延迟 SLA |

### 告警

```bash
aws cloudwatch put-metric-alarm   --alarm-name "High CPU"   --metric-name CPUUtilization   --namespace AWS/EC2   --statistic Average   --period 300   --threshold 80   --comparison-operator GreaterThanThreshold   --evaluation-periods 2   --alarm-actions arn:aws:sns:us-east-1:123456789012:alerts
```

### Log Insights 查询

```sql
fields @timestamp, @message
| filter @message like /ERROR/
| sort @timestamp desc
| limit 20
```

---

## 成本管理

### 预留实例 vs Savings Plans

| 特性 | 预留实例 | Savings Plans |
|---------|-------------------|---------------|
| 承诺 | 实例系列/大小 | 每小时消费金额 |
| 灵活性 | 有限（实例替换） | 计算或 EC2 实例 |
| 付款方式 | 全预付/部分预付/无预付 | 全预付/部分预付/无预付 |
| 期限 | 1 或 3 年 | 1 或 3 年 |
| 范围 | 区域或可用区 | 计算（跨服务） |

### Trusted Advisor 类别

| 类别 | 检查项 | 示例 |
|----------|--------|----------|
| 成本优化 | 11 | 空闲资源、RI 覆盖率 |
| 性能 | 11 | 高使用率实例 |
| 安全 | 18 | IAM 使用、安全组规则 |
| 容错 | 12 | Multi-AZ、备份状态 |

### 成本分配标签

```bash
aws ec2 create-tags --resources i-1234567890abcdef0   --tags Key=Environment,Value=Production Key=Team,Value=Backend
```

**推荐标签：** Environment, Team, Project, CostCenter, Owner

---

## 网络服务

### Route 53

| 策略 | 用途 | 配置 |
|--------|----------|---------------|
| 简单路由 | 单一资源 | 一条记录 |
| 加权路由 | 流量分配 | 基于百分比 |
| 延迟路由 | 低延迟 | 基于区域 |
| 故障转移路由 | 主动-被动 | 主/备 |
| 地理位置路由 | 基于位置 | 国家/大洲 |

### CloudFront 缓存行为

| 路径模式 | TTL | 源站 | 用途 |
|--------------|-----|--------|----------|
| /static/* | 86400秒 | S3 | 静态资源 |
| /api/* | 0秒 | ALB | API 请求 |
| /images/* | 604800秒 | S3 | 图片 |
| 默认 | 3600秒 | ALB | 动态内容 |

### ELB 类型

| 类型 | 用途 | 协议 | 特性 |
|------|----------|----------|----------|
| 应用型 (ALB) | HTTP/HTTPS | 第7层 | 基于路径的路由 |
| 网络型 (NLB) | TCP/UDP | 第4层 | 超低延迟 |
| 网关型 (GWLB) | 第三方设备 | 第3层 | 防火墙、检查 |

---

## 数据库服务

### DynamoDB

**容量模式：**

| 模式 | 定价 | 用途 |
|------|---------|----------|
| 按需模式 | 按请求计费 | 不可预测的流量 |
| 预置模式 | 按 RCU/WCU 计费 | 可预测的流量 |

**容量单位：**
- 1 RCU = 每秒 1 次强一致性读取（4 KB）
- 1 WCU = 每秒 1 次写入（1 KB）

### ElastiCache

| 特性 | Redis | Memcached |
|---------|-------|-----------|
| 数据结构 | 丰富（列表、集合、哈希） | 简单键值对 |
| 持久化 | 支持 | 不支持 |
| 复制 | 支持 | 不支持 |
| 集群 | 支持 | 支持 |
| 用途 | 复杂数据、持久化 | 简单缓存 |

---

## CI/CD 服务

### CodePipeline 阶段

| 阶段 | 操作 | 用途 |
|-------|---------|---------|
| 源代码 | GitHub, CodeCommit, S3 | 获取源代码 |
| 构建 | CodeBuild, Jenkins | 编译、测试 |
| 测试 | CodeBuild, Lambda | 集成测试 |
| 部署 | CodeDeploy, ECS, CloudFormation | 部署 |

### CodeBuild Buildspec

```yaml
version: 0.2
phases:
  install:
    runtime-versions:
      nodejs: 16
    commands:
      - npm install
  build:
    commands:
      - npm run build
  post_build:
    commands:
      - aws s3 sync dist/ s3://my-bucket/
artifacts:
  files:
    - '**/*'
  base-directory: dist
```

---

## 常见陷阱

### 成本陷阱

| 陷阱 | 影响 | 预防措施 |
|---------|--------|------------|
| 未使用的资源 | 浪费开支 | 定期清理 |
| 过度配置实例 | 超支 30-50% | 合理调整大小、Auto Scaling |
| 数据传输费用 | 账单不可预测 | VPC 端点 |
| 未挂载的 EBS 卷 | 存储费用 | 快照后删除 |

### 安全陷阱

| 陷阱 | 风险 | 预防措施 |
|---------|------|------------|
| 使用根账户 | 完全访问权限泄露 | 使用 IAM 用户/角色 |
| 公共 S3 存储桶 | 数据暴露 | 阻止公共访问 |
| 开放的安全组 | 未授权访问 | 限制 CIDR 范围 |
| 未启用 MFA | 账户被入侵 | 全面启用 MFA |

### 架构陷阱

| 陷阱 | 影响 | 解决方案 |
|---------|--------|----------|
| 单可用区部署 | 无高可用性 | Multi-AZ 架构 |
| 无缓存 | 性能差 | ElastiCache, CloudFront |
| 同步耦合 | 级联故障 | 使用 SQS/SNS 异步解耦 |
| 无监控 | 盲区 | CloudWatch, X-Ray |

---

## 常见问题

**问：应该选择哪个区域？**
答：考虑用户延迟、服务可用性、合规性要求和成本。美国区域通常最便宜。

**问：什么时候应该使用 Spot 实例？**
答：适用于容错、灵活的工作负载：批处理、CI/CD、大数据、无状态 Web 服务器。

**问：RDS 还是 DynamoDB？**
答：关系型数据、复杂查询、ACID 事务使用 RDS。键值访问、大规模扩展、无服务器使用 DynamoDB。

**问：如何降低数据传输成本？**
答：使用 VPC 端点访问 AWS 服务，压缩数据，使用 CloudFront 进行内容分发。

---

## 架构决策矩阵

| 需求 | 服务选择 | 原因 |
|-------------|----------------|-----------|
| 静态网站 | S3 + CloudFront | 低成本、高可用 |
| REST API | API Gateway + Lambda | 无服务器、自动扩展 |
| 微服务 | ECS/EKS + ALB | 容器编排 |
| 关系型数据库 | Aurora PostgreSQL | 托管服务、兼容性强 |
| NoSQL 数据库 | DynamoDB | 无服务器、大规模扩展 |
| 缓存 | ElastiCache Redis | 低延迟、功能丰富 |
| 消息队列 | SQS/SNS | 解耦、可靠性 |
| 对象存储 | S3 | 持久、可扩展 |
| 监控 | CloudWatch | 原生集成 |
