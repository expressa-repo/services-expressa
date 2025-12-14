# Services Expressa

Koleksi service development PHP dan database menggunakan Docker. Setiap service tersedia dalam branch terpisah untuk fleksibilitas maksimal.

## 🎯 Available Services

| Service       | Branch         | Port | Description                         |
| ------------- | -------------- | ---- | ----------------------------------- |
| PHP 5.6       | `php56`        | 8056 | PHP 5.6 dengan test dashboard MySQL |
| PHP 7.4       | `php74`        | 8074 | PHP 7.4 modern development          |
| MySQL 5.7     | `mysql57`      | 3306 | MySQL 5.7 database server           |
| PostgreSQL 16 | `postgresql16` | 9494 | PostgreSQL 16 database server       |

## 🚀 Quick Start

### Clone Service Tertentu

```bash
# Clone PHP 5.6 saja
git clone -b php56 https://github.com/username/services-expressa.git php56-expressa
cd php56-expressa

# Clone MySQL 5.7 saja
git clone -b mysql57 https://github.com/username/services-expressa.git mysql57-expressa
cd mysql57-expressa

# Clone PHP 7.4 saja
git clone -b php74 https://github.com/username/services-expressa.git php74-expressa
cd php74-expressa

# Clone PostgreSQL 16 saja
git clone -b postgresql16 https://github.com/username/services-expressa.git postgresql16-expressa
cd postgresql16-expressa
```

### Clone Multiple Services

```bash
# Setup workspace
mkdir expressa-workspace && cd expressa-workspace

# Clone services yang dibutuhkan
git clone -b php56 https://github.com/username/services-expressa.git php56
git clone -b mysql57 https://github.com/username/services-expressa.git mysql57

# atau kombinasi lain
git clone -b php74 https://github.com/username/services-expressa.git php74
git clone -b postgresql16 https://github.com/username/services-expressa.git postgresql16
```

## ⚠️ WAJIB: Setup Network

Sebelum menjalankan service apapun:

```bash
docker network create expressa-net
```

## 🔧 Setup Environment

Setiap service memiliki `.env.example` yang bisa langsung digunakan:

```bash
# Masuk ke folder service
cd php56  # atau mysql57, php74, postgresql16

# Copy environment file
cp .env.example .env

# Start service
docker-compose up -d
```

## 📖 Dokumentasi Lengkap

Setiap branch memiliki README lengkap dengan:

- Setup dan konfigurasi detail
- Management commands
- Database connection examples
- Troubleshooting guide
- Development tips

### Branch Documentation:

- **[php56 branch](https://github.com/username/services-expressa/tree/php56)** - PHP 5.6 dengan MySQL test dashboard
- **[php74 branch](https://github.com/username/services-expressa/tree/php74)** - PHP 7.4 modern development
- **[mysql57 branch](https://github.com/username/services-expressa/tree/mysql57)** - MySQL 5.7 database server
- **[postgresql16 branch](https://github.com/username/services-expressa/tree/postgresql16)** - PostgreSQL 16 database server

## 🎯 Use Cases

### Development Stack: PHP 5.6 + MySQL

```bash
mkdir php56-mysql-stack && cd php56-mysql-stack
git clone -b mysql57 https://github.com/username/services-expressa.git mysql57
git clone -b php56 https://github.com/username/services-expressa.git php56

# Setup
docker network create expressa-net
cd mysql57 && cp .env.example .env && docker-compose up -d && cd ..
cd php56 && cp .env.example .env && docker-compose up -d && cd ..

# Access: http://localhost:8056
```

### Development Stack: PHP 7.4 + PostgreSQL

```bash
mkdir php74-postgres-stack && cd php74-postgres-stack
git clone -b postgresql16 https://github.com/username/services-expressa.git postgresql16
git clone -b php74 https://github.com/username/services-expressa.git php74

# Setup
docker network create expressa-net
cd postgresql16 && cp .env.example .env && docker-compose up -d && cd ..
cd php74 && cp .env.example .env && docker-compose up -d && cd ..

# Access: http://localhost:8074
```

### Database Only

```bash
# Hanya butuh MySQL
git clone -b mysql57 https://github.com/username/services-expressa.git mysql57
cd mysql57 && cp .env.example .env && docker-compose up -d

# Hanya butuh PostgreSQL
git clone -b postgresql16 https://github.com/username/services-expressa.git postgresql16
cd postgresql16 && cp .env.example .env && docker-compose up -d
```

## 🔍 Troubleshooting

### Network Issues

```bash
# Pastikan network sudah dibuat
docker network create expressa-net
docker network ls | grep expressa-net
```

### Port Conflicts

Edit file `.env` di service yang bentrok:

```bash
# Contoh: ubah port PHP 5.6
cd php56
nano .env  # ubah WEB_PORT=8056 ke WEB_PORT=8057
docker-compose up -d
```

## 🤝 Contributing

1. Fork repository
2. Buat branch untuk service baru atau update existing
3. Submit pull request ke branch yang sesuai

---

**Services Expressa** - Modular development services untuk PHP dan database

## 📝 Migration Guide

Jika Anda sudah menggunakan versi monorepo sebelumnya:

### Dari Monorepo ke Branch Terpisah

```bash
# Backup existing work
cp -r php56/app php56-app-backup
cp -r php74/app php74-app-backup

# Clone branch baru
git clone -b php56 https://github.com/username/services-expressa.git php56-new
git clone -b php74 https://github.com/username/services-expressa.git php74-new

# Restore aplikasi
cp -r php56-app-backup/* php56-new/app/
cp -r php74-app-backup/* php74-new/app/

# Setup environment
cd php56-new && cp .env.example .env && docker-compose up -d
cd php74-new && cp .env.example .env && docker-compose up -d
```
