# Prime CLI Examples

This document provides practical examples of common Prime CLI workflows and usage patterns.

## Getting Started

### Check Installation
```bash
# Verify CLI installation
prime-cli --version

# Optional: Set up Docker if needed
prime-cli docker-setup

# Optional: Set up Helm for Kubernetes deployments
prime-cli helm-setup
```

## Docker-based Deployment

### Basic Setup
```bash
# Create new instance
prime-cli add my-plane --type community

# Install with required settings
prime-cli install \
  --domain plane.company.com \
  --version v0.24.0 \
  --start

# Check status
prime-cli status
```

### Advanced Installation
```bash
# Create instance with custom directory
prime-cli add my-plane \
  --type community \
  --dir /opt/plane/instances/prod

# Install with advanced options
prime-cli install \
  --domain plane.company.com \
  --version v0.24.0 \
  --map-volume-to-disk \
  --scale web=2 \
  --scale worker=3 \
  --env DB_HOST=localhost \
  --env REDIS_HOST=localhost
```

### Registry Configuration
```bash
# Install with private registry
prime-cli install \
  --domain plane.company.com \
  --registry-url registry.company.com \
  --registry-username user \
  --registry-password pass \
  --registry-email user@company.com
```

## Kubernetes-based Deployment

### Basic Setup
```bash
# Create Kubernetes instance
prime-cli add my-plane \
  --type community \
  --kubernetes \
  --kubecontext my-cluster

# Install with Helm
prime-cli install \
  --namespace plane-system \
  --release-name plane \
  --set ingress.appHost=plane.company.com \
  --set ingress.ingressClass=nginx \
  --set postgres.storageClass=standard-rwo
```

### Advanced Kubernetes Configuration
```bash
# Install with custom values
prime-cli install \
  --namespace plane-system \
  --release-name plane \
  --values custom-values.yaml \
  --set web.replicas=3 \
  --set api.replicas=2 \
  --wait-for-services
```

## Instance Management

### Working with Multiple Instances
```bash
# List instances
prime-cli list

# Switch between instances
prime-cli switch prod
prime-cli switch staging

# Check instance status
prime-cli status
prime-cli status prod
```

### Instance Operations
```bash
# Start instance
prime-cli start

# Monitor services
prime-cli monitor

# Stop instance
prime-cli stop

# Restart instance
prime-cli restart
```

## Configuration Management

### Basic Configuration
```bash
# View current configuration
prime-cli configure list

# Update domain
prime-cli configure set --domain new.company.com

# Set environment variables
prime-cli configure set \
  --env DB_HOST=new-db.company.com \
  --env REDIS_URL=redis://new-redis:6379

# Scale services
prime-cli configure set \
  --scale web=3 \
  --scale worker=2
```

### Advanced Configuration
```bash
# View compose/values file
prime-cli configure view
prime-cli configure view --out config.yaml

# Update and restart
prime-cli configure set \
  --domain new.company.com \
  --env DB_URL=new-url \
  --scale web=2 \
  --restart
```

## Data Management

### Backup and Restore
```bash
# Create backup
prime-cli backup

# List available backups
prime-cli backup list

# Validate backup
prime-cli backup validate <backup-path>

# Restore from backup
prime-cli restore <backup-path>
```

## Maintenance Operations

### Updates and Upgrades
```bash
# Update CLI
prime-cli update-cli

# Pull latest images
prime-cli pull

# Upgrade instance
prime-cli upgrade --start

# Repair instance
prime-cli repair
```

### Environment Updates
```bash
# Update database configuration
prime-cli configure set \
  --env DB_HOST=new-host \
  --env DB_PORT=5432 \
  --env DB_NAME=plane \
  --restart

# Update email settings
prime-cli configure set \
  --env SMTP_HOST=smtp.company.com \
  --env SMTP_PORT=587 \
  --env SMTP_USER=user \
  --env SMTP_PASS=pass \
  --restart
```

## Best Practice Examples

### Development Setup
```bash
# Create development instance
prime-cli add dev --type community
prime-cli switch dev
prime-cli install \
  --domain localhost \
  --version v0.24.0 \
  --env MODE=development \
  --env DEBUG=true \
  --map-volume-to-disk

# Start and monitor
prime-cli start
prime-cli monitor
```

### Production Setup
```bash
# Create production instance
prime-cli add prod --type community
prime-cli switch prod
prime-cli install \
  --domain plane.company.com \
  --version v0.24.0 \
  --map-volume-to-disk \
  --scale web=3 \
  --scale worker=2 \
  --env MODE=production \
  --env REDIS_URL=redis://prod-redis:6379

# Backup before changes
prime-cli backup

# Apply changes
prime-cli configure set \
  --scale web=4 \
  --restart
```

### Multi-Environment Management
```bash
# Create environments
prime-cli add dev --type community
prime-cli add staging --type community
prime-cli add prod --type community

# Configure each environment
for env in dev staging prod; do
  prime-cli switch $env
  prime-cli install \
    --domain $env.plane.company.com \
    --version v0.24.0 \
    --env ENV=$env
done

# Check status of all instances
for env in dev staging prod; do
  echo "Status for $env:"
  prime-cli status $env
done
```

## Custom Registry Setup

### Private Registry Example
```bash
# Create instance
prime-cli add custom-plane --type community

# Install with registry
prime-cli install \
  --domain plane.company.com \
  --registry-url registry.company.com \
  --registry-username user \
  --registry-password pass \
  --registry-email user@company.com \
  --version v0.24.0
```

## Troubleshooting Examples

### Service Issues
```bash
# Check service status
prime-cli status

# View detailed logs
prime-cli monitor

# Restart specific service
prime-cli configure set \
  --scale web=0 \
  --restart
prime-cli configure set \
  --scale web=2 \
  --restart
```

### Recovery Operations
```bash
# Backup before changes
prime-cli backup

# Attempt repair
prime-cli repair

# Restore if needed
prime-cli restore <backup-path>
```