# PHP 7.4 Expressa

Service PHP 7.4 dengan Apache/Nginx untuk development modern.

## 🚀 Quick Start

```bash
# 1. WAJIB: Pastikan network sudah dibuat
docker network create expressa-net

# 2. Start service
docker-compose up -d

# 3. Akses PHPInfo
# Browser: http://localhost:8074
# Curl: curl http://localhost:8074
```

## 📋 Informasi Service

- **Image**: `jdanuc7/php74-expressa:latest`
- **Container**: `php74-expressa`
- **Port**: 8074
- **Network**: `expressa-net`
- **Volume**: `./app` → `/var/www/html`

## 🔧 Konfigurasi (.env)

```bash
# Application
APP_NAME=PHP74-Expressa
APP_ENV=development
TZ=Asia/Jakarta

# Web Server
WEB_PORT=8074

# PHP Settings
PHP_MEMORY_LIMIT=256M
PHP_MAX_EXECUTION_TIME=300
PHP_UPLOAD_MAX_FILESIZE=100M
PHP_POST_MAX_SIZE=100M
```

## 🔗 Database Connection

### PostgreSQL Configuration

```php
$host = 'postgresql16-expressa';  // Container name
$port = 5432;
$database = 'expressa_db';
$username = 'svc_pg3xp';
$password = 'PgP4ss_s9494!';
```

### MySQL Configuration (jika menggunakan MySQL)

```php
$host = 'mysql57-expressa';  // Container name
$port = 3306;
$database = 'test_db';
$username = 'svc_my3xp';
$password = 'MyP4ss_9494!';
```

## 🛠️ Management Commands

```bash
# Basic Docker commands
docker-compose up -d      # Start service
docker-compose down       # Stop service
docker-compose restart    # Restart service
docker-compose logs -f    # Show logs

# Container access
docker-compose exec php74 bash  # Access shell
docker-compose exec php74 php -v  # Check PHP version
```

## 🔍 Troubleshooting

### Service Not Starting

```bash
# Check container status
docker-compose ps

# Check logs for errors
docker-compose logs -f

# Restart service
docker-compose restart
```

### Port Conflict

```bash
# Edit .env file
WEB_PORT=8075  # Change to available port

# Restart service
docker-compose down && docker-compose up -d
```

### Network Issues

```bash
# Verify network exists
docker network ls | grep expressa-net

# Create if missing
docker network create expressa-net

# Restart container
docker-compose down && docker-compose up -d
```

## 📁 File Structure

```
php74/
├── .env                 # Environment configuration
├── docker-compose.yml   # Docker compose config
└── app/                # Web application files
```

## 🔄 Development

### Menambah Aplikasi

1. Buat file PHP di folder `app/`
2. Akses via http://localhost:8074/filename.php

### Custom Extensions

Jika perlu extension tambahan, buat Dockerfile custom atau gunakan image yang sudah include extension yang dibutuhkan.

---

**PHP 7.4 Expressa** - Modern PHP development environment
