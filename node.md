# Node-RED：IoT 自动化平台指南

## 目录

1. [Node-RED 简介](#introduction)
2. [安装与设置](#installation)
3. [核心概念](#core-concepts)
4. [构建流程](#building-flows)
5. [常用节点](#common-nodes)
6. [IoT 协议](#protocols)
7. [仪表板与 UI](#dashboard)
8. [部署与安全](#deployment)

---

## 简介

Node-RED 是一个基于流程的编程工具，用于将硬件设备、API 和在线服务连接在一起。它提供基于浏览器的编辑器，可可视化构建自动化工作流。

### Node-RED 核心功能

| 功能 | 描述 | 好处 |
|------|------|------|
| 可视化编辑器 | 拖拽式流程构建 | 易于学习 |
| 基于浏览器 | 无需客户端安装 | 随处访问 |
| 可扩展 | 数千个节点 | 连接一切 |
| 轻量级 | 可运行在树莓派 | IoT 就绪 |
| JSON 流程 | 可移植配置 | 易于备份 |

### Node-RED vs 其他工具

| 功能 | Node-RED | Home Assistant | n8n |
|------|----------|----------------|-----|
| 重点 | IoT/自动化 | 家庭自动化 | 工作流 |
| 学习曲线 | 低 | 中等 | 低 |
| 可视化编辑器 | 是 | 有限 | 是 |
| 可扩展性 | 高 | 高 | 高 |
| 资源使用 | 极低 | 中等 | 中等 |

### 常见用例

| 类别 | 示例 |
|------|------|
| 家庭自动化 | 灯光控制、恒温器 |
| IoT 传感器 | 温度、湿度监控 |
| API 集成 | Webhook 处理 |
| 数据处理 | ETL 管道 |
| 消息 | 聊天机器人、通知 |

---

## 安装与设置

Node-RED 可以安装在各种平台上。

### 安装方式

| 平台 | 方式 | 命令 |
|------|------|------|
| npm (全局) | npm | `npm install -g node-red` |
| Docker | Docker | `docker run -p 1880:1880 nodered/node-red` |
| Raspberry Pi | 脚本 | `bash <(curl -sL https://raw.githubusercontent.com/node-red/linux-installers/master/deb/update-nodejs-and-nodered)` |
| Snap | Snap | `sudo snap install node-red` |

### Docker 安装

```yaml
# docker-compose.yml
version: '3'
services:
  node-red:
    image: nodered/node-red:latest
    ports:
      - "1880:1880"
    volumes:
      - node-red-data:/data
    environment:
      - TZ=UTC

volumes:
  node-red-data:
```

### 系统要求

| 组件 | 最低 | 推荐 |
|------|------|------|
| CPU | 1 核 | 2 核 |
| 内存 | 256MB | 1GB |
| 存储 | 100MB | 1GB |
| Node.js | v14 | v18 LTS |

### 首次访问

| 步骤 | 操作 | URL |
|------|------|-----|
| 1 | 启动 Node-RED | `node-red` |
| 2 | 打开浏览器 | http://localhost:1880 |
| 3 | 访问编辑器 | 可视化流程编辑器 |
| 4 | 创建第一个流程 | 拖拽节点 |

---

## 核心概念

理解 Node-RED 基础以有效构建流程。

### 流程组件

| 组件 | 描述 | 示例 |
|------|------|------|
| 节点 | 单个功能 | HTTP 请求、开关 |
| 连线 | 节点间的连接 | 数据流路径 |
| 流程 | 节点集合 | 完整工作流 |
| Tab | 流程组织 | 分离关注点 |

### 消息结构

```json
{
  "payload": "Main data",
  "topic": "Message topic",
  "_msgid": "Unique ID",
  "custom": "Any additional data"
}
```

### 节点属性

| 属性 | 描述 | 示例 |
|------|------|------|
| 名称 | 显示名称 | "获取天气" |
| 类型 | 节点功能 | http request |
| 配置 | 节点设置 | URL、方法 |
| 连线 | 输出连接 | 下一个节点 |

### 流程生命周期

| 事件 | 触发 | 操作 |
|------|------|------|
| 部署 | 保存变更 | 流程重启 |
| 启动 | Node-RED 启动 | 流程初始化 |
| 停止 | Node-RED 停止 | 清理 |
| 消息 | 接收输入 | 处理数据 |

---

## 构建流程

创建自动化流程的分步指南。

### 流程设计流程

| 步骤 | 操作 | 考虑因素 |
|------|------|----------|
| 1 | 定义目标 | 自动化什么 |
| 2 | 确定触发器 | 何时启动 |
| 3 | 添加处理 | 转换数据 |
| 4 | 添加输出 | 发送到哪里 |
| 5 | 测试 | 验证行为 |
| 6 | 部署 | 激活流程 |

### 基本流程模式

```
[触发] → [处理] → [输出]

Example:
[Inject] → [Function] → [Debug]
```

### 常见流程模式

| 模式 | 描述 | 使用的节点 |
|------|------|------------|
| 线性 | 顺序处理 | Inject → Function → Debug |
| 分支 | 条件逻辑 | Switch → 多个输出 |
| 合并 | 合并输入 | 多个 → Join |
| 循环 | 重复操作 | Function 带计数器 |

### 节点配置

| 步骤 | 操作 | 备注 |
|------|------|------|
| 1 | 拖拽节点 | 从调色板 |
| 2 | 双击 | 打开设置 |
| 3 | 配置 | 设置属性 |
| 4 | 连线 | 连接到其他节点 |
| 5 | 部署 | 应用变更 |

### 调试流程

| 工具 | 描述 | 用途 |
|------|------|------|
| Debug 节点 | 输出到侧边栏 | 查看消息 |
| Status 节点 | 节点状态 | 监控健康 |
| Catch 节点 | 错误处理 | 处理失败 |
| Complete 节点 | 流程完成 | 后处理 |

---

## 常用节点

构建 Node-RED 流程的必备节点。

### 输入节点

| 节点 | 用途 | 配置 |
|------|------|------|
| Inject | 手动/定时触发 | 间隔、payload |
| HTTP Request | API 调用 | URL、方法 |
| MQTT In | MQTT 消息 | Broker、topic |
| WebSocket | 实时数据 | URL、events |

### 处理节点

| 节点 | 用途 | 用例 |
|------|------|------|
| Function | 自定义 JavaScript | 复杂逻辑 |
| Switch | 条件路由 | If/else |
| Change | 修改消息 | 转换数据 |
| JSON | 解析/序列化 | 数据转换 |
| Delay | 速率限制 | 节流消息 |

### 输出节点

| 节点 | 用途 | 配置 |
|------|------|------|
| Debug | 在侧边栏查看 | 显示选项 |
| HTTP Response | API 响应 | 状态、headers |
| MQTT Out | 发布 MQTT | Broker、topic |
| Email | 发送邮件 | SMTP 设置 |
| File | 写入文件 | 路径、格式 |

### 存储节点

| 节点 | 用途 | 存储类型 |
|------|------|----------|
| File | 读写文件 | 本地文件系统 |
| SQLite | 数据库操作 | SQLite 数据库 |
| Context | 内存存储 | Flow/全局上下文 |
| Redis | 缓存/存储 | Redis 数据库 |

### Function 节点示例

```javascript
// Transform payload
msg.payload = msg.payload.toUpperCase();
return msg;

// Conditional logic
if (msg.payload > 100) {
  return [msg, null]; // First output
} else {
  return [null, msg]; // Second output
}

// Create new message
return {
  payload: {
    temperature: msg.payload,
    timestamp: Date.now()
  }
};
```

---

## IoT 协议

Node-RED 支持各种 IoT 通信协议。

### MQTT

| 设置 | 描述 | 示例 |
|------|------|------|
| Broker | MQTT 服务器 | mqtt://localhost |
| Port | 连接端口 | 1883 |
| Topic | 消息频道 | home/temperature |
| QoS | 服务质量 | 0, 1, 或 2 |

### MQTT 配置

| 属性 | 选项 | 推荐 |
|------|------|------|
| Clean session | True/False | 新连接用 True |
| Keepalive | 秒 | 60 |
| Username | 凭据 | 如需要 |
| Password | 凭据 | 如需要 |

### HTTP/REST

| 方法 | 用途 | 节点 |
|------|------|------|
| GET | 获取数据 | HTTP Request |
| POST | 创建数据 | HTTP Request |
| PUT | 更新数据 | HTTP Request |
| DELETE | 删除数据 | HTTP Request |

### WebSocket

| 模式 | 描述 | 用途 |
|------|------|------|
| Listener | 接受连接 | 服务器 |
| Client | 连接到服务器 | 客户端 |
| 双向 | 双向通信 | 实时 |

### CoAP

| 功能 | 描述 | 用途 |
|------|------|------|
| 轻量级 | 基于 UDP | 受限设备 |
| RESTful | 类似 HTTP | IoT 传感器 |
| Observe | 订阅变更 | 实时更新 |

### 协议对比

| 协议 | 传输 | 开销 | 用途 |
|------|------|------|------|
| MQTT | TCP | 低 | IoT 消息 |
| HTTP | TCP | 中等 | API 集成 |
| WebSocket | TCP | 低 | 实时 Web |
| CoAP | UDP | 极低 | 受限设备 |

---

## 仪表板与 UI

创建用于监控和控制的可视化仪表板。

### 仪表板安装

```bash
# Install dashboard nodes
cd ~/.node-red
npm install node-red-dashboard
```

### 仪表板组件

| 组件 | 用途 | 示例 |
|------|------|------|
| Chart | 数据可视化 | 温度图表 |
| Gauge | 单个值 | 速度计 |
| Switch | 开关控制 | 灯光开/关 |
| Slider | 值输入 | 亮度控制 |
| Text | 显示值 | 状态消息 |

### 仪表板布局

| 元素 | 描述 | 配置 |
|------|------|------|
| Tab | 页面 | 多个标签页 |
| Group | 区域 | 组织组件 |
| Widget | 单个 UI | 大小、位置 |

### 创建仪表板

| 步骤 | 操作 | 结果 |
|------|------|------|
| 1 | 添加标签页 | 仪表板页面 |
| 2 | 添加分组 | 区域 |
| 3 | 添加组件 | UI 元素 |
| 4 | 连接数据 | 连接到流程 |
| 5 | 访问 | http://localhost:1880/ui |

### 仪表板组件

| 组件 | 输入 | 显示 |
|------|------|------|
| Chart | 时间序列 | 折线/柱状图 |
| Gauge | 数字 | 表盘显示 |
| Switch | 布尔 | 切换按钮 |
| Slider | 数字 | 范围输入 |
| Text | 字符串 | 文本显示 |
| Button | 点击 | 操作触发 |

### 样式选项

| 属性 | 选项 | 效果 |
|------|------|------|
| 颜色 | 主题色 | 组件颜色 |
| 大小 | 小、中、大 | 组件大小 |
| 标签 | 自定义文本 | 显示名称 |
| 图标 | Material 图标 | 可视指示器 |

---

## 部署与安全部署

在生产环境中安全部署 Node-RED。

### 部署选项

| 选项 | 优点 | 缺点 |
|------|------|------|
| 本地 | 简单 | 访问受限 |
| Docker | 隔离 | 需要 Docker 知识 |
| 云 | 可扩展 | 成本 |
| Raspberry Pi | 低功耗 | 资源有限 |

### 安全配置

| 设置 | 默认值 | 推荐 |
|------|--------|------|
| 认证 | 无 | 启用 |
| HTTPS | 否 | 启用 |
| API 安全 | 无 | 基于 Token |
| 流程保护 | 无 | 用户只读 |

### 启用认证

```javascript
// settings.js
module.exports = {
  adminAuth: {
    type: "credentials",
    users: [{
      username: "admin",
      password: "$2b$08$...",
      permissions: "*"
    }]
  }
};
```

### HTTPS 配置

```javascript
// settings.js
module.exports = {
  https: {
    key: fs.readFileSync('key.pem'),
    cert: fs.readFileSync('cert.pem')
  },
  requireHttps: true
};
```

### 备份与恢复

| 方式 | 命令 | 频率 |
|------|------|------|
| 导出流程 | 编辑器 → 导出 | 变更前 |
| 导入流程 | 编辑器 → 导入 | 恢复 |
| 文件备份 | 复制 .node-red | 每周 |
| Git | 版本控制 | 持续 |

### 性能优化

| 方面 | 操作 | 效果 |
|------|------|------|
| 内存 | 增加 Node.js 堆 | 处理更多流程 |
| 上下文 | 限制存储大小 | 防止内存泄漏 |
| 日志 | 降低详细度 | 减少 I/O |
| 节点 | 禁用未使用 | 降低 CPU |

### 监控

| 指标 | 工具 | 阈值 |
|------|------|------|
| CPU | 系统工具 | < 80% |
| 内存 | 系统工具 | < 80% |
| 消息 | Debug 节点 | 监控速率 |
| 错误 | Catch 节点 | 理想为零 |

---

## 总结

| 主题 | 核心要点 |
|------|----------|
| 安装 | Docker 简化部署 |
| 概念 | 节点、连线、流程、消息 |
| 构建 | 可视化编辑器创建流程 |
| 协议 | 支持 MQTT、HTTP、WebSocket |
| 仪表板 | 内置可视化 |
| 安全 | 启用认证和 HTTPS |
