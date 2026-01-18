# Quick Start Guide

## Starting the Infrastructure

```bash
# Start all services
docker compose up -d

# Check services status
docker compose ps

# View logs
docker compose logs -f nginx
docker compose logs -f sftp
```

## Testing the Setup

### 1. Test HTTP to HTTPS Redirect (301)
```bash
curl -I http://localhost:8080/
# Should return: HTTP/1.1 301 Moved Permanently
```

### 2. Test HTTPS Main Site
```bash
curl -I -k https://localhost:8443/
# Should return: HTTP/1.1 200 OK
```

### 3. Test Clock App (/reloj)
```bash
curl -I -k https://localhost:8443/reloj/
# Should return: HTTP/1.1 200 OK
```

### 4. Test Admin Area (Protected)
```bash
# Without credentials (should fail)
curl -I -k https://localhost:8443/admin/
# Should return: HTTP/1.1 401 Unauthorized

# With credentials (should succeed)
curl -I -k -u admin:'Admin1234!' https://localhost:8443/admin/
# Should return: HTTP/1.1 200 OK
```

### 5. Test Security Headers
```bash
curl -k -I https://localhost:8443/ | grep -E 'X-Content-Type-Options|X-Frame-Options|Content-Security-Policy'
```

## SFTP Access

### Connection Details
- **Host**: localhost
- **Port**: 2222
- **Username**: sftpuser
- **Password**: sftppass
- **Upload Directory**: /home/sftpuser/upload (mapped to ./webdata)

### Using Command Line
```bash
sftp -P 2222 sftpuser@localhost
# Password: sftppass
```

### Using FileZilla
1. Host: `sftp://localhost`
2. Port: `2222`
3. Username: `sftpuser`
4. Password: `sftppass`

## Nginx Configuration Validation

```bash
# Test configuration
docker compose exec nginx nginx -t

# Reload configuration after changes
docker compose exec nginx nginx -s reload
```

## Stopping the Infrastructure

```bash
docker compose down
```

## Directory Structure

```
.
├── docker-compose.yml       # Docker orchestration
├── default.conf            # Nginx configuration
├── nginx-selfsigned.crt    # SSL certificate
├── nginx-selfsigned.key    # SSL private key (gitignored)
├── .htpasswd              # Basic auth credentials (gitignored)
├── webdata/               # Web content (shared via volume)
│   ├── index.html         # Main site
│   ├── reloj/            
│   │   └── index.html    # Clock app
│   └── admin/
│       └── index.html    # Protected admin area
└── evidencias/           # Evidence/screenshots directory
```

## URLs

- Main site: https://localhost:8443/
- Clock app: https://localhost:8443/reloj/
- Admin area: https://localhost:8443/admin/ (requires auth)

## Credentials

### Admin Area
- Username: `admin`
- Password: `Admin1234!`

### SFTP
- Username: `sftpuser`
- Password: `sftppass`
