# Prime CLI Configuration Guide

Comprehensive documentation of Prime CLI's configuration options, structure, and best practices.

## Configuration Files

### CLI Configuration
```
~/.prime-cli/config
```
This is the main configuration file that stores instance settings in JSON format. Example structure:

```json
{
  "current_instance": "prod",
  "instances": {
    "prod": {
      "name": "prod",
      "app_version": "v1.2.3",
      "os": "linux",
      "cpu_arch": "amd64",
      "domain": "plane.company.com",
      "install_date": "2024-11-21T10:00:00Z",
      "created_at": "2024-11-21T10:00:00Z",
      "last_update": "2024-11-21T10:00:00Z",
      "install_dir": "~/.prime/prod",
      "github_repo": "makeplane/plane-releases",
      "compose_file": "docker-compose.yml",
      "env_file": "plane.env",
      "instance_signature": "unique-instance-identifier",
      "env": {
        "http_port": 80,
        "https_port": 443,
        "enable_ssl": "true",
        "db_url": "postgres://user:pass@host:5432/plane",
        "redis_url": "redis://host:6379",
        "s3_bucket": "plane-uploads",
        "s3_region": "us-east-1",
        "s3_access_key": "access-key",
        "s3_secret_key": "secret-key",
        "s3_endpoint": "https://s3.amazonaws.com"
      }
    }
  }
}
```

### Environment File
Located at `~/.prime/<instance>/plane.env`, this file contains instance-specific environment variables:

```bash
# Core Configuration
APP_DOMAIN=plane.company.com
DOMAIN_NAME=plane.company.com
INSTALL_DIR=~/.prime/prod
WEB_URL=https://plane.company.com
SITE_ADDRESS=https://plane.company.com
CORS_ALLOWED_ORIGINS=http://plane.company.com:80,https://plane.company.com:443
APP_PROTOCOL=https

# Server Configuration
LISTEN_HTTP_PORT=80
LISTEN_HTTPS_PORT=443
APP_RELEASE_VERSION=v1.2.3
MACHINE_SIGNATURE=unique-instance-identifier
DEPLOY_PLATFORM=docker-compose

# Database Configuration
DATABASE_URL=postgres://user:pass@host:5432/plane

# Redis Configuration
REDIS_URL=redis://host:6379

# S3 Storage Configuration
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=access-key
AWS_SECRET_ACCESS_KEY=secret-key
AWS_S3_BUCKET_NAME=plane-uploads
AWS_S3_ENDPOINT_URL=https://s3.amazonaws.com
```

## Directory Structure

### Installation Directory
Default location: `~/.prime/<instance-name>/`

```
~/.prime/instance-name/
├── docker-compose.yml     # Docker services configuration
├── plane.env             # Environment variables
├── .run.yml             # Generated runtime compose file
├── pgdata/              # PostgreSQL data directory
│   └── ...
├── minio/               # MinIO/S3 data directory
│   └── ...
├── redis/              # Redis data directory
│   └── ...
└── logs/               # Application logs
    ├── api/
    ├── web/
    └── worker/
```

## Configuration Options

### Domain Configuration

```bash
# Basic install
prime-cli install --domain plane.example.com

# With SSL
prime-cli install --domain plane.example.com --ssl

# Custom Ports
prime-cli install \
  --domain plane.example.com \
  --http-port 8080 \
  --https-port 8443
```

### Database Configuration

#### Local Database
```bash
# Uses default local PostgreSQL container
prime-cli install --domain plane.example.com
```

#### Remote Database
```bash
# Using external PostgreSQL
prime-cli install \
  --domain plane.example.com \
  --remote-db-url "postgres://user:pass@host:5432/plane"
```

### Redis Configuration

#### Local Redis
```bash
# Uses default local Redis container
prime-cli install --domain plane.example.com
```

#### Remote Redis
```bash
# Using external Redis
prime-cli install \
  --domain plane.example.com \
  --remote-redis-url "redis://user:pass@host:6379"
```

### Storage Configuration

#### Local Storage
```bash
# Uses local MinIO container
prime-cli install --domain plane.example.com
```

#### S3 Storage
```bash
# Using AWS S3
prime-cli install \
  --domain plane.example.com \
  --s3-bucket "plane-uploads" \
  --s3-region "us-east-1" \
  --s3-access-key-id "access-key" \
  --s3-secret-access-key "secret-key" \
  --s3-endpoint "https://s3.amazonaws.com"

# Using MinIO
prime-cli install \
  --domain plane.example.com \
  --s3-bucket "plane-uploads" \
  --s3-region "us-east-1" \
  --s3-access-key-id "access-key" \
  --s3-secret-access-key "secret-key" \
  --s3-endpoint "http://minio.example.com:9000"
```

