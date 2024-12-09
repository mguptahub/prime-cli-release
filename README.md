# Prime CLI

A command-line interface tool for managing Plane instances.

## Features

- Easy installation and configuration of Plane instances
- Multiple instance management with status monitoring
- Docker-based deployment with custom registry support
- Volume mapping for persistent data storage
- Support for custom compose files and environment configurations
- GitHub repository integration
- Instance health monitoring and detailed status reporting
- Automatic updates and maintenance

## Installation

```bash
curl -sSL https://github.com/mguptahub/prime-cli-release/releases/latest/download/install.sh | bash
```

## Quick Start

1. Create a new instance:
```bash
prime-cli add myinstance
```

2. Install Plane with your domain:
```bash
prime-cli install --domain your-domain.com
```

3. Start the instance:
```bash
prime-cli start
```

## Available Commands

### Instance Management
- `add` - Create a new instance
- `list` (alias: `ls`) - List all instances
- `switch` - Switch between instances
- `status` - Show instance status
- `remove` (alias: `rm`) - Remove an instance

### Docker Setup
- `docker-setup` - Ensure Docker is properly installed and configured for Plane
```bash
prime-cli docker-setup
```
This command will:
- Check if Docker is installed and running correctly
- For Linux systems, attempt automatic installation if Docker is not present
- Verify Docker daemon is responding after installation
- Configure Docker for optimal use with Plane

### Installation & Configuration
- `install` - Install a new Plane instance
- `configure` (alias: `config`) - Configure instance settings
- `upgrade` - Upgrade to latest version

### System Management
- `update-cli` (alias: `update`) - Update the Prime CLI tool to the latest version
  - Requires root/administrator privileges depending on installation directory
  - Preserves all instance configurations and settings
  - Downloads and installs the latest version from GitHub

### Operations
- `start` (alias: `up`) - Start instance
- `stop` (alias: `down`) - Stop instance
- `restart` (alias: `reboot`) - Restart instance
- `pull` (alias: `get`) - Pull latest Docker images
- `monitor` (alias: `ps`) - Monitor instance status

### Maintenance
- `repair` - Repair installation
- `backup` - Backup instance data
- `restore` - Restore instance data

For detailed command documentation, see [COMMANDS.md](docs/COMMANDS.md)

## Configuration

For detailed configuration options, see [CONFIG.md](docs/CONFIG.md)

## Examples

For usage examples, see [EXAMPLES.md](docs/EXAMPLES.md)

## Support

- GitHub Issues: [Report a bug](https://github.com/mguptahub/prime-cli-release/issues)
- Documentation: [View full documentation](https://docs.plane.so)

## License

This project is licensed under the [MIT License](LICENSE)
