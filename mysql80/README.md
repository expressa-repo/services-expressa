# MySQL 5.7 Expressa

Service MySQL 5.7 server untuk development dengan persistent storage dan health monitoring.

## 🚀 Quick Start

```bash
# 1. WAJIB: Pastikan network sudah dibuat
docker network create expressa-net

# 2. Start MySQL service
docker-compose up -d

# 3. Tunggu MySQL ready (30-60 detik)
docker-compose logs -f mysql

# 4. Test koneksi
mysql -h 127.0.0.1 -P 3306 -u root -p
# Password: MyR00t_5757!
```

## 📋 Informasi Service

- **Image**: `jdanuc7/mysql57-expressa:latest`
- **Container**: `mysql57-expressa`
- **Port**: 3306
- **Network**: `expressa-net`
- **Timezone**: Asia/Jakarta
- **Health Check**: ✅ Enabled

## 🔧 Konfigurasi (.env)

```bash
MYSQL_ROOT_PASSWORD=MyR00t_5757!
MYSQL_PORT=3306
TZ=Asia/Jakarta
```

## 🔑 Database Credentials

### Root Access

- **Host**: 127.0.0.1 (external) / mysql57-expressa (container)
- **Port**: 3306
- **Username**: root
- **Password**: MyR00t_5757!

### Application User (jika sudah dikonfigurasi)

- **Host**: 127.0.0.1 (external) / mysql57-expressa (container)
- **Port**: 3306
- **Database**: test_db
- **Username**: svc_my3xp
- **Password**: MyP4ss_9494!

## 🛠️ Management Commands

```bash
# Service management
docker-compose up -d      # Start MySQL
docker-compose down       # Stop MySQL
docker-compose restart    # Restart MySQL
docker-compose logs -f    # Show logs

# MySQL access
docker-compose exec mysql mysql -u root -p
# Password: MyR00t_5757!

# Database backup
docker-compose exec mysql mysqldump -u root -p --all-databases > backup.sql

# Database restore
docker-compose exec -T mysql mysql -u root -p < backup.sql
```

## 🔍 Health Check & Monitoring

### Check MySQL Status

```bash
# Container health
docker-compose ps

# MySQL process status
docker-compose exec mysql mysqladmin -u root -p status
docker-compose exec mysql mysqladmin -u root -p processlist

# Connection test
docker-compose exec mysql mysql -u root -p -e "SELECT 1"
```

### Performance Monitoring

```bash
# Show MySQL variables
docker-compose exec mysql mysql -u root -p -e "SHOW VARIABLES LIKE '%version%'"

# Show databases
docker-compose exec mysql mysql -u root -p -e "SHOW DATABASES"

# Show processes
docker-compose exec mysql mysql -u root -p -e "SHOW PROCESSLIST"
```

## 💾 Data Persistence

### Volumes

- `mysql_data:/var/lib/mysql` - Database files
- `mysql_logs:/var/log/mysql` - MySQL logs

### Backup & Restore

```bash
# Manual backup
docker-compose exec mysql mysqldump -u root -p database_name > backup.sql

# Restore backup
docker-compose exec -T mysql mysql -u root -p database_name < backup.sql

# Full backup
docker-compose exec mysql mysqldump -u root -p --all-databases > full_backup.sql
```

## 🔗 Connection dari Aplikasi

### PHP Connection (dari container lain)

```php
$host = 'mysql57-expressa';  // Container name
$port = 3306;
$database = 'test_db';
$username = 'root';
$password = 'MyR00t_5757!';

$pdo = new PDO("mysql:host=$host;port=$port;dbname=$database", $username, $password);
```

### External Connection (dari host)

```bash
# MySQL CLI
mysql -h 127.0.0.1 -P 3306 -u root -p

# MySQL Workbench / phpMyAdmin
Host: 127.0.0.1
Port: 3306
Username: root
Password: MyR00t_5757!
```

## 🔍 Troubleshooting

### MySQL Won't Start

```bash
# Check logs
docker-compose logs -f mysql

# Check disk space
df -h

# Remove and recreate container
docker-compose down
docker-compose up -d
```

### Connection Refused

```bash
# Check if container is running
docker-compose ps

# Check port binding
docker port mysql57-expressa

# Test network connectivity
docker network inspect expressa-net
```

### Performance Issues

```bash
# Check MySQL configuration
docker-compose exec mysql mysql -u root -p -e "SHOW VARIABLES LIKE '%buffer%'"

# Check slow queries
docker-compose exec mysql mysql -u root -p -e "SHOW VARIABLES LIKE '%slow%'"
```

### Data Recovery

```bash
# If data is corrupted, stop container
docker-compose down

# Backup current data volume
docker run --rm -v mysql57_mysql_data:/data -v $(pwd):/backup alpine tar czf /backup/mysql_backup.tar.gz /data

# Remove volume and recreate
docker volume rm mysql57_mysql_data
docker-compose up -d
```

## 📁 File Structure

```
mysql57/
├── .env                 # Environment configuration
└── docker-compose.yml   # Docker compose config
```

## 🔄 Development

### Custom Configuration

1. Buat file `my.cnf` untuk custom MySQL config
2. Mount sebagai volume di docker-compose.yml
3. Restart container

### Database Initialization

1. Buat folder `init/`
2. Tambahkan file `.sql` untuk initial data
3. Mount folder ke `/docker-entrypoint-initdb.d/`

---

**MySQL 5.7 Expressa** - Reliable database server untuk development
