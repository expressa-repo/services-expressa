# PHP 5.6 Expressa

Service PHP 5.6 dengan Apache/Nginx dan dashboard test untuk koneksi database.

## 🚀 Quick Start

```bash
# 1. WAJIB: Pastikan network sudah dibuat
docker network create expressa-net

# 2. Start service
docker-compose up -d

# 3. Akses dashboard
# Browser: http://localhost:8056
# Curl: curl http://localhost:8056
```

## 📋 Informasi Service

- **Image**: `jdanuc7/php56-expressa:latest`
- **Container**: `php56-expressa`
- **Port**: 8056
- **Network**: `expressa-net`
- **Volume**: `./app` → `/var/www/html`

## 🔧 Konfigurasi (.env)

```bash
# Application
APP_NAME=PHP56-Expressa
APP_ENV=development
TZ=Asia/Jakarta

# Web Server
WEB_PORT=8056

# PHP Settings
PHP_MEMORY_LIMIT=256M
PHP_MAX_EXECUTION_TIME=300
PHP_UPLOAD_MAX_FILESIZE=100M
PHP_POST_MAX_SIZE=100M
```

## 🧪 Test Dashboard

Akses http://localhost:8056 untuk dashboard dengan fitur:

- PHP version info dan server status
- Database connection tests
- Extension checks
- Test scripts navigation

### Available Test Scripts

- `/mysql.php` - Comprehensive MySQL test dengan UI lengkap
- `/test-mysql.php` - Quick MySQL connection test
- `/simple-test.php` - Simple connection test
- `/phpinfo.php` - PHP configuration info

## 🛠️ Management Commands

```bash
# Basic Docker commands
docker-compose up -d      # Start container
docker-compose down       # Stop container
docker-compose restart    # Restart container
docker-compose logs -f    # Show logs

# Container access
docker-compose exec php56 bash  # Access shell
docker-compose exec php56 php -v  # Check PHP version
```

## 🔗 Database Connection

### MySQL Configuration

```php
$host = 'mysql57-expressa';  // Container name
$port = 3306;
$database = 'test_db';
$username = 'svc_my3xp';
$password = 'MyP4ss_9494!';
```

### External Access

- **Host**: 127.0.0.1:3306
- **Database**: test_db
- **Username**: svc_my3xp
- **Password**: MyP4ss_9494!

## 🔍 Troubleshooting

### 502 Bad Gateway

```bash
# Check container status
docker-compose ps

# Check logs for errors
docker-compose logs -f php56

# Restart container
docker-compose restart
```

### Container Issues

```bash
# Check status
docker-compose ps
docker ps

# Check logs
docker-compose logs -f

# Restart service
docker-compose restart
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
php56/
├── .env                 # Environment configuration
├── docker-compose.yml   # Docker compose config
└── app/                # Web application files (auto-generated)
    ├── index.php       # Main dashboard
    ├── mysql.php       # MySQL test (detailed)
    ├── test-mysql.php  # MySQL test (quick)
    ├── simple-test.php # Simple test
    └── phpinfo.php     # PHP info
```

## 🔄 Development

### Menambah Script Test

1. Buat file PHP baru di folder `app/`
2. Akses via http://localhost:8056/filename.php

### Custom Configuration

1. Edit file `.env` untuk mengubah setting
2. Restart container: `docker-compose restart`

---

**PHP 5.6 Expressa** - Development environment dengan test dashboard
