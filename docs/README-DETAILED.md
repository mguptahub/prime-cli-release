# Prime CLI - Detailed Command Reference

Prime CLI is a powerful command-line interface tool for managing Plane instances. This document provides comprehensive documentation of all available commands, sub-commands, and their options.

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

## Table of Contents
- [Docker Setup](#docker-setup)
- [Global Flags](#global-flags)
- [Instance Management Commands](#instance-management-commands)
  - [Add Instance](#add-instance)
  - [List Instances](#list-instances)
  - [Switch Instance](#switch-instance)
  - [Status](#status)
  - [Remove Instance](#remove-instance)
- [Installation Commands](#installation-commands)
  - [Install](#install)
  - [Configure](#configure)
  - [Upgrade](#upgrade)
  - [Update CLI](#update-cli)
- [Operation Commands](#operation-commands)
  - [Start](#start)
  - [Stop](#stop)
  - [Restart](#restart)
  - [Monitor](#monitor)
  - [Pull](#pull)
- [Maintenance Commands](#maintenance-commands)
  - [Repair](#repair)
  - [Backup](#backup)
  - [Restore](#restore)


## Docker Setup
Ensures Docker is properly configured for Plane.

```bash
prime-cli docker-setup
```

**Actions:**
- Verifies Docker installation
- Checks Docker daemon status
- Configures Docker for optimal use with Plane
- Attempts automatic installation on Linux systems if needed
- Exit and restart the terminal session if necessary
- Check the status of the Docker daemon after installation by running `docker --version`


## Global Flags

These flags are available for all commands:

| Flag | Description |
|------|-------------|
| `--debug` | Enable debug logging for verbose output |
| `--help`, `-h` | Display help information for any command |
| `--version`, `-v` | Display version information |

## Instance Management Commands

### Add Instance
Creates a new Plane instance.

```bash
prime-cli add <name>
Aliases: create, new
```

**Arguments:**
- `name`: Name of the instance (required)
  - Must be 3-20 characters long
  - Only lowercase alphanumeric characters allowed

**Flags:**
| Flag | Description |
|------|-------------|
| `--dir` | Custom installation directory (default: ~/.prime/<name>) |
| `--type` | Instance type (community, commercial) |
| `--force` | Force create, overwrite if exists |

**Default Behavior:**
- Creates instance configuration in `~/.prime-cli`
- Sets up installation directory at `~/.prime/<name>`

### List Instances
Displays all configured instances.

```bash
prime-cli list
Aliases: ls
```

**Output Information:**
- Lists all configured instances
- Marks current instance with an asterisk (*)
- Shows instance status (Ready/Not Ready)
- Displays installation directory

### Switch Instance
Changes the active instance context.

```bash
prime-cli switch <name>
Aliases: use
```

**Arguments:**
- `name`: Name of the instance to switch to (required)

**Notes:**
- Must be run before using instance-specific commands
- Validates instance exists before switching
- Updates current instance pointer in configuration

### Status
Shows detailed information about an instance.

```bash
prime-cli status [instance]
```

**Arguments:**
- `instance`: Name of the instance (optional, defaults to current instance)

**Output Information:**
- Instance name and installation directory
- Instance state (Ready, Running)
- Start and stop timestamps
- Domain and app version
- Volume mapping configuration
- GitHub repository details
- Docker compose configuration
- Additional files and custom configurations
- Registry settings

### Remove Instance
Removes an instance configuration.

```bash
prime-cli remove <name>
Aliases: rm, delete
```

**Arguments:**
- `name`: Name of the instance to remove (required)

**Flags:**
| Flag | Description |
|------|-------------|
| `--force` | Force remove without confirmation |

**Notes:**
- Removes instance configuration from `~/.prime-cli`
- Optionally removes installation directory from `~/.prime/<name>`

## Installation Commands

### Install
Installs Plane on the current instance.

```bash
prime-cli install [flags]
```

**Required Flags:**
- `--domain <domain-name>`: Domain name for the instance

**Optional Flags:**

*Source Configuration:*
| Flag | Description |
|------|-------------|
| `--release <version>` | Specific version to install |
| `--start`, `-s` | Start after installation |

*GitHub Based Configuration:*
| Flag | Description |
|------|-------------|
| `--github-repo <repo>` | Custom GitHub repository |
| `--github-token`, `-t` | GitHub token for private repos |
| `--compose-file`, `-f` | Custom compose file name |
| `--compose-env`, `-n` | Custom env file name |
| `--additional-file` | Additional files to download |

*URL Based Configuration:*
| Flag | Description |
|------|-------------|
| `--compose-file-url` | URL to download compose file (format: filename=url) |
| `--compose-env-url` | URL to download env file (format: filename=url) |
| `--additional-file-url` | URL to download additional files (format: filename=url) |

*Environment Configuration:*
| Flag | Description |
|------|-------------|
| `--env`, `-e` | Set environment variables (format: KEY=VALUE) |
| `--map-volume-to-disk` | Map volumes to disk |
| `--scale` | Scale services (format: SERVICE=COUNT) |

*Docker Registry Configuration:* (optional)
| Flag | Description |
|------|-------------|
| `--registry-url` | Docker registry URL (default: https://index.docker.io/v1/) |
| `--registry-username` | Registry username |
| `--registry-password` | Registry password |
| `--registry-email` | Registry email |

### Configure
Updates instance configuration.

```bash
prime-cli configure [flags]
Aliases: config
```

**Flags:**
| Flag | Description |
|------|-------------|
| `--domain <domain>` | Update domain name |
| `--env`, `-e` | Set environment variables (format: KEY=VALUE) |
| `--scale` | Scale services (format: SERVICE=COUNT) |

**Subcommands:**

#### List Configuration (ls)
Display current configuration.

```bash
prime-cli configure ls
Aliases: list
```

**Output Information:**
- Services:
  * Lists all services defined in compose file
  * Shows service names in alphabetical order
- Environment Variables:
  * Shows all configured environment variables
  * Displays KEY=VALUE pairs
  * Includes both default and custom variables

#### View Configuration
View the current Docker Compose configuration.

```bash
prime-cli configure view
Aliases: print
```

**Flags:**
| Flag | Description |
|------|-------------|
| `--out`, `-o` | Save the configuration to the specified file path |

**Output Information:**
- If the service is running, displays the current `.run.yml` configuration
- If the service is not running, generates and displays a new configuration
- Use `--out` flag to save the configuration to a file instead of displaying it

**Examples:**
```bash
# Display configuration
prime-cli configure view

# Save configuration to file
prime-cli configure view --out /path/to/config.yml
prime-cli configure view -o ./my-config.yml
```

**Notes:**
- At least one flag must be specified for the main configure command
- Changes take effect after restart
- Multiple `--env` flags can be used
- Scale accepts multiple service specifications

### Upgrade
Upgrades instance to latest version.

```bash
prime-cli upgrade [flags]
```

**Flags:**
| Flag | Description |
|------|-------------|
| `--start`, `-s` | Start after upgrade |

**Notes:**
- Preserves existing configuration
- Downloads new Docker images
- Updates compose files if needed

### Update CLI
Updates the Prime CLI tool itself.

```bash
prime-cli update-cli
```

**Notes:**
- Updates only the CLI binary
- Preserves all instance configurations
- Checks GitHub for latest release

## Operation Commands

### Start
Starts all services for current instance.

```bash
prime-cli start
Aliases: up
```

**Notes:**
- Starts all configured services
- Applies current environment configuration
- Respects service scaling settings

### Stop
Stops all services for current instance.

```bash
prime-cli stop
Aliases: down
```

**Notes:**
- Stops all running services
- Preserves volume data
- Updates instance status

### Restart
Restarts all services for current instance.

```bash
prime-cli restart
Aliases: reboot
```

**Notes:**
- Equivalent to stop followed by start
- Reloads all configuration
- Preserves volume data

### Monitor
Shows status of running services.

```bash
prime-cli monitor
Aliases: ps
```

**Output Information:**
- Lists all services
- Shows container status
- Displays resource usage
- Indicates service health

### Pull
Updates Docker images.

```bash
prime-cli pull
Aliases: get
```

**Notes:**
- Downloads latest Docker images
- Does not change version
- Updates only container images

## Maintenance Commands

### Repair
Repairs broken installations.

```bash
prime-cli repair
```

**Notes:**
- Not yet implemented
- Will fix common installation issues
- Validates configuration integrity

### Backup
Creates a backup of the current Plane instance.

```bash
prime-cli backup [flags]
```

**Subcommands:**
- `list`, `ls`: Lists all available backups
- `validate`, `check`: Validates a backup

#### Backup Creation
Running `backup` without subcommands creates a new backup:
- Creates a timestamped backup in the instance's backup directory
- Includes database data, configuration files, and environment settings
- Backup directory: `<instance-dir>/backups/<timestamp>`

#### List Backups
```bash
prime-cli backup list
Aliases: ls
```

**Output Information:**
- Lists all available backups for the current instance
- Shows backup date and time
- Displays backup size
- Shows backup path

#### Validate Backup
```bash
prime-cli backup validate <backup-path>
Aliases: check
```

**Arguments:**
- `backup-path`: Path to the backup directory to validate (required)

**Validation Checks:**
- Verifies backup structure and integrity
- Checks for required files and configurations
- Validates backup metadata

### Restore
Restores a Plane instance from a backup.

```bash
prime-cli restore [flags]
```

**Required Flags:**
| Flag | Description |
|------|-------------|
| `--backup`, `-b` | Path to backup directory (required) |

**Notes:**
1. Ensure the instance is stopped before restoration
2. Backup validation is performed before restoration
3. Current data will be replaced with backup data
4. Service configurations will be restored to backup state

## Usage Notes

1. Instance names must be 3-20 characters long and contain only lowercase alphanumeric characters.
2. Commands requiring instance context will fail if no instance is selected.
3. SSL setup requires proper DNS configuration.
4. Remote services need valid connection strings.
5. Multiple `--env` flags can be used for setting environment variables.
6. The `--debug` flag enables verbose logging for troubleshooting.

For detailed help on any command:
```bash
prime-cli [command] --help
