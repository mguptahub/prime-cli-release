# Prime CLI

Prime CLI is a command-line tool for managing Docker-based Plane application instances. It simplifies the deployment, maintenance, and updates of Plane across multiple environments.

## Features

- Multi-instance management for running multiple Plane deployments
- Automatic Docker installation and configuration
- Simple domain and SSL/TLS setup
- Remote database, Redis, and S3 storage integration
- Version management and automatic updates
- Comprehensive logging and monitoring
- Environment-specific configurations

## Quick Start

### Installation

Download the latest release for your platform:

```bash
# Linux (x64)
curl -L https://github.com/mguptahub/prime-cli-release/releases/latest/download/prime-cli-linux-amd64 -o prime-cli
chmod +x prime-cli
sudo mv prime-cli /usr/local/bin/

# macOS (x64)
curl -L https://github.com/mguptahub/prime-cli-release/releases/latest/download/prime-cli-darwin-amd64 -o prime-cli
chmod +x prime-cli
xattr -d com.apple.quarantine prime-cli
sudo mv prime-cli /usr/local/bin/
```

### Basic Usage

1. Create a new instance:
```bash
prime-cli add myapp
```

2. Set up Plane with your domain:
```bash
prime-cli install --domain plane.example.com --start
```

## Available Commands

### Instance Management
- `prime-cli add <name>` - Create new instance (aliases: create, new)
- `prime-cli list` - List all instances (alias: ls)
- `prime-cli switch <name>` - Switch between instances (alias: use)
- `prime-cli remove <name>` - Remove instance (aliases: rm, delete)

### Installation and Configuration
- `prime-cli install` - Configure instance with domain and services
  ```bash
  # Basic installation
  prime-cli install --domain plane.example.com
  
  # With SSL and custom ports
  prime-cli install --domain plane.example.com --ssl --http-port 80 --https-port 443
  
  # With remote services
  prime-cli install --domain plane.example.com \
    --remote-db-url "postgres://user:pass@host:5432/plane" \
    --remote-redis-url "redis://host:6379"
  ```

- `prime-cli configure` - Update instance configuration (alias: config)
  ```bash
  # Update domain and SSL settings
  prime-cli configure --domain new.example.com --ssl
  
  # Update environment variables
  prime-cli configure --env KEY1=value1 --env KEY2=value2
  ```

### Operation Commands
- `prime-cli start` - Start instance (alias: up)
- `prime-cli stop` - Stop instance (alias: down)
- `prime-cli restart` - Restart instance (alias: reboot)
- `prime-cli status` - View instance status (aliases: ps, monitor)
- `prime-cli logs <service>` - View service logs (alias: log)
  ```bash
  # Follow logs with tail
  prime-cli logs api --follow --tail 100
  ```

### Maintenance Commands
- `prime-cli pull` - Pull latest Docker images (alias: get)
- `prime-cli upgrade` - Upgrade to latest version
- `prime-cli uninstall` - Remove instance setup (alias: un)
- `prime-cli update` - Update Prime CLI itself

### Work in Progress Commands
The following commands are planned but not yet implemented:
- `prime-cli backup` - Backup Plane data (WIP)
- `prime-cli restore` - Restore Plane data (WIP)
- `prime-cli repair` - Repair broken installations (WIP)

## Directory Structure

### Installation Directory
```
~/.prime/myapp/
├── docker-compose.yml  # Docker compose configuration
├── plane.env          # Environment variables
├── .....
└── .....
```

### Configuration
```
~/.prime-cli/config   # CLI configuration file
```

## Documentation

- [Command Reference](docs/COMMANDS.md) - Detailed command documentation
- [Examples](docs/EXAMPLES.md) - Common use cases and examples
- [Configuration Guide](docs/CONFIG.md) - Configuration options and best practices

## Support

- GitHub Issues: Report bugs and feature requests
- Documentation: [Full documentation](https://docs.plane.so)
- Community: [Discord](https://discord.gg/A92xrEGCge)
