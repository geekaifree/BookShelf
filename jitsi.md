# 使用 Jitsi Meet 进行视频会议

## 简介

Jitsi Meet 是一个免费开源的视频会议平台。它提供安全的、加密的视频会议，直接在浏览器中运行，无需下载或注册账户。本教程涵盖安装、配置、功能和集成选项。

## 架构概览

| 组件 | 描述 | 角色 |
|------|------|------|
| Jitsi Videobridge (JVB) | 媒体服务器 | 路由音频/视频流 |
| Jicofo | 会议焦点 | 管理会议会话 |
| Prosody | XMPP 服务器 | 认证和信令 |
| Jitsi Meet | Web 应用 | 用户界面 |
| Jibri | 录制机器人 | 录制和直播 |
| TURN/STUN | NAT 穿透 | 穿过防火墙的连接 |

## 系统要求

| 组件 | 最低配置 | 推荐配置 |
|------|----------|----------|
| CPU | 2 核 | 4+ 核 |
| RAM | 4 GB | 8 GB+ |
| 网络 | 100 Mbps | 1 Gbps |
| 操作系统 | Ubuntu 20.04+ | Ubuntu 22.04 |
| 端口 | 80, 443, 10000/UDP | 全部开放 |
| 存储 | 20 GB | 50+ GB |

## 安装

### Docker Compose 设置

```yaml
version: "3.8"

services:
  jitsi-meet:
    image: jitsi/meet:latest
    container_name: jitsi-meet
    restart: unless-stopped
    ports:
      - "8443:443"
      - "8080:80"
      - "10000:10000/udp"
    volumes:
      - ./config:/config
      - ./web:/usr/share/jitsi-meet
    environment:
      - ENABLE_AUTH=0
      - PUBLIC_URL=https://meet.example.com
      - ENABLE_OCTO=0

  prosody:
    image: jitsi/prosody:latest
    container_name: prosody
    restart: unless-stopped
    volumes:
      - ./config/prosody:/config

  jicofo:
    image: jitsi/jicofo:latest
    container_name: jicofo
    restart: unless-stopped
    volumes:
      - ./config/jicofo:/config

  jvb:
    image: jitsi/jvb:latest
    container_name: jvb
    restart: unless-stopped
    ports:
      - "10000:10000/udp"
    volumes:
      - ./config/jvb:/config
```

### Docker 快速开始

```bash
# 克隆仓库
git clone https://github.com/jitsi/docker-jitsi-meet
cd docker-jitsi-meet

# 复制环境文件
cp env.example .env

# 生成密码
./gen-passwords.sh

# 启动服务栈
docker compose up -d
```

## 使用 Jitsi Meet

### 开始会议

| 方法 | 步骤 |
|------|------|
| 直接 URL | 导航到 `https://your-server/room-name` |
| 随机房间 | 访问首页，点击 "Start meeting" |
| 共享链接 | 与参与者分享房间 URL |
| 嵌入 | 使用 iframe 集成 |

### 会议界面

| 元素 | 位置 | 功能 |
|------|------|------|
| Video Grid | 中央 | 参与者视频流 |
| Chat Panel | 右侧 | 文字消息 |
| Participants | 右侧 | 参与者列表 |
| Toolbar | 底部 | 会议控制 |
| Settings | 齿轮图标 | 音视频设置 |

### 会议控制

| 控制 | 图标 | 功能 |
|------|------|------|
| Microphone | 麦克风 | 切换音频 |
| Camera | 视频 | 切换视频 |
| Screen Share | 显示器 | 共享屏幕 |
| Chat | 消息 | 打开聊天 |
| Participants | 人 | 显示参与者 |
| Raise Hand | 手 | 信号发言者 |
| Reactions | 表情 | 发送反应 |
| Record | 圆圈 | 开始录制 |
| Leave | 电话 | 退出会议 |

## 参与者功能

### 视频布局

| 布局 | 描述 | 用途 |
|------|------|------|
| Grid | 等大小格子 | 小型会议 |
| Stage | 大活跃发言者 | 演示 |
| Sidebar | 活跃发言者加侧栏 | 混合内容 |
| Vertical Filmstrip | 发言者加垂直条 | 网络研讨会 |

### 音频选项

| 选项 | 描述 | 用途 |
|------|------|------|
| Noise suppression | 减少背景噪音 | 家庭环境 |
| Echo cancellation | 防止音频反馈 | 内置扬声器 |
| Auto gain | 标准化音量 | 一致电平 |
| Stereo audio | 空间音频 | 音乐表演 |

### 视频选项

| 选项 | 描述 | 用途 |
|------|------|------|
| Virtual background | 替换背景 | 隐私 |
| Blur background | 模糊背景 | 减少干扰 |
| Mirror video | 翻转自拍视图 | 自然外观 |
| Low bandwidth | 降低视频质量 | 慢速连接 |
| HD video | 高分辨率 | 快速连接 |

## 管理工具

### 主持人权限

| 操作 | 主持人 | 参与者 |
|------|--------|--------|
| 静音他人 | 是 | 否 |
| 踢出用户 | 是 | 否 |
| 开始录制 | 是 | 否 |
| 锁定房间 | 是 | 否 |
| 设置等候室 | 是 | 否 |
| 启用屏幕共享 | 控制 | 请求 |

### 安全设置

