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

## Docker Setup

To set up Docker for optimal performance, run:
```bash
prime-cli docker-setup
```

## Setting Up Community Edition

### Docker Based Setup

> Optional: To set up Docker for optimal performance, run:
> ```bash
> prime-cli docker-setup
> ```

To set up a community edition instance, run:
```bash
prime-cli add <instance-name> --type community
```

To install the latest version of Plane, run:
```bash
prime-cli install --domain plane.company.com --version v0.24.0
```

This will:
- Download and install the latest version of Plane
- Configure the instance with the provided domain and version
- Set up the instance for community user access

### Kubernetes Based Setup

To set up a community edition instance, run:
```bash
prime-cli add <instance-name> --type community --kubernetes
```

To install the latest version of Plane, run:
```bash
prime-cli install \
    --namespace plane-ns \
    --release-name myplane-ce \
    --set planeVersion=v0.24.1 \
    --set ingress.appHost="myplane.example.com" \
    --set ingress.ingressClass=nginx \
    --set postgres.storageClass=standard-rwo \
    --set redis.storageClass=standard-rwo \
    --set minio.storageClass=standard-rwo \
    --set rabbitmq.storageClass=standard-rwo
```

This will:

- Create a new Kubernetes namespace for Plane
- Install the specified version of Plane 
- Configure the instance with the provided `--set` options

## Usage

To list available commands, run:
```bash
prime-cli --help
```

## Setting Up Commercial Edition

This is Work-In-Progress and will be available in a future release.

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
