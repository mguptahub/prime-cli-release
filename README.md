# Prime CLI

A command-line interface tool for managing Plane instances.

## Features

- Easy installation and configuration of Plane instances
- Multiple instance management
- Docker-based deployment
- Automatic updates and maintenance
- Instance monitoring and logging

## Installation

```bash
# Download and install the latest release
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

### Installation & Configuration
- `install` - Install a new Plane instance
- `configure` (alias: `config`) - Configure instance settings
- `upgrade` - Upgrade to latest version
- `update-cli` - Update the CLI tool

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
