# Prime CLI

```
      /////////
      /////////   Plane
/////     /////   Project management software
/////     /////   www.plane.so
     /////     
     /////     
```

Prime CLI is the official command-line interface tool for managing Plane instances. Whether you're running Plane on Docker or Kubernetes, Prime CLI simplifies deployment, maintenance, and operations.

## Overview

### Purpose
- Deploy and manage Plane instances with simple commands
- Handle multiple instances on the same machine
- Automate deployment and configuration
- Monitor instance health and status
- Perform backups and restores
- Manage updates and maintenance

### Supported Platforms
- **Operating Systems**:
  - Linux (amd64, arm64)
  - macOS (amd64, arm64)
  
- **Deployment Options**:
  - Docker-based deployment (default)
  - Kubernetes deployment using Helm charts

### Key Features
- Multi-instance management
- Docker and Kubernetes support
- Volume management for persistent data
- Custom domain configuration
- Service scaling
- Health monitoring
- Backup and restore capabilities
- Instance configuration management
- Registry support for private deployments

## Quick Start

### Installation

```bash
curl -sSL https://mguptahub.github.io/prime-cli/install.sh | bash
```

After installation, reload your shell
```bash
source ~/.bashrc  # For bash users
# OR
source ~/.zshrc   # For zsh users
```

Verify installation:
```bash
prime-cli --version
```

### Prerequisites

#### For Docker-based Setup (Optional)
If you don't have Docker installed or need to configure it:
```bash
prime-cli docker-setup
```

### Basic Usage

1. Create a new instance:
```bash
prime-cli add my-instance --type community 
```
> Allowed types: `community` (default), `commercial`

2. Install Plane:
```bash
prime-cli install --domain plane.example.com 
```

3. Start the instance:
```bash
prime-cli start
```

### Common Commands

- `prime-cli list` - List all instances
- `prime-cli switch <instance>` - Switch between instances
- `prime-cli status` - View instance status
- `prime-cli stop` - Stop instance
- `prime-cli restart` - Restart instance
- `prime-cli monitor` - Monitor services
- `prime-cli configure` - Update configuration
- `prime-cli backup` - Create backup
- `prime-cli restore <backup-path>` - Restore from backup

### Kubernetes Setup

#### Prerequisites
- A working Kubernetes cluster and valid `kubeconfig` context
- Helm (optional - you can install it with `prime-cli helm-setup` if needed)

To deploy on Kubernetes:

1. Create instance:
```bash
prime-cli add my-instance --type community --kubernetes
```

3. Install:
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

## Support

- Issues: [Report bugs](https://github.com/makeplane/prime-cli/issues)
- Documentation: [View full docs](https://docs.plane.so)

## License

Licensed under the [MIT License](LICENSE)
