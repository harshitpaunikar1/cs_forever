# Terminal & Bash Scripting

The terminal is the primary interface for interacting with servers and automating
infrastructure tasks. A strong command of Bash and the Unix toolset is non-negotiable
for anyone working in DevOps. This page covers everything from basic navigation through
production-grade scripting patterns.

---

## Shell Types

| Shell | Notes |
|-------|-------|
| `bash` | Bourne Again Shell — the default on most Linux distros; POSIX-compliant plus extensions |
| `zsh` | Default on macOS; better tab completion and plugin ecosystem (Oh My Zsh) |
| `sh` | POSIX shell; most portable, least featureful; used in Docker `CMD` and init scripts |
| `fish` | Friendly interactive shell; not POSIX-compatible; great for humans, avoid in scripts |
| `dash` | Faster sh-compatible shell; used as `/bin/sh` on Debian/Ubuntu |

**Rule**: Write scripts with `#!/usr/bin/env bash` (or `#!/bin/sh` for maximum portability).
Never rely on `#!/bin/sh` pointing to bash — on Ubuntu it points to dash.

---

## Navigation

```bash
pwd                    # Print working directory
ls -la                 # List all files including hidden, long format
ls -lh                 # Human-readable file sizes
cd /etc/nginx          # Change to absolute path
cd ..                  # Go up one level
cd -                   # Go back to previous directory
pushd /tmp             # Push current dir to stack, go to /tmp
popd                   # Pop back to previous dir
```

### Finding Files

```bash
find /var/log -name "*.log" -mtime -7        # Logs modified in last 7 days
find /home -type f -size +100M               # Files larger than 100MB
find . -name "*.conf" -exec grep -l "proxy" {} \;  # Conf files containing "proxy"
locate nginx.conf                            # Fast search using mlocate database
which python3                                # Find executable in PATH
type curl                                    # Shows if it's an alias, function, or binary
```

---

## File Operations

```bash
# Create
touch app.log                  # Create empty file or update timestamp
mkdir -p /opt/app/config       # Create directory and parents

# Copy / Move
cp -r src/ dst/                # Recursive copy
cp -a src/ dst/                # Archive: preserves permissions, timestamps, symlinks
mv old.txt new.txt             # Move or rename
rsync -avz src/ user@host:dst/ # Efficient sync (skips unchanged files)

# Delete
rm file.txt
rm -rf /tmp/old-build          # Recursive force delete — be careful
rmdir empty_dir                # Remove empty directory only

# Links
ln -s /opt/app/current /usr/local/bin/app  # Symbolic link
ln file.txt hardlink.txt                    # Hard link (same inode)

# Viewing
cat /etc/os-release
less /var/log/syslog           # Scrollable viewer
head -20 access.log            # First 20 lines
tail -f /var/log/nginx/error.log  # Follow (live stream)
tail -n 100 app.log            # Last 100 lines
```

---

## Text Processing

### grep

```bash
grep "ERROR" app.log                        # Lines containing ERROR
grep -i "error" app.log                     # Case-insensitive
grep -r "database_url" /etc/               # Recursive directory search
grep -v "DEBUG" app.log                     # Invert: exclude matching lines
grep -c "ERROR" app.log                     # Count matching lines
grep -n "WARN" app.log                      # Show line numbers
grep -A 3 -B 2 "EXCEPTION" app.log         # 3 lines after, 2 before
grep -E "ERROR|FATAL" app.log              # Extended regex (egrep equivalent)
grep -P "\d{4}-\d{2}-\d{2}" app.log        # Perl regex
```

### sed

```bash
sed 's/foo/bar/' file.txt                  # Replace first occurrence per line
sed 's/foo/bar/g' file.txt                 # Replace all occurrences
sed -i 's/old/new/g' config.conf           # In-place edit
sed -i.bak 's/old/new/g' file             # In-place with backup
sed -n '10,20p' file.txt                   # Print lines 10-20
sed '/^#/d' config.conf                    # Delete comment lines
sed 's/^[[:space:]]*//' file              # Strip leading whitespace
```

### awk

```bash
awk '{print $1, $3}' access.log            # Print columns 1 and 3
awk -F: '{print $1}' /etc/passwd           # Use : as delimiter, print first field
awk '$9 == "404" {print $7}' access.log    # Filter by column value (HTTP 404 URLs)
awk '{sum += $1} END {print sum}' nums.txt # Sum a column
awk 'NR > 5' file.txt                      # Skip first 5 lines
awk 'length($0) > 80' file.txt             # Lines longer than 80 chars
```

### Other text tools

