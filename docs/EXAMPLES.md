# Prime CLI Examples

Comprehensive examples for using Prime CLI in various scenarios.

## Basic Usage Examples

### Local Development Install
```bash
# Create development instance
prime-cli add dev
prime-cli install \
  --domain localhost \
  --http-port 8080 \
  --https-port 8443 \
  --start

# Monitor services
prime-cli status -f
prime-cli logs api --tail 50 -f
```

### Production Deployment
```bash
# Create and configure production instance
prime-cli add prod
prime-cli install \
  --domain plane.company.com \
  --ssl \
  --env ENVIRONMENT=production \
  --start

# View status and logs
prime-cli status
prime-cli logs web
```

### Staging Environment
```bash
# Create staging instance with custom database
prime-cli add staging
prime-cli install \
  --domain staging.plane.company.com \
  --remote-db-url "postgres://user:pass@host:5432/plane_staging" \
  --env ENVIRONMENT=staging
```

## Advanced Configuration Examples

### Complete Production Install with Remote Services
```bash
prime-cli add prod
prime-cli install \
  --domain plane.company.com \
  --ssl \
  --remote-db-url "postgres://user:pass@host:5432/plane" \
  --remote-redis-url "redis://user:pass@host:6379" \
  --s3-bucket "plane-uploads" \
  --s3-region "us-east-1" \
  --s3-access-key-id "your-access-key" \
  --s3-secret-access-key "your-secret-key" \
  --s3-endpoint "https://s3.amazonaws.com" \
  --env SMTP_HOST=smtp.example.com \
  --env SMTP_PORT=587 \
  --env SMTP_USER=user@example.com \
  --env SMTP_PASS=password \
  --env COMPANY_NAME="ACME Corp" \
  --start
```

### Custom Repository and Version
```bash
# Use private repository
prime-cli install \
  --domain plane.example.com \
  --github-repo organization/private-repo \
  --github-token ghp_yourtokenhere \
  --compose-file custom-compose.yml \
  --env-file custom.env

# Install specific version
prime-cli install \
  --domain plane.example.com \
  --release v1.2.3
```

### Multiple Instances
```bash
# Create instances
prime-cli add prod
prime-cli add staging
prime-cli add dev

# List and switch
prime-cli list
prime-cli switch staging

# Remove old instance
prime-cli remove old-instance --force
```

## Maintenance Examples

### Backup and Restore
```bash
# Stop instance before backup
prime-cli stop

# Backup data directories
tar -czf backup.tar.gz ~/.prime/myapp/pgdata ~/.prime/myapp/minio

# Restore from backup
prime-cli stop
rm -rf ~/.prime/myapp/pgdata ~/.prime/myapp/minio
tar -xzf backup.tar.gz -C /
prime-cli start
```

### Upgrades and Updates
```bash
# Update CLI
prime-cli update-cli

# Upgrade instance
prime-cli upgrade --start

# Repair broken installation
prime-cli repair
```

### Monitoring and Debugging
```bash
# Live status monitoring
prime-cli status -f

# Follow multiple service logs
prime-cli logs api -f
prime-cli logs web -f
prime-cli logs worker -f

# Debug mode
prime-cli --debug status
prime-cli --debug install --domain example.com
```

## Environment-Specific Examples

### Development Environment
```bash
prime-cli add dev
prime-cli install \
  --domain localhost \
  --http-port 8080 \
  --env ENVIRONMENT=development \
  --env DEBUG=true \
  --env LOG_LEVEL=debug
```

### Testing Environment
```bash
prime-cli add test
prime-cli install \
  --domain test.plane.local \
  --env ENVIRONMENT=testing \
  --env TEST_MODE=true \
  --remote-db-url "postgres://test:test@localhost:5432/plane_test"
```

### Production Environment
```bash
prime-cli add prod
prime-cli install \
  --domain plane.company.com \
  --ssl \
  --env ENVIRONMENT=production \
  --env LOG_LEVEL=info \
  --env RATE_LIMIT=true \
  --env RATE_LIMIT_REQUESTS=100 \
  --env RATE_LIMIT_PERIOD=60
```

## Docker Compose Service Examples

### Basic Service Status
```bash
# View all services
prime-cli status

# Monitor specific service
prime-cli logs web --tail 100 -f
```

### Service Management
```bash
# Start all services
prime-cli start

# Stop specific service
docker compose stop web

# Restart services
prime-cli restart
```

## Troubleshooting Examples

### Debug Mode
```bash
# Enable debug logging
prime-cli --debug install --domain example.com
prime-cli --debug status
prime-cli --debug logs api
```

### Repair and Recovery
```bash
# Repair broken installation
prime-cli repair

# Force remove problematic instance
prime-cli remove broken --force

# Clean reinstall
prime-cli uninstall --force
prime-cli install --domain example.com --start
```
