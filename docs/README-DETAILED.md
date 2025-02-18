# Prime CLI - Detailed Command Reference

## Table of Contents
- [Overview](#overview)
- [File Locations](#file-locations)
- [Prerequisites](#prerequisites)
- [Global Flags](#global-flags)
- [Instance Management Commands](#instance-management-commands)
- [Instance Lifecycle Commands](#instance-lifecycle-commands)
- [Maintenance and Configuration Commands](#maintenance-and-configuration-commands)
- [Data Protection Commands](#data-protection-commands)
- [CLI Tool Management Commands](#cli-tool-management-commands)
- [Runtime Tools Management Commands](#runtime-tools-management-commands)

## Overview

Prime CLI provides a comprehensive set of commands for managing Plane instances. This document details each command's usage, options, and examples.

## File Locations

Prime CLI uses several key locations for its operation:

| Location | Description |
|----------|-------------|
| `~/.local/bin/prime-cli` | Default CLI installation path |
| `~/.prime-cli/config` | Instance configuration file storing all instance metadata |
| `~/.prime/<instance-name>` | Default instance installation directory |

The instance configuration file (`~/.prime-cli/config`) stores:
- List of all instances
- Current active instance
- Instance-specific settings
- Installation paths
- Version information
- Registry configurations

## Prerequisites

### For Docker-based Deployments
- Docker installed and running
- Docker Compose support
- Optional: Run `prime-cli docker-setup` to configure Docker

### For Kubernetes-based Deployments
- Access to a Kubernetes cluster
- Valid kubeconfig and context
- Helm (Optional: Install using `prime-cli helm-setup`)
- Storage classes for persistence

## Global Flags

Available for all commands:

| Flag | Description |
|------|-------------|
| `--debug` | Enable debug logging |
| `--help`, `-h` | Show help for any command |
| `--version`, `-v` | Show CLI version |

## Instance Management Commands

### add
Creates a new Plane instance.

```bash
prime-cli add <name> [flags]
Aliases: create, new
```

**Arguments:**
- `name`: Instance name (required)
  - Must be 3-20 characters
  - Only lowercase alphanumeric characters

**Flags:**
| Flag | Description | Default |
|------|-------------|---------|
| `--dir` | Installation directory | ~/.prime/<name> |
| `--type` | Instance type (community/commercial) | community |
| `--force` | Force create, overwrite if exists | false |
| `--kubernetes` | Use Kubernetes deployment | false |
| `--kubeconfig` | Path to kubeconfig file | ~/.kube/config |
| `--kubecontext` | Kubernetes context to use | current-context |

### list
Shows all configured instances.

```bash
prime-cli list
Alias: ls
```

**Output includes:**
- Instance name
- Type (community/commercial)
- Ready status
- Kubernetes status
- Running status
- Installation path
- Current instance marker (*)

### switch
Changes the active instance.

```bash
prime-cli switch <name>
Alias: use
```

**Arguments:**
- `name`: Instance name to switch to (required)

### status
Displays detailed instance information.

```bash
prime-cli status [instance]
```

**Arguments:**
- `instance`: Optional instance name (defaults to current)

**Shows:**
- Basic Info:
  - Name and install directory
  - Type and version
  - Domain configuration
  - Running status
- Docker-specific:
  - Service status
  - Volume mappings
  - Registry settings
- Kubernetes-specific:
  - Namespace
  - Release name
  - Resource status

### remove
Removes an instance.

```bash
prime-cli remove <name>
Aliases: rm, delete
```

**Flags:**
| Flag | Description |
|------|-------------|
| `--force` | Skip confirmation |

## Instance Lifecycle Commands

### install
Installs or configures a Plane instance.

```bash
# Docker-based installation
prime-cli install --domain example.com [flags]

# Kubernetes-based installation
prime-cli install --release-name plane --namespace plane [flags]
```

**Docker-specific Flags:**
| Flag | Description |
|------|-------------|
| `--domain` | Domain name (required) |
| `--release` | Plane version |
| `--map-volume-to-disk` | Map volumes to host |
| `--scale` | Scale services (SERVICE=COUNT) |

**Kubernetes-specific Flags:**
| Flag | Description |
|------|-------------|
| `--release-name` | Helm release name |
| `--namespace` | Kubernetes namespace |
| `--set` | Set Helm values |
| `--set-string` | Set string values |
| `--values` | Values file path |
| `--wait` | Wait for pods |

### configure
Updates instance configuration.

```bash
prime-cli configure [command]
Alias: config
```

**Subcommands:**
- `list` (alias: `ls`): Show current config
- `set`: Update configuration
- `view`: Display compose/values file
- `reload`: Regenerate configuration

**Common Flags for `set`:**
| Flag | Description |
|------|-------------|
| `--domain` | Update domain |
| `--env`, `-e` | Set environment variables |
| `--scale` | Scale services |
| `--restart` | Restart after changes |

## Maintenance and Configuration Commands

### start
Starts the instance services.

```bash
prime-cli start
Alias: up
```

### stop
Stops the instance services.

```bash
prime-cli stop
Alias: down
```

### restart
Restarts all services.

```bash
prime-cli restart
Alias: reboot
```

### monitor
Shows service status and logs.

```bash
prime-cli monitor
Alias: ps
```

**Features:**
- Real-time service status
- Log streaming
- Resource usage
- Interactive navigation

### pull
Updates service images.

```bash
prime-cli pull
Alias: get
```

## Data Protection Commands

### backup
Creates instance backup.

```bash
prime-cli backup
```

**Subcommands:**
- `list` (alias: `ls`): List backups
- `validate`: Check backup integrity

### restore
Restores from backup.

```bash
prime-cli restore <backup-path>
```

**Flags:**
| Flag | Description |
|------|-------------|
| `--backup`, `-b` | Backup path |

### repair
Repairs instance installation.

```bash
prime-cli repair
```

## CLI Tool Management Commands

### update-cli
Updates Prime CLI to latest version.

```bash
prime-cli update-cli
Alias: update
```

## Runtime Tools Management Commands

### docker-setup
Configures Docker as the default runtime.

```bash
prime-cli docker-setup
```

### helm-setup
Verifies and sets up Helm installation.

```bash
prime-cli helm-setup
```

## Usage Examples

### Docker-based Setup
```bash
# Create and install
prime-cli add plane-instance --type community
prime-cli install --domain plane.example.com --release v0.24.1 --start

# Scale services
prime-cli configure set --scale web=2 --scale worker=3 --restart

# Backup/Restore
prime-cli backup
prime-cli restore --backup /path/to/backup
```

### Kubernetes-based Setup
```bash
# Create and install
prime-cli add k8s-plane --type community --kubernetes
prime-cli install \
  --namespace plane \
  --release-name plane \
  --set ingress.host=plane.example.com

# Update configuration
prime-cli configure set \
  --set replicas.web=3 \
  --set replicas.worker=2
```

## Best Practices

1. **Instance Management**
   - Use meaningful instance names
   - Keep backups before major changes
   - Monitor resource usage

2. **Configuration**
   - Use environment files for sensitive data
   - Scale services based on load
   - Validate changes before production

3. **Maintenance**
   - Regular backups
   - Monitor logs for issues
   - Keep CLI and instances updated

## Troubleshooting

1. **Docker Issues**
   - Check Docker daemon status
   - Verify volume permissions
   - Review service logs

2. **Kubernetes Issues**
   - Validate kubeconfig
   - Check pod status and events
   - Verify storage classes

3. **General**
   - Use `--debug` for verbose logs
   - Check instance status
   - Verify network connectivity