| 设置 | 描述 | 默认值 |
|------|------|--------|
| Lobby | 等候室 | 关闭 |
| Room lock | 密码保护 | 关闭 |
| End-to-end encryption | 加密媒体 | 关闭 |
| Authentication | 要求登录 | 关闭 |
| Guest access | 允许匿名 | 开启 |

### 启用等候室

1. 打开安全选项（盾牌图标）
2. 启用 "Enable Lobby"
3. 参与者等待主持人批准
4. 从等候队列中批准或拒绝

## 屏幕共享

### 共享选项

| 类型 | 内容 | 质量 |
|------|------|------|
| Full screen | 整个显示 | 高 |
| Window | 特定应用 | 高 |
| Browser tab | Chrome/Edge 标签页 | 高带音频 |
| Whiteboard | 绘图画布 | 不适用 |

### 共享提示

| 提示 | 描述 |
|------|------|
| 关闭不必要的标签页 | 减少干扰 |
| 使用演示者视图 | 用于幻灯片 |
| 共享标签页音频 | 用于视频播放时启用 |
| 为视频优化 | 共享视频时启用 |

## 录制

### Jibri 设置

```yaml
# 添加到 docker-compose.yml
services:
  jibri:
    image: jitsi/jibri:latest
    container_name: jibri
    restart: unless-stopped
    volumes:
      - ./config/jibri:/config
      - ./recordings:/config/recordings
    environment:
      - ENABLE_RECORDING=1
      - JIBRI_RECORDING_DIR=/config/recordings
```

### 录制选项

| 选项 | 描述 | 格式 |
|------|------|------|
| Local recording | 保存到服务器 | MP4 |
| Live streaming | 串流到 YouTube/RTMP | 串流 |
| Dropbox | 保存到 Dropbox | MP4 |

## 集成

### 嵌入网站

```html
<iframe
  src="https://your-server/room-name"
  allow="camera; microphone; fullscreen; display-capture"
  style="height: 100%; width: 100%; border: 0;">
</iframe>
```

### Iframe API

```javascript
const domain = 'meet.your-server.com';
const options = {
  roomName: 'MyMeeting',
  width: 800,
  height: 600,
  parentNode: document.querySelector('#meet'),
  configOverwrite: {
    startWithAudioMuted: true,
    startWithVideoMuted: false
  }
};
const api = new JitsiMeetExternalAPI(domain, options);

// Event listeners
api.addEventListener('participantJoined', (event) => {
  console.log('Participant joined:', event.displayName);
});

api.addEventListener('readyToClose', () => {
  console.log('Meeting ended');
});
```

### API 事件

| 事件 | 描述 | 数据 |
|------|------|------|
| participantJoined | 用户加入 | displayName, id |
| participantLeft | 用户离开 | displayName, id |
| audioMuteStatusChanged | 音频切换 | muted |
| videoMuteStatusChanged | 视频切换 | muted |
| readyToClose | 会议结束 | 无 |

## 自定义

### 品牌选项

| 元素 | 自定义 | 方法 |
|------|--------|------|
| Logo | 公司标志 | 配置文件 |
| Background | 自定义壁纸 | 配置文件 |
| Colors | 品牌颜色 | CSS 覆盖 |
| Welcome page | 自定义消息 | 配置文件 |

### 配置覆盖

```javascript
// 在 config.js 中
configOverwrite = {
  startWithAudioMuted: true,
  startWithVideoMuted: false,
  disableDeepLinking: true,
  enableClosePage: false,
  toolbarButtons: [
    'microphone', 'camera', 'closedcaptions',
    'desktop', 'fullscreen', 'hangup',
    'chat', 'recording', 'livestreaming',
    'settings', 'raisehand'
  ]
};
```

## 性能优化

### 服务器扩展

| 用户 | 服务器 | JVB 实例 | 架构 |
|------|--------|----------|------|
| 1-50 | 1 | 1 | 单服务器 |
| 50-200 | 1-2 | 1-2 | 负载均衡 |
| 200-500 | 2-3 | 3-5 | 多 JVB |
| 500+ | 3+ | 5+ | Octo 网状 |

### 网络优化

| 设置 | 建议 | 影响 |
|------|------|------|
| UDP preferred | 是 | 更低延迟 |
| Bandwidth limits | 按层级配置 | 质量管理 |
| TURN server | 为 NAT 配置 | 连接性 |
| STUN servers | 多个来源 | NAT 发现 |

## 故障排除

| 问题 | 可能原因 | 解决方案 |
|------|----------|----------|
| 无音频 | 麦克风被阻止 | 检查浏览器权限 |
| 视频质量差 | 带宽限制 | 降低视频质量 |
| 断开连接 | 网络不稳定 | 检查连接 |
| 无法录制 | Jibri 未配置 | 设置 Jibri 服务 |
| 无法加入 | 防火墙阻止 | 打开所需端口 |

## 总结

Jitsi Meet 提供了一个安全的自托管视频会议解决方案，适合个人和组织使用。其基于浏览器的方式消除了安装障碍，同时提供专业的会议功能。

关键实践：

- 使用 Docker 部署以便管理
- 为敏感会议启用等候室和认证
- 使用硬件加速进行录制
- 为防火墙后面的用户配置 TURN 服务器
- 使用 iframe API 将会议嵌入 Web 应用
- 监控服务器资源以做出扩展决策
