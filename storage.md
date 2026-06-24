# MinIO 对象存储教程

## 简介

MinIO 是一款高性能、兼容 S3 的对象存储系统，专为大规模数据基础设施设计。它为云原生工作负载而构建，支持从单节点部署到多 PB 级分布式集群的多种部署方式。

| 特性 | 描述 |
|---------|-------------|
| S3 兼容性 | 完全兼容 Amazon S3 API |
| 性能 | 专为高吞吐量工作负载设计 |
| 可扩展性 | 支持分布式多节点集群 |
| 部署方式 | 可在裸机、虚拟机、Kubernetes 或容器上运行 |
| 许可证 | GNU AGPL v3 |

## 架构概述

MinIO 使用与传统文件系统和块存储不同的独特架构。

| 组件 | 角色 |
|-----------|------|
| MinIO Server | 处理读写操作的核心存储引擎 |
| MinIO Client (mc) | 管理对象和存储桶的命令行工具 |
| Console | 基于 Web 的管理界面 |
| Erasure Coding | 通过奇偶校验实现数据冗余保护 |
| Bitrot Protection | 自动检测和修复静默数据损坏 |

### 存储模型

MinIO 使用扁平命名空间模型组织数据：

| 层级 | 描述 |
|-------|-------------|
| Bucket | 对象的顶层容器，类似于文件夹 |
| Object | 带元数据存储的单个文件 |
| Prefix | 使用对象名称中的正斜杠实现虚拟层级结构 |
| Version | 可选的版本控制，用于跟踪对象随时间的变化 |

## 安装

### 独立部署

```bash
# 下载 MinIO 二进制文件
wget https://dl.min.io/server/minio/release/linux-amd64/minio
chmod +x minio

# 启动 MinIO 服务器
./minio server /data --console-address ":9001"
```

### Docker 部署

```bash
# 在容器中运行 MinIO
docker run -p 9000:9000 -p 9001:9001 \
  -e MINIO_ROOT_USER=admin \
  -e MINIO_ROOT_PASSWORD=strongpassword \
  minio/minio server /data --console-address ":9001"
```

### 分布式部署

```bash
# 启动 4 节点分布式集群
minio server http://node{1...4}/data{1...4}
```

| 部署模式 | 节点数 | 磁盘数 | 使用场景 |
|----------------|-------|--------|----------|
| 独立模式 | 1 | 1 | 开发和测试 |
| 单节点多磁盘 | 1 | 多个 | 小型生产工作负载 |
| 分布式多节点 | 4+ | 每节点多个 | 生产环境 |
| Kubernetes Operator | 可变 | 基于 PVC | 云原生部署 |

## MinIO Client (mc)

MinIO Client 提供了全面的命令行管理接口。

### 安装和配置

```bash
# 安装 mc
wget https://dl.min.io/client/mc/release/linux-amd64/mc
chmod +x mc

# 配置别名
mc alias set myminio http://localhost:9000 admin strongpassword
```

### 常用操作

| 操作 | 命令 | 描述 |
|-----------|---------|-------------|
| 创建存储桶 | `mc mb myminio/mybucket` | 创建新存储桶 |
| 列出存储桶 | `mc ls myminio` | 列出所有存储桶 |
| 上传文件 | `mc put file.txt myminio/mybucket` | 上传单个文件 |
| 下载文件 | `mc get myminio/mybucket/file.txt` | 下载文件 |
| 复制目录 | `mc cp --recursive ./dir myminio/mybucket/` | 上传目录内容 |
| 删除对象 | `mc rm myminio/mybucket/file.txt` | 删除对象 |
| 镜像存储桶 | `mc mirror ./local myminio/mybucket` | 将本地同步到存储桶 |
| 删除存储桶 | `mc rb myminio/mybucket` | 删除空存储桶 |

## 存储桶配置

### 版本控制

版本控制可在同一存储桶中保留对象的多个版本。

```bash
# 启用版本控制
mc version enable myminio/mybucket

# 检查版本控制状态
mc version info myminio/mybucket
```

### 生命周期策略

生命周期规则可自动执行对象的转换和过期操作。

| 策略类型 | 描述 | 示例用例 |
|-------------|-------------|------------------|
| 过期 | 在一段时间后删除对象 | 30 天后删除临时文件 |
| 转换 | 将对象移动到不同的存储层 | 90 天后归档日志 |
| 非当前版本过期 | 移除旧版本 | 仅保留最近 5 个版本 |
| 基于前缀 | 对特定前缀应用规则 | 不同文件夹使用不同规则 |