```bash
cut -d: -f1,3 /etc/passwd       # Extract fields 1 and 3 (: delimiter)
sort -k2 -n file.txt            # Sort by column 2, numerically
sort -u file.txt                # Sort and remove duplicates
uniq -c sorted.txt              # Count consecutive duplicates
wc -l file.txt                  # Line count
wc -w file.txt                  # Word count
tr 'a-z' 'A-Z' < file.txt      # Translate (lowercase to uppercase)
tr -d '\r' < windows.txt        # Delete carriage returns
paste file1.txt file2.txt       # Merge files side by side
join file1.txt file2.txt        # SQL-style join on first field
```

---

## Pipes and Redirection

```bash
# Pipes
ls -la | grep ".log" | wc -l         # Count .log files
cat access.log | awk '{print $1}' | sort | uniq -c | sort -rn | head -10
                                      # Top 10 IPs by request count

# Redirection
command > output.txt                  # Stdout to file (overwrite)
command >> output.txt                 # Stdout to file (append)
command < input.txt                   # Stdin from file
command 2> errors.txt                 # Stderr to file
command > output.txt 2>&1            # Both stdout and stderr to file
command 2>/dev/null                   # Discard stderr
command > /dev/null 2>&1             # Discard all output

# Process substitution
diff <(sort file1.txt) <(sort file2.txt)  # Diff sorted versions

# tee: write to file AND stdout
command | tee output.txt             # See output and save it
command | tee -a output.txt          # Append mode
```

---

## Permissions

```bash
# View permissions
ls -l file.txt         # -rw-r--r-- 1 user group 1234 Jan 1 file.txt
stat file.txt          # Detailed: permissions, inode, size, timestamps

# chmod: symbolic
chmod u+x script.sh    # Add execute for owner
chmod g-w file.txt     # Remove write for group
chmod o=r file.txt     # Set others to read-only
chmod a+x script.sh    # Add execute for all

# chmod: numeric (octal)
chmod 755 script.sh    # rwxr-xr-x
chmod 644 file.txt     # rw-r--r--
chmod 600 ~/.ssh/id_rsa  # rw------- (SSH key requirement)
chmod 700 ~/.ssh         # rwx------

# chown
chown user:group file.txt
chown -R www-data:www-data /var/www/html
chgrp docker /var/run/docker.sock

# umask
umask            # Show current umask (e.g., 0022)
umask 0027       # New files: 640, new dirs: 750

# Special bits
chmod u+s /usr/bin/passwd   # setuid: run as file owner
chmod g+s /shared/dir       # setgid: new files inherit group
chmod +t /tmp               # sticky bit: only owner can delete
```

---

## Process Management

```bash
# View processes
ps aux                         # All processes (BSD style)
ps -ef                         # All processes (POSIX style)
ps aux | grep nginx            # Find process by name
pgrep nginx                    # PIDs matching name
top                            # Interactive process viewer
htop                           # Better interactive viewer

# Kill
kill 1234                      # Send SIGTERM (graceful)
kill -9 1234                   # Send SIGKILL (force)
kill -HUP $(pgrep nginx)       # Reload nginx config
pkill -f "python app.py"       # Kill by command pattern
killall nginx                  # Kill all processes named nginx

# Background/foreground
command &                      # Run in background
jobs                           # List background jobs
fg %1                          # Bring job 1 to foreground
bg %1                          # Resume job 1 in background
Ctrl+Z                         # Suspend foreground job
nohup command &                # Run immune to hangup signal
disown %1                      # Detach job from shell (won't die on logout)

# Priority
nice -n 10 command             # Start with lower priority (+10 niceness)
renice 15 -p 1234             # Change priority of running process
```

---

## Environment Variables

```bash
# View
env                           # All environment variables
printenv HOME                 # Print specific variable
echo $PATH                    # Print PATH

# Set
export MY_VAR="hello"         # Set and export to child processes
export PATH="$PATH:/opt/bin"  # Append to PATH

# Unset
unset MY_VAR

# Persistence
# ~/.bashrc         — interactive non-login shells (most terminal sessions)
# ~/.bash_profile   — login shells (SSH, su -)
# ~/.profile        — sh-compatible login shells
# /etc/environment  — system-wide, plain KEY=VALUE, no export
# /etc/profile.d/   — drop-in scripts for all users
```

---

## Bash Scripting

### Structure

```bash
#!/usr/bin/env bash
# Script description
# Usage: ./script.sh [args]

set -euo pipefail   # Exit on error, undefined vars, pipe failures

# Constants
readonly LOG_DIR="/var/log/myapp"
readonly SCRIPT_DIR="$(cd "$(dirname "${BASH_SOURCE[0]}")" && pwd)"
```

### Variables and Quoting

