# Expressa Development Environment

Paket development PHP beserta service database yang terdiri dari **PHP 5.6**, **PHP 7.4**, **MySQL 5.7**, dan **PostgreSQL 16**.

## 🎯 Installation

```bash
git clone https://github.com/expressa-repo/services-expressa.git
cd services-expressa
```

## ⚠️ WAJIB: Buat Network Terlebih Dahulu

```bash
docker network create expressa-net
```

## 📋 Daftar Service

| Service       | Port | Akses                 | README                                           |
| ------------- | ---- | --------------------- | ------------------------------------------------ |
| PHP 5.6       | 8056 | http://localhost:8056 | [php56/README.md](php56/README.md)               |
| PHP 7.4       | 8074 | http://localhost:8074 | [php74/README.md](php74/README.md)               |
| MySQL 5.7     | 3306 | localhost:3306        | [mysql57/README.md](mysql57/README.md)           |
| PostgreSQL 16 | 9494 | localhost:9494        | [postgresql16/README.md](postgresql16/README.md) |

## 🚀 Quick Start

```bash
# 1. WAJIB: Buat network
docker network create expressa-net

# 2. Start service yang dibutuhkan
cd php56 && docker-compose up -d    # PHP 5.6
cd mysql57 && docker-compose up -d  # MySQL 5.7
cd php74 && docker-compose up -d    # PHP 7.4
cd postgresql16 && docker-compose up -d  # PostgreSQL 16
```

## 📖 Dokumentasi Detail

Setiap service memiliki dokumentasi lengkap di folder masing-masing:

- **[php56/README.md](php56/README.md)** - PHP 5.6 dengan test dashboard
- **[php74/README.md](php74/README.md)** - PHP 7.4 dengan PHPInfo
- **[mysql57/README.md](mysql57/README.md)** - MySQL 5.7 server
- **[postgresql16/README.md](postgresql16/README.md)** - PostgreSQL 16 server

## � Troubleshooting

### Network Error

```bash
# Pastikan network sudah dibuat
docker network create expressa-net
```

### Port Conflict

Edit file `.env` di masing-masing service untuk mengubah port.

---

**Expressa Development Environment** - Paket lengkap development PHP dan database
