# PostgreSQL 16 Expressa

Service PostgreSQL 16 server untuk development dengan persistent storage dan health monitoring.

## 🚀 Quick Start

```bash
# 1. WAJIB: Pastikan network sudah dibuat
docker network create expressa-net

# 2. Start PostgreSQL service
docker-compose up -d

# 3. Tunggu PostgreSQL ready (30-60 detik)
docker-compose logs -f postgresql

# 4. Test koneksi
psql -h 127.0.0.1 -p 9494 -U svc_pg3xp -d expressa_db
# Password: PgP4ss_s9494!
```

## 📋 Informasi Service

- **Image**: `jdanuc7/postgresql16-expressa:latest`
- **Container**: `postgresql16-expressa` (default)
- **Port**: 9494
- **Network**: `expressa-net`
- **Timezone**: Asia/Jakarta
- **Health Check**: ✅ Enabled

## 🔧 Konfigurasi

### Environment Variables

```bash
CONTAINER_NAME=postgresql16-expressa
DB_PORT=9494
POSTGRES_PASSWORD=PgP4ss_s9494!
POSTGRES_USER=svc_pg3xp
POSTGRES_DB=expressa_db
TZ=Asia/Jakarta
```

### Makefile Commands

```bash
make help      # Lihat semua perintah tersedia
make up        # Start PostgreSQL
make down      # Stop PostgreSQL
make restart   # Restart PostgreSQL
make logs      # Show logs
make status    # Show status
make shell     # Access container shell
make psql      # Connect to PostgreSQL
make backup    # Backup database
make clean     # Clean up
```

## 🔑 Database Credentials

### Default Access

- **Host**: 127.0.0.1 (external) / postgresql16-expressa (container)
- **Port**: 9494
- **Database**: expressa_db
- **Username**: svc_pg3xp
- **Password**: PgP4ss_s9494!

## 🛠️ Management Commands

```bash
# Service management
docker-compose up -d      # Start PostgreSQL
docker-compose down       # Stop PostgreSQL
docker-compose restart    # Restart PostgreSQL
docker-compose logs -f    # Show logs

# PostgreSQL access
docker-compose exec postgresql psql -U svc_pg3xp -d expressa_db

# Database backup
docker-compose exec postgresql pg_dump -U svc_pg3xp expressa_db > backup.sql

# Database restore
docker-compose exec -T postgresql psql -U svc_pg3xp -d expressa_db < backup.sql
```

## 🔍 Health Check & Monitoring

### Check PostgreSQL Status

```bash
# Container health
docker-compose ps

# PostgreSQL status
docker-compose exec postgresql pg_isready -U svc_pg3xp -d expressa_db

# Connection test
docker-compose exec postgresql psql -U svc_pg3xp -d expressa_db -c "SELECT version();"
```

### Performance Monitoring

```bash
# Show PostgreSQL version
docker-compose exec postgresql psql -U svc_pg3xp -d expressa_db -c "SELECT version();"

# Show databases
docker-compose exec postgresql psql -U svc_pg3xp -c "\l"

# Show active connections
docker-compose exec postgresql psql -U svc_pg3xp -d expressa_db -c "SELECT * FROM pg_stat_activity;"
```

## 💾 Data Persistence

### Volumes

- `postgresql_data:/var/lib/postgresql/data` - Database files

### Backup & Restore

```bash
# Database backup
docker-compose exec postgresql pg_dump -U svc_pg3xp expressa_db > backup.sql

# Restore backup
docker-compose exec -T postgresql psql -U svc_pg3xp -d expressa_db < backup.sql

# Full cluster backup
docker-compose exec postgresql pg_dumpall -U svc_pg3xp > full_backup.sql

# Custom format backup (recommended)
docker-compose exec postgresql pg_dump -U svc_pg3xp -Fc expressa_db > backup.dump

# Restore custom format
docker-compose exec -T postgresql pg_restore -U svc_pg3xp -d expressa_db backup.dump
```

## 🔗 Connection dari Aplikasi

### PHP Connection (dari container lain)

```php
$host = 'postgresql16-expressa';  // Container name
$port = 5432;
$database = 'expressa_db';
$username = 'svc_pg3xp';
$password = 'PgP4ss_s9494!';

$pdo = new PDO("pgsql:host=$host;port=$port;dbname=$database", $username, $password);
```

### External Connection (dari host)

```bash
# psql CLI
psql -h 127.0.0.1 -p 9494 -U svc_pg3xp -d expressa_db

# pgAdmin / DBeaver
Host: 127.0.0.1
Port: 9494
Database: expressa_db
Username: svc_pg3xp
Password: PgP4ss_s9494!
```

## 🔍 Troubleshooting

### PostgreSQL Won't Start

```bash
# Check logs
docker-compose logs -f postgresql

# Check disk space
df -h

# Remove and recreate container
docker-compose down
docker-compose up -d
```

### Connection Issues

```bash
# Check if container is running
docker-compose ps

# Check port binding
docker port postgresql16-expressa

# Test network connectivity
docker network inspect expressa-net

# Check PostgreSQL is accepting connections
docker-compose exec postgresql pg_isready -U svc_pg3xp
```

### Permission Issues

```bash
# Check PostgreSQL logs
docker-compose logs postgresql

# Reset permissions (if needed)
docker-compose down
docker volume rm postgresql16_postgresql_data
docker-compose up -d
```

### Performance Issues

```bash
# Check PostgreSQL configuration
docker-compose exec postgresql psql -U svc_pg3xp -d expressa_db -c "SHOW all;"

# Check active queries
docker-compose exec postgresql psql -U svc_pg3xp -d expressa_db -c "SELECT * FROM pg_stat_activity WHERE state = 'active';"

# Check database size
docker-compose exec postgresql psql -U svc_pg3xp -d expressa_db -c "SELECT pg_size_pretty(pg_database_size('expressa_db'));"
```

## 📁 File Structure

```
postgresql16/
├── Makefile            # Management commands
├── docker-compose.yml  # Docker compose config
└── init/              # Database initialization scripts (optional)
```

## 🔄 Development

### Database Initialization

1. Buat file `.sql` di folder `init/`
2. Mount folder ke `/docker-entrypoint-initdb.d/`
3. Script akan dijalankan saat container pertama kali dibuat

### Custom Configuration

1. Buat file `postgresql.conf` untuk custom config
2. Mount sebagai volume di docker-compose.yml
3. Restart container

### Extensions

```sql
-- Install extensions (jika tersedia)
CREATE EXTENSION IF NOT EXISTS "uuid-ossp";
CREATE EXTENSION IF NOT EXISTS "pgcrypto";
```

---

**PostgreSQL 16 Expressa** - Modern database server untuk development
