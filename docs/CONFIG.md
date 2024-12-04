# Prime CLI Configuration Guide

This document outlines the configuration options and structure for Prime CLI.

## Configuration Files

### CLI Configuration
Location: `~/.prime-cli/config`

The main configuration file stores instance settings in JSON format:

```json
{
  "current_instance": "prod",
  "instances": {
    "prod": {
      "name": "prod",
      "install_dir": "~/.prime/prod",
      "settings": {
        "domain": "plane.company.com",
        "app_version": "v1.2.3",
        "compose_file": "docker-compose.yml",
        "compose_env": "plane.env",
        "registry": {
          "url": "registry.example.com",
          "username": "user",
          "password": "pass",
          "email": "user@example.com"
        },
        "service_scales": {
          "web": 2,
          "api": 3,
          "worker": 2
        },
        "envs": {
          "APP_DOMAIN": "plane.company.com",
          "DOMAIN_NAME": "plane.company.com",
          "WEB_URL": "https://plane.company.com",
          "CORS_ALLOWED_ORIGINS": "http://plane.company.com:80,https://plane.company.com:443"
        }
      },
      "created_at": "2024-01-01T00:00:00Z",
      "updated_at": "2024-01-01T00:00:00Z"
    }
  }
}
```

### Environment File
Location: `~/.prime/<instance>/plane.env`

Instance-specific environment variables:

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

# Database Configuration
DATABASE_URL=postgres://user:pass@host:5432/plane

# Redis Configuration
REDIS_URL=redis://host:6379

# Storage Configuration
AWS_REGION=us-east-1
AWS_ACCESS_KEY_ID=access-key
AWS_SECRET_ACCESS_KEY=secret-key
AWS_S3_BUCKET_NAME=plane-uploads
AWS_S3_ENDPOINT_URL=https://s3.amazonaws.com
```

## Directory Structure

```
~/.prime/
├── instance-1/
│   ├── docker-compose.yml     # Docker services configuration
│   ├── plane.env             # Environment variables
│   ├── .run.yml             # Generated runtime compose file
│   ├── pgdata/              # PostgreSQL data
│   ├── minio/               # MinIO/S3 data
│   ├── redis/              # Redis data
│   └── logs/               # Application logs
└── instance-2/
    └── ...
```

## Configuration Commands

### View Configuration
```bash
prime-cli configure list  # List all configuration values
prime-cli configure ls    # Shorthand for list
```

### Update Configuration
```bash
# Update domain
prime-cli configure --domain new-domain.com

# Set environment variables
prime-cli configure --env KEY1=VALUE1 --env KEY2=VALUE2

# Scale services
prime-cli configure --scale web=2 --scale worker=3

# Multiple updates at once
prime-cli configure --domain new-domain.com --env DB_URL=new-url --scale web=2
```

## Best Practices

1. **Environment Variables**
   - Use environment variables for sensitive data
   - Keep secrets in the environment file
   - Use appropriate file permissions

2. **Service Scaling**
   - Scale services based on load requirements
   - Consider resource constraints
   - Monitor performance after scaling

3. **Registry Configuration**
   - Use secure registry URLs
   - Store registry credentials securely
   - Update credentials periodically

4. **SSL/TLS**
   - Always use HTTPS in production
   - Configure proper DNS records
   - Use valid SSL certificates

5. **Backup and Recovery**
   - Regularly backup data directories
   - Test restore procedures
   - Document recovery steps

## Troubleshooting

1. **Configuration Issues**
   - Check environment file syntax
   - Verify file permissions
   - Validate JSON structure

2. **Service Scaling**
   - Verify resource availability
   - Check service dependencies
   - Monitor container health

3. **Registry Access**
   - Verify registry credentials
   - Check network connectivity
   - Validate image paths

4. **SSL/TLS**
   - Verify certificate paths
   - Check certificate validity
   - Confirm DNS records