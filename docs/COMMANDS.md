# Prime CLI Command Reference

Complete documentation of all Prime CLI commands and their options.

## Global Flags

These flags can be used with any command:

- `--debug`: Enable debug logging
- `--help`, `-h`: Show command help

## Instance Management Commands

### Create Instance
```bash
prime-cli add <name> [flags]

Notes:
- Creates a new Plane instance
- Default installation directory: ~/.prime/<name>
```

### List Instances
```bash
prime-cli list
Aliases: ls

Notes:
- Shows all configured instances
- Current instance marked with *
```

### Switch Instance
```bash
prime-cli switch <name>
Aliases: use

Notes:
- Switches active instance context
- Required before using other commands
```

### Instance Status
```bash
prime-cli status [instance]

Notes:
- Shows status of specified instance
- Shows current instance if none specified
```

### Remove Instance
```bash
prime-cli remove <name>
Aliases: rm, delete

Notes:
- Removes instance configuration
- Optionally removes installation directory
```

## Installation Commands

### Install Instance
```bash
prime-cli install --domain <domain-name> [flags]

Required Flags:
  --domain string               Domain name for instance

Optional Flags:
  # Source Configuration
  --release string             Specific version to install
  --start, -s                  Start after installation
  --github-repo string         Custom GitHub repository
  --github-token, -t string    GitHub token for private repos

  # File Configuration
  --compose-file, -f string    Custom compose file name
  --compose-file-url string    URL to download compose file (format: filename=url)
  --compose-env, -n string     Custom env file name
  --compose-env-url string     URL to download env file (format: filename=url)
  --additional-file strings    Additional files to download
  --additional-file-url string URL to download additional files (format: filename=url)

  # Environment Variables
  --env, -e stringArray        Set env variables (KEY=VALUE)
  --scale stringArray          Scale services (format: SERVICE=COUNT)

  # Registry Configuration
  --registry-url string        Docker registry URL
  --registry-username string   Registry username
  --registry-password string   Registry password
  --registry-email string      Registry email

Notes:
- Required for first-time setup
- Creates necessary configuration files
- Downloads required Docker images
```

### Configure Instance
```bash
prime-cli configure [flags]
Aliases: config

Flags:
  --domain string          Update domain name
  --env, -e stringArray    Set env variables (KEY=VALUE)
  --scale stringArray      Scale services (SERVICE=COUNT)

Subcommands:
  ls, list    List current configuration

Notes:
- Updates instance configuration
- Changes take effect after restart
```

### Upgrade Instance
```bash
prime-cli upgrade [flags]

Flags:
  --start, -s    Start after upgrade

Notes:
- Updates to latest version
- Preserves configuration
```

### Update CLI
```bash
prime-cli update-cli

Notes:
- Updates Prime CLI tool itself
- Preserves instance configurations
```

## Operation Commands

### Start Instance
```bash
prime-cli start
Aliases: up

Notes:
- Starts all services
- Updates environment configuration
```

### Stop Instance
```bash
prime-cli stop
Aliases: down

Notes:
- Stops all services
- Preserves data
```

### Restart Instance
```bash
prime-cli restart
Aliases: reboot

Notes:
- Equivalent to stop + start
- Reloads configuration
```

### Monitor Instance
```bash
prime-cli monitor
Aliases: ps

Notes:
- Shows running services
- Displays service status
```

### Pull Updates
```bash
prime-cli pull
Aliases: get

Notes:
- Downloads latest Docker images
- Does not upgrade version
```

## Maintenance Commands

### Repair Installation
```bash
prime-cli repair

Notes:
- Not yet implemented
- Will fix broken installations
```

### Backup Instance
```bash
prime-cli backup

Notes:
- Not yet implemented
- Will backup instance data
```

### Restore Instance
```bash
prime-cli restore

Notes:
- Not yet implemented
- Will restore instance data
```

## Usage Notes

- Instance names must be 3-20 characters, lowercase alphanumeric
- Commands requiring instance context fail if none selected
- SSL setup requires proper DNS configuration
- Remote services need valid connection strings
- Multiple `--env` flags can be used for environment variables
- The `--debug` flag enables verbose logging for troubleshooting

For detailed help on any command:
```bash
prime-cli [command] --help