### Environment Variables

```bash
# Setting individual variables
prime-cli install \
  --domain plane.example.com \
  --env KEY1=value1 \
  --env KEY2=value2

# Common configurations
prime-cli install \
  --domain plane.example.com \
  --env SMTP_HOST=smtp.example.com \
  --env SMTP_PORT=587 \
  --env SMTP_USER=user@example.com \
  --env SMTP_PASS=password \
  --env COMPANY_NAME="ACME Corp" \
  --env LOG_LEVEL=info
```

## Best Practices

### Security

1. **SSL Configuration**
   - Always use SSL in production
   - Configure proper DNS records
   - Use valid SSL certificates
   ```bash
   prime-cli install --domain plane.company.com --ssl
   ```

2. **Database Security**
   - Use strong passwords
   - Restrict database access
   - Enable SSL for database connections
   ```bash
   prime-cli install \
     --domain plane.company.com \
     --remote-db-url "postgres://user:pass@host:5432/plane?sslmode=verify-full"
   ```

3. **S3 Security**
   - Use IAM roles when possible
   - Restrict bucket permissions
   - Enable bucket encryption
   ```bash
   prime-cli install \
     --domain plane.company.com \
     --s3-bucket "plane-uploads" \
     --s3-region "us-east-1" \
     --s3-access-key-id "access-key" \
     --s3-secret-access-key "secret-key" \
     --env S3_FORCE_PATH_STYLE=true \
     --env S3_USE_SSL=true
   ```

### Performance

1. **Resource Allocation**
   - Monitor resource usage
   - Scale services appropriately
   - Use appropriate instance sizes

2. **Caching**
   - Use Redis for caching
   - Configure appropriate cache sizes
   - Monitor cache hit rates

3. **Storage**
   - Regular cleanup of temporary files
   - Monitor disk usage
   - Configure appropriate backup strategies

### Maintenance

1. **Backup Strategy**
   ```bash
   # Stop instance
   prime-cli stop

   # Backup data
   tar -czf backup.tar.gz ~/.prime/prod/pgdata ~/.prime/prod/minio

   # Start instance
   prime-cli start
   ```

2. **Update Strategy**
   ```bash
   # Update CLI
   prime-cli update-cli

   # Upgrade instance
   prime-cli upgrade --start
   ```

3. **Monitoring**
   ```bash
   # Monitor status
   prime-cli status -f

   # Check logs
   prime-cli logs api --tail 1000
   ```

## Troubleshooting

### Common Issues

1. **Database Connection Issues**
   ```bash
   # Check database URL format
   prime-cli --debug logs api
   
   # Verify connection
   psql "postgres://user:pass@host:5432/plane"
   ```

2. **Redis Connection Issues**
   ```bash
   # Check Redis URL format
   prime-cli --debug logs api
   
   # Verify connection
   redis-cli -u redis://user:pass@host:6379
   ```

3. **S3 Storage Issues**
   ```bash
   # Verify S3 settings
   prime-cli --debug logs api
   
   # Check bucket access
   aws s3 ls s3://plane-uploads
   ```

### Debug Mode
Enable debug logging for troubleshooting:
```bash
prime-cli --debug install --domain example.com
prime-cli --debug status
prime-cli --debug logs api
```

### Recovery
```bash
# Repair installation
prime-cli repair

# Reinstall if needed
prime-cli uninstall --force
prime-cli install --domain example.com --start
```

## Environment-Specific Configurations

### Development
```bash
prime-cli install \
  --domain localhost \
  --http-port 8080 \
  --env ENVIRONMENT=development \
  --env DEBUG=true \
  --env LOG_LEVEL=debug
```

### Staging
```bash
prime-cli install \
  --domain staging.plane.company.com \
  --ssl \
  --env ENVIRONMENT=staging \
  --env LOG_LEVEL=info
```

### Production
```bash
prime-cli install \
  --domain plane.company.com \
  --ssl \
  --env ENVIRONMENT=production \
  --env LOG_LEVEL=warn \
  --env RATE_LIMIT=true
```

This configuration guide provides a comprehensive overview of Prime CLI's configuration options, best practices, and troubleshooting steps. Would you like me to expand on any particular section or add additional examples?