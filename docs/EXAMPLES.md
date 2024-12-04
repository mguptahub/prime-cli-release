# Prime CLI Examples

This document provides practical examples of common Prime CLI usage patterns.

## Instance Management

### Adding Instances

```bash
# Basic instance creation
prime-cli add prod

# Create instance with custom directory
prime-cli add staging --dir /opt/plane/staging

# Create instance with specific type
prime-cli add dev --type community

# Force create (overwrite existing)
prime-cli add prod --force
```

### Managing Instances

```bash
# List all instances
prime-cli list
prime-cli ls

# Switch between instances
prime-cli switch prod
prime-cli use staging

# Check instance status
prime-cli status

# Remove instance
prime-cli remove dev
prime-cli rm dev --force  # Force remove with data deletion
```

## Installation & Configuration

### Basic Installation

```bash
# Install with minimum configuration
prime-cli install --domain plane.company.com

# Install and start immediately
prime-cli install --domain plane.company.com --start

# Install specific version
prime-cli install --domain plane.company.com --release v1.2.3
```

### Advanced Installation

```bash
# Install with custom registry
prime-cli install --domain plane.company.com \
  --registry-url registry.example.com \
  --registry-username user \
  --registry-password pass \
  --registry-email user@example.com

# Install with volume mapping enabled
prime-cli install --domain plane.company.com \
  --map-volume-to-disk

# Install from GitHub repository
prime-cli install --domain plane.company.com \
  --github-repo makeplane/plane \
  --github-token ghp_token123

# Install with custom compose files and additional configurations
prime-cli install --domain plane.company.com \
  --compose-file custom-compose.yml \
  --compose-env custom.env \
  --additional-file nginx.conf \
  --additional-file custom-script.sh

# Combined installation with all features
prime-cli install --domain plane.company.com \
  --map-volume-to-disk \
  --github-repo makeplane/plane \
  --github-token ghp_token123 \
  --registry-url registry.example.com \
  --registry-username user \
  --registry-password pass \
  --scale web=2 --scale worker=3
```

### Environment Configuration

```bash
# Set multiple environment variables
prime-cli configure --env DB_HOST=localhost \
  --env DB_PORT=5432 \
  --env REDIS_URL=redis://localhost:6379

# Update domain
prime-cli configure --domain new-domain.com

# Scale services
prime-cli configure --scale web=2 --scale worker=3

# Combined configuration
prime-cli configure \
  --domain new-domain.com \
  --env DB_URL=new-url \
  --scale web=2
```

## Instance Operations

### Lifecycle Management

```bash
# Start instance
prime-cli start
prime-cli up

# Stop instance
prime-cli stop
prime-cli down

# Restart instance
prime-cli restart
prime-cli reboot

# Monitor instance
prime-cli monitor
prime-cli ps
```

### Status and Monitoring

```bash
# View detailed status of current instance
prime-cli status

# View status of specific instance
prime-cli status prod

# Monitor instance with continuous updates
prime-cli monitor

# View instance logs
prime-cli logs
```

### Updates and Maintenance

```bash
# Update CLI tool
prime-cli update

# Upgrade instance
prime-cli upgrade
prime-cli upgrade --start  # Upgrade and start

# Pull latest changes
prime-cli pull
prime-cli get
```

## Working with Multiple Instances

```bash
# Create development setup
prime-cli add dev --type community
prime-cli switch dev
prime-cli install --domain dev.local --start

# Create staging environment
prime-cli add staging
prime-cli switch staging
prime-cli install --domain staging.company.com \
  --env ENVIRONMENT=staging \
  --scale web=2

# Create production environment
prime-cli add prod
prime-cli switch prod
prime-cli install --domain plane.company.com \
  --env ENVIRONMENT=production \
  --scale web=3 \
  --scale worker=2
```

## Common Workflows

### Setting Up a New Instance

```bash
# 1. Create and switch to instance
prime-cli add prod
prime-cli switch prod

# 2. Install with configuration
prime-cli install --domain plane.company.com \
  --registry-url registry.company.com \
  --registry-username user \
  --registry-password pass \
  --env DB_URL=postgres://user:pass@host:5432/plane \
  --env REDIS_URL=redis://host:6379 \
  --scale web=2 \
  --scale worker=2

# 3. Start the instance
prime-cli start
```

### Upgrading an Instance

```bash
# 1. Pull latest changes
prime-cli pull

# 2. Stop the instance
prime-cli stop

# 3. Upgrade
prime-cli upgrade

# 4. Start the instance
prime-cli start

# Or, combine steps with
prime-cli upgrade --start
```

### Scaling for Production

```bash
# Scale web and worker processes
prime-cli configure \
  --scale web=3 \
  --scale worker=2 \
  --scale scheduler=2

# Update environment configuration
prime-cli configure \
  --env MAX_WORKERS=4 \
  --env CACHE_SIZE=2048 \
  --env LOG_LEVEL=info
```

### Development Workflow

```bash
# Create development instance
prime-cli add dev
prime-cli switch dev

# Install with development settings
prime-cli install --domain localhost \
  --env ENVIRONMENT=development \
  --env DEBUG=true \
  --env LOG_LEVEL=debug

# Start development server
prime-cli start

# Monitor logs and status
prime-cli monitor
```

## Tips and Tricks

### Using Environment Files

```bash
# Export current configuration
prime-cli configure list > config.txt

# View all configuration
prime-cli configure ls
```

### Troubleshooting

```bash
# Check instance status
prime-cli status

# Monitor service logs
prime-cli monitor

# Force cleanup and reinstall
prime-cli remove prod --force
prime-cli add prod
prime-cli install --domain plane.company.com --start
