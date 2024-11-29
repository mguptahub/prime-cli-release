# Prime CLI Command Reference

Complete documentation of all Prime CLI commands and their options.

## Global Flags

These flags can be used with any command:

- `--debug`: Enable debug logging
- `--help`, `-h`: Show command help
- `--version`, `-v`: Show CLI version

## Instance Management Commands

### Create Instance
```bash
prime-cli add <name> [flags]

Flags:
  --dir string    Custom installation directory (default: ~/.prime/<name>)
  --force         Force overwrite if directory exists
```

### List Instances
```bash
prime-cli list

Notes:
- Shows all configured instances
- Current instance marked with *
```

### Switch Instance
```bash
prime-cli switch <name>

Notes:
- Switches active instance context
- Required before using other commands
```

### Remove Instance
```bash
prime-cli remove <name> [flags]

Flags:
  --force         Skip confirmation prompt

Notes:
- Removes instance from management
- Optionally deletes installation directory
```

## Install Commands

### Configure Instance
```bash
prime-cli install [flags]

Required Flags:
  --domain string               Domain name for instance

Optional Flags:
  # Basic Configuration
  --http-port int              HTTP port (default: 80)
  --https-port int             HTTPS port (default: 443)
  --ssl                        Enable SSL/TLS
  --start                      Start after install
  --release string             Specific version to install

  # Repository Configuration
  --github-token, -t string    GitHub token for private repos
  --github-repo, -r string     Custom GitHub repository
  --compose-file, -f string    Custom compose file name
  --env-file string           Custom env file name
  --additional-file strings    Additional files to download

  # Environment Variables
  --env, -e stringArray        Set env variables (KEY=VALUE)

  # Remote Services
  --remote-db-url string       PostgreSQL database URL
  --remote-redis-url string    Redis URL
  
  # S3 Storage
  --s3-bucket string           S3 bucket name
  --s3-region string           S3 region
  --s3-access-key-id string    S3 access key
  --s3-secret-access-key string S3 secret key
  --s3-endpoint string         S3 endpoint URL

Notes:
- All configuration stored in ~/.prime-cli/config
- Environment variables take precedence over defaults
```

## Operation Commands

### Start Instance
```bash
prime-cli start
Aliases: up

Notes:
- Starts all services
- Creates required directories
- Loads environment configuration
```

### Stop Instance
```bash
prime-cli stop
Aliases: down

Notes:
- Stops all services
- Preserves data directories
```

### Restart Instance
```bash
prime-cli restart

Notes:
- Equivalent to stop + start
- Reloads configuration
```

### View Status
```bash
prime-cli status [flags]
Aliases: ps, monitor

Flags:
  -f, --follow    Live status updates

Notes:
- Shows running services
- Displays ports and health status
```

### View Logs
```bash
prime-cli logs <service> [flags]
Alias: log

Flags:
  -f, --follow        Follow log output
  --tail string       Number of lines (default "100")

Notes:
- Streams service logs
- Supports all docker-compose services
```

### Pull Updates
```bash
prime-cli pull

Notes:
- Downloads latest Docker images
- Does not upgrade version
```

## Maintenance Commands

### Upgrade Instance
```bash
prime-cli upgrade [flags]

Flags:
  --start         Start after upgrade

Notes:
- Updates to latest version
- Preserves configuration
- Backs up data
```

### Repair Installation
```bash
prime-cli repair

Notes:
- Fixes broken installations
- Preserves data and configuration
- Downloads fresh files
```

### Update CLI
```bash
prime-cli update-cli

Notes:
- Updates Prime CLI itself
- Preserves instance configurations
```

### Uninstall Instance
```bash
prime-cli uninstall [flags]

Flags:
  --force         Skip confirmation

Notes:
- Removes instance files
- Optionally preserves data
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
```
