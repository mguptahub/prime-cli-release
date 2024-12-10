# Prime CLI

```
      /////////
      /////////   Plane
/////     /////   Project management software
/////     /////   www.plane.so
     /////     
     /////     
```

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

To install Prime CLI, run:

```bash
curl -sSL https://github.com/mguptahub/prime-cli-release/releases/latest/download/install.sh | bash
```

This will:
- Download the latest version of Prime CLI
- Install it to `~/.local/bin/prime-cli`
- Make it available system-wide for current user
- Set appropriate permissions

Verify the installation:
```bash
prime-cli --version
```

## Documentation

For detailed documentation on all commands, sub-commands, and their options, please refer to:
- [Detailed Command Reference](docs/README-DETAILED.md) - Complete documentation of all commands and options
- [Configuration Guide](docs/CONFIG.md) - Detailed configuration options and examples
- [Usage Examples](docs/EXAMPLES.md) - Common usage patterns and workflows

## Support

- GitHub Issues: [Report a bug](https://github.com/mguptahub/prime-cli-release/issues)
- Documentation: [View full documentation](https://docs.plane.so)

## License

This project is licensed under the [MIT License](LICENSE)