```bash
name="world"
echo "Hello $name"          # Double quotes: variable expansion
echo 'Hello $name'          # Single quotes: literal string
echo "Path: ${name}_suffix" # Braces required when followed by word chars

# Default values
echo "${VAR:-default}"       # Use default if VAR unset or empty
echo "${VAR:=default}"       # Assign default if VAR unset or empty
echo "${VAR:?error message}" # Error and exit if VAR unset or empty

# String length
echo "${#name}"              # 5

# Substrings
echo "${name:0:3}"           # First 3 chars
echo "${name: -3}"           # Last 3 chars

# String replacement
file="backup.tar.gz"
echo "${file%.gz}"           # Remove .gz suffix: backup.tar
echo "${file%%.*}"           # Remove all from first dot: backup
echo "${file#backup.}"       # Remove prefix: tar.gz
```

### Conditionals

```bash
# File tests
if [[ -f "/etc/nginx/nginx.conf" ]]; then
  echo "Config exists"
fi

if [[ -d "/var/log" && -w "/var/log" ]]; then
  echo "Log dir exists and is writable"
fi

# String tests
if [[ "$ENV" == "production" ]]; then
  echo "Production mode"
elif [[ "$ENV" == "staging" ]]; then
  echo "Staging mode"
else
  echo "Unknown environment"
fi

# Numeric tests
count=5
if (( count > 0 )); then
  echo "Has items"
fi

# Command success test
if curl -sf https://api.example.com/health; then
  echo "API is up"
else
  echo "API is down"
fi

# Common test flags
# -f  file exists and is a regular file
# -d  file exists and is a directory
# -e  file exists (any type)
# -r  readable
# -w  writable
# -x  executable
# -z  string is empty
# -n  string is non-empty
# -eq -ne -lt -le -gt -ge  numeric comparisons
```

### Loops

```bash
# For loop over list
for env in dev staging prod; do
  echo "Deploying to $env"
done

# For loop over files
for file in /etc/nginx/conf.d/*.conf; do
  nginx -t -c "$file" && echo "OK: $file"
done

# C-style for loop
for (( i=0; i<10; i++ )); do
  echo "Iteration $i"
done

# While loop
while IFS= read -r line; do
  echo "Processing: $line"
done < servers.txt

# Until loop
until curl -sf http://localhost/health; do
  echo "Waiting for service..."
  sleep 2
done
echo "Service is up!"

# Loop control
for item in "${items[@]}"; do
  [[ "$item" == "skip" ]] && continue
  [[ "$item" == "stop" ]] && break
  process "$item"
done
```

### Functions

```bash
# Define
log() {
  local level="$1"
  local message="$2"
  echo "$(date '+%Y-%m-%dT%H:%M:%S') [$level] $message" >&2
}

deploy() {
  local environment="$1"
  local version="$2"

  log "INFO" "Starting deploy of $version to $environment"

  if [[ -z "$environment" || -z "$version" ]]; then
    log "ERROR" "Usage: deploy <environment> <version>"
    return 1
  fi

  # ... deploy logic ...
  log "INFO" "Deploy complete"
  return 0
}

# Arrays
servers=("web1" "web2" "db1")
echo "${servers[0]}"         # First element
echo "${servers[@]}"         # All elements
echo "${#servers[@]}"        # Array length
servers+=("cache1")          # Append

for server in "${servers[@]}"; do
  ssh "$server" "uptime"
done
```

### Error Handling

```bash
set -e           # Exit immediately on error
set -u           # Treat unset variables as error
set -o pipefail  # Pipeline fails if any command fails
set -x           # Print each command before executing (debug mode)

# Trap for cleanup
cleanup() {
  log "INFO" "Cleaning up..."
  rm -f /tmp/deploy.lock
}
trap cleanup EXIT          # Run cleanup on exit (normal or error)
trap cleanup ERR SIGINT SIGTERM

# Check exit codes explicitly
if ! command; then
  echo "Command failed" >&2
  exit 1
fi

# Ignore errors selectively
rm -f /tmp/optional_file || true
```

---

## Here Documents

```bash
# Write multi-line content
cat > /etc/nginx/conf.d/app.conf << 'EOF'
server {
    listen 80;
    server_name example.com;
    location / {
        proxy_pass http://localhost:3000;
    }
}
EOF

# Feed to command
ssh user@host << 'ENDSSH'
  sudo apt-get update
  sudo apt-get install -y nginx
ENDSSH

# Variable expansion (no quotes on delimiter)
cat > config.env << EOF
APP_ENV=$ENVIRONMENT
APP_VERSION=$VERSION
EOF
```

---

## Cron Jobs