```bash
# 设置过期策略
cat > lifecycle.json <<EOF
{
  "Rules": [
    {
      "ID": "expire-temp",
      "Status": "Enabled",
      "Expiration": {
        "Days": 30
      },
      "Filter": {
        "Prefix": "temp/"
      }
    }
  ]
}
EOF

mc ilm import myminio/mybucket < lifecycle.json
```

### 存储桶通知

MinIO 支持对象操作的事件通知。

| 目标 | 协议 | 使用场景 |
|--------|----------|----------|
| AMQP | AMQP 0-9-1 | 消息队列集成 |
| NATS | NATS | 实时事件流 |
| Kafka | Kafka | 大规模事件处理 |
| Redis | Redis | 缓存失效和队列 |
| Webhook | HTTP POST | 自定义集成 |
| Elasticsearch | HTTP | 搜索索引 |

## 安全

### 身份和访问管理

| 概念 | 描述 |
|---------|-------------|
| Root 凭证 | 通过环境变量设置的初始管理员用户 |
| IAM 用户 | 具有特定访问密钥的独立用户 |
| 用户组 | 共享通用策略的用户集合 |
| 策略 | 定义允许/拒绝操作的 JSON 文档 |
| 服务账户 | 应用程序的限定范围凭证 |

### 策略示例

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::mybucket/*"
    },
    {
      "Effect": "Allow",
      "Action": [
        "s3:ListBucket"
      ],
      "Resource": "arn:aws:s3:::mybucket"
    }
  ]
}
```

### 加密

| 类型 | 描述 |
|------|-------------|
| 服务端加密 (SSE-S3) | MinIO 自动管理加密密钥 |
| SSE-KMS | 与外部密钥管理系统集成 |
| SSE-C | 客户端提供的加密密钥 |
| 客户端加密 | 上传前的应用层加密 |

## 性能调优

### 硬件建议

| 组件 | 建议 |
|-----------|----------------|
| CPU | 多核，生产环境至少 4 核 |
| 内存 | 生产工作负载至少 32 GB |
| 网络 | 分布式部署建议 10 GbE 或更高 |
| 存储 | 热数据使用 NVMe SSD，冷存储使用 HDD |
| 文件系统 | 推荐使用 XFS 格式化磁盘 |

### 磁盘配置

```bash
# 使用 XFS 格式化磁盘
mkfs.xfs /dev/sdb
mkfs.xfs /dev/sdc

# 使用适当的选项挂载
mount /dev/sdb /data/disk1
mount /dev/sdc /data/disk2
```

## 监控

### Prometheus 指标

MinIO 暴露与 Prometheus 兼容的指标。

```yaml
# prometheus.yml
scrape_configs:
  - job_name: 'minio'
    metrics_path: /minio/v2/metrics/cluster
    scheme: https
    static_configs:
      - targets: ['minio-server:9000']
```

| 指标类别 | 示例 |
|----------------|---------|
| 存储桶指标 | 对象数量、存储桶大小、请求速率 |
| 集群指标 | 节点健康状态、磁盘状态、网络吞吐量 |
| 系统指标 | CPU 使用率、内存、goroutines |
| API 指标 | 请求延迟、每个端点的错误率 |

## S3 API 兼容性

MinIO 可与任何兼容 S3 的 SDK 配合使用。

```python
from minio import Minio

client = Minio(
    "localhost:9000",
    access_key="admin",
    secret_key="strongpassword",
    secure=False
)

# 创建存储桶
if not client.bucket_exists("mybucket"):
    client.make_bucket("mybucket")

# 上传文件
client.fput_object("mybucket", "report.pdf", "./report.pdf")

# 列出对象
objects = client.list_objects("mybucket", prefix="reports/")
for obj in objects:
    print(obj.object_name, obj.size)
```

## 总结

| 主题 | 核心要点 |
|-------|-------------|
| 架构 | 扁平命名空间，使用纠删码保证持久性 |
| 部署 | 从单节点到分布式集群的灵活部署 |
| 管理 | mc CLI 和 Web 控制台进行管理 |
| 安全 | 细粒度 IAM 配合多种加密选项 |
| 兼容性 | 完全兼容 S3 API 和标准 SDK |
| 性能 | 针对高吞吐量、大规模工作负载优化 |
