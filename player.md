# 使用 Koel 搭建音乐播放器

## 简介

Koel 是一个开源音乐流媒体服务器，允许您从任何地方托管和播放个人音乐收藏。它提供了一个现代化的 Web 界面，并支持多种音频格式。

### 什么是 Koel？

Koel 是一个自托管音乐流媒体平台，可以索引您的音乐库并提供基于 Web 的播放器界面。

| 特性 | 描述 |
|------|------|
| Web 播放器 | 现代化的音乐播放 UI |
| 音乐串流 | 通过任何有浏览器的设备播放 |
| 播放列表管理 | 创建和管理播放列表 |
| 用户管理 | 多用户独立音乐库 |
| 专辑封面 | 自动获取专辑封面 |

### 与其他方案的比较

| 特性 | Koel | Plex | Jellyfin |
|------|------|------|----------|
| 专注 | 仅音乐 | 多媒体 | 多媒体 |
| Web 界面 | 是 | 是 | 是 |
| 移动应用 | 第三方 | 官方 | 官方 |
| 转码 | 是 | 是 | 是 |
| 自托管 | 是 | 是 | 是 |

## 安装

### 前置要求

| 要求 | 最低版本 |
|------|----------|
| PHP | 8.1 或更高 |
| Composer | 2.0 或更高 |
| Node.js | 16.0 或更高 |
| 数据库 | MySQL 或 MariaDB |
| Web 服务器 | Nginx 或 Apache |

### 安装步骤

```bash
git clone https://github.com/koel/koel.git
cd koel
composer install
npm install
npm run build
php artisan koel:init
```

### 环境配置

```env
APP_NAME=Koel
APP_URL=https://music.example.com
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=koel
DB_USERNAME=root
DB_PASSWORD=secret
MEDIA_PATH=/path/to/music
```

### 数据库设置

```bash
php artisan migrate
php artisan db:seed
```

## Web 服务器配置

### Nginx 配置

```nginx
server {
    listen 80;
    server_name music.example.com;
    root /var/www/koel/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

### Apache 配置

```apache
<VirtualHost *:80>
    ServerName music.example.com
    DocumentRoot /var/www/koel/public
    <Directory /var/www/koel/public>
        AllowOverride All
        Require all granted
    </Directory>
</VirtualHost>
```

## 音乐库管理

### 支持的格式

| 格式 | 扩展名 | 质量 |
|------|--------|------|
| MP3 | .mp3 | 良好 |
| FLAC | .flac | 无损 |
| OGG | .ogg | 良好 |
| AAC | .m4a | 良好 |
| WAV | .wav | 无损 |

### 扫描音乐

将音乐文件添加到媒体路径后，扫描音乐库：

```bash
php artisan koel:sync
```

### 音乐库结构

```
/path/to/music/
├── Artist Name/
│   ├── Album Name/
│   │   ├── 01 - Track Name.mp3
│   │   ├── 02 - Track Name.mp3
│   │   └── cover.jpg
│   └── Another Album/
│       └── 01 - Track Name.flac
└── Various Artists/
    └── Compilation/
        └── 01 - Track Name.mp3
```

## 用户管理

### 创建用户

```bash
php artisan koel:user:create
```

### 用户角色

| 角色 | 权限 |
|------|------|
| Admin | 完全访问权限，管理用户 |
| User | 播放音乐，管理自己的播放列表 |

### 用户配置

```bash
# 更改用户密码
php artisan koel:user:change-password

# 删除用户
php artisan koel:user:delete
```

## 播放功能

### 音频串流

Koel 支持多种串流方式：

| 方式 | 描述 | 用例 |
|------|------|------|
| 直接 | 直接串流文件 | 局域网 |
| 转码 | 实时转换 | 远程串流 |
| 渐进式 | 下载后播放 | 低带宽 |

### 转码设置

```env
TRANSCODE_FLAC=true
TRANSCODE_MP3_320=true
TRANSCODE_CACHE_PATH=/tmp/koel-transcode
```

### 播放列表管理

| 功能 | 描述 |
|------|------|
| 创建播放列表 | 将歌曲分组为收藏 |
| 智能播放列表 | 基于规则自动生成 |
| 分享播放列表 | 与其他用户分享 |
| 导出播放列表 | 下载播放列表数据 |

## API 访问

### REST API 端点

| 端点 | 方法 | 描述 |
|------|------|------|
| `/api/songs` | GET | 列出所有歌曲 |
| `/api/albums` | GET | 列出所有专辑 |
| `/api/artists` | GET | 列出所有艺术家 |
| `/api/playlists` | GET | 列出播放列表 |
| `/api/search` | GET | 搜索音乐库 |

### 身份验证

```bash
# 获取 API 令牌
curl -X POST https://music.example.com/api/me \
  -d "email=user@example.com" \
  -d "password=password"
```

### API 使用示例

```bash
# 列出歌曲
curl -H "Authorization: Bearer TOKEN" \
  https://music.example.com/api/songs

# 创建播放列表
curl -X POST https://music.example.com/api/playlists \
  -H "Authorization: Bearer TOKEN" \
  -d "name=My Playlist"
```

## Docker 部署

### Docker Compose

```yaml
version: '3'
services:
  koel:
    image: koel/koel
    ports:
      - "8080:80"
    environment:
      - DB_CONNECTION=mysql
      - DB_HOST=db
      - DB_DATABASE=koel
      - DB_USERNAME=koel
      - DB_PASSWORD=secret
      - MEDIA_PATH=/music
    volumes:
      - /path/to/music:/music

  db:
    image: mysql:8.0
    environment:
      - MYSQL_ROOT_PASSWORD=secret
      - MYSQL_DATABASE=koel
      - MYSQL_USER=koel
      - MYSQL_PASSWORD=secret
    volumes:
      - mysql_data:/var/lib/mysql

volumes:
  mysql_data:
```

### 使用 Docker 运行

```bash
docker-compose up -d
```

## 移动端访问

### 移动应用

| 应用 | 平台 | 状态 |
|------|------|------|
| Amperfy | iOS | 第三方 |
| Ultrasonic | Android | 第三方 |
| Web 浏览器 | 任意 | 原生 |

### Subsonic API

Koel 实现了 Subsonic API，兼容许多第三方客户端。

## 性能优化

### 缓存配置

```env
CACHE_DRIVER=redis
SESSION_DRIVER=redis
QUEUE_CONNECTION=redis
```

### PHP 优化

```ini
memory_limit = 256M
max_execution_time = 60
upload_max_filesize = 50M
```

## 安全

### HTTPS 配置

```nginx
server {
    listen 443 ssl;
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;
}
```

### 安全最佳实践

| 实践 | 描述 |
|------|------|
| 使用 HTTPS | 加密所有连接 |
| 强密码 | 强制密码要求 |
| 定期更新 | 保持 Koel 更新 |
| 防火墙 | 限制访问必要端口 |
| 备份 | 定期备份数据库和文件 |

## 总结

| 组件 | 用途 |
|------|------|
| Web UI | 音乐浏览和播放 |
| REST API | 编程访问 |
| Subsonic API | 移动应用兼容性 |
| 转码 | 格式转换用于串流 |
| 用户系统 | 多用户支持 |