```bash
# Crontab syntax: minute hour day-of-month month day-of-week command
# *      *    *              *     *           command
# 0-59   0-23 1-31           1-12  0-7 (0 and 7 = Sunday)

crontab -e              # Edit current user's crontab
crontab -l              # List current user's crontab
sudo crontab -u www-data -e  # Edit another user's crontab

# Common schedules
# 0 * * * *       Every hour
# 0 2 * * *       Daily at 2 AM
# 0 2 * * 0       Weekly on Sunday at 2 AM
# 0 2 1 * *       Monthly on the 1st at 2 AM
# */5 * * * *     Every 5 minutes
# 0 9-17 * * 1-5  Every hour from 9-5, Mon-Fri

# Always redirect output or cron will email you
0 2 * * * /opt/scripts/backup.sh >> /var/log/backup.log 2>&1

# System cron directories (no crontab, root-owned)
# /etc/cron.hourly/
# /etc/cron.daily/
# /etc/cron.weekly/
# /etc/cron.monthly/
```

---

## SSH

```bash
# Key generation
ssh-keygen -t ed25519 -C "your_email@example.com"   # Recommended
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"  # RSA fallback

# Copy public key to server
ssh-copy-id user@host
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@host

# SSH agent
eval "$(ssh-agent -s)"     # Start agent
ssh-add ~/.ssh/id_ed25519  # Add key to agent
ssh-add -l                 # List loaded keys

# ~/.ssh/config
cat >> ~/.ssh/config << 'EOF'
Host bastion
    HostName 1.2.3.4
    User ec2-user
    IdentityFile ~/.ssh/prod_key

Host prod-*
    User ubuntu
    ProxyJump bastion
    IdentityFile ~/.ssh/prod_key
    ServerAliveInterval 60
EOF

# Port forwarding
ssh -L 5432:db.internal:5432 user@bastion   # Local forward (access remote DB locally)
ssh -R 8080:localhost:80 user@server        # Remote forward
ssh -D 1080 user@server                     # SOCKS proxy
ssh -N -f -L 5432:db:5432 user@bastion     # Background, no command
```

---

## Practical Scripts

### Health Check Script

```bash
#!/usr/bin/env bash
set -euo pipefail

check_service() {
  local name="$1"
  local url="$2"
  local http_code

  http_code=$(curl -s -o /dev/null -w "%{http_code}" --max-time 5 "$url")

  if [[ "$http_code" == "200" ]]; then
    echo "OK   [$http_code] $name"
    return 0
  else
    echo "FAIL [$http_code] $name"
    return 1
  fi
}

failed=0
check_service "API"       "http://localhost:8080/health" || (( failed++ ))
check_service "Admin UI"  "http://localhost:8081/"       || (( failed++ ))
check_service "Metrics"   "http://localhost:9090/"       || (( failed++ ))

if (( failed > 0 )); then
  echo "$failed service(s) failed" >&2
  exit 1
fi
```

### Backup Script

```bash
#!/usr/bin/env bash
set -euo pipefail

BACKUP_DIR="/backups"
SOURCE_DIR="/opt/app/data"
RETENTION_DAYS=30
TIMESTAMP=$(date +%Y%m%d_%H%M%S)
BACKUP_FILE="$BACKUP_DIR/backup_${TIMESTAMP}.tar.gz"

mkdir -p "$BACKUP_DIR"

echo "Starting backup..."
tar -czf "$BACKUP_FILE" -C "$(dirname "$SOURCE_DIR")" "$(basename "$SOURCE_DIR")"
echo "Backup created: $BACKUP_FILE ($(du -sh "$BACKUP_FILE" | cut -f1))"

# Upload to S3
aws s3 cp "$BACKUP_FILE" "s3://my-backups/app/" && echo "Uploaded to S3"

# Delete old local backups
find "$BACKUP_DIR" -name "backup_*.tar.gz" -mtime "+$RETENTION_DAYS" -delete
echo "Pruned backups older than $RETENTION_DAYS days"
```

---

## Essential Tools

| Tool | Use |
|------|-----|
| `tmux` / `screen` | Terminal multiplexer — persist sessions over SSH |
| `curl` | HTTP requests, file downloads, API testing |
| `wget` | File downloads with resume support |
| `jq` | JSON processor: `curl ... \| jq '.items[].name'` |
| `xargs` | Build and execute commands from stdin |
| `parallel` | Run commands in parallel (GNU parallel) |
| `bc` | Calculator for scripts: `echo "scale=2; 100/3" \| bc` |
| `diff` / `vimdiff` | Compare files |
| `lsof` | List open files/sockets: `lsof -i :8080` |
| `strace` | Trace system calls for debugging |
| `watch` | Repeat a command: `watch -n 2 'df -h'` |
