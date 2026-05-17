# Containers & Docker

Containers solve the "works on my machine" problem by packaging an application
together with all its dependencies into an isolated, reproducible unit. Docker
popularized the container model and remains the standard toolchain for building
and running containers. This page covers everything from Linux internals through
production best practices.

---

## What Containers Solve

Before containers, deploying software required:
- Matching exact library versions between dev and prod
- Managing conflicting dependencies across applications
- Slow, heavy VMs for isolation
- "It works on my machine" bugs that took hours to reproduce

Containers give you:
- **Reproducibility**: same image runs identically everywhere
- **Isolation**: processes, filesystem, and network are separated
- **Portability**: run on any Linux host, any cloud
- **Density**: dozens of containers per host vs a few VMs
- **Fast startup**: seconds, not minutes

---

## Containers vs VMs

| | Container | VM |
|--|----------|-----|
| Isolation | Namespace/cgroup (OS-level) | Hypervisor (hardware-level) |
| Overhead | Near-zero | Guest OS overhead |
| Startup | Seconds | Minutes |
| Image size | MBs | GBs |
| Kernel | Shared with host | Separate per VM |
| Security isolation | Weaker | Stronger |
| Use case | Microservices, CI | Database servers, legacy apps |

Use containers for stateless applications and services.
Use VMs when you need stronger isolation or a different OS kernel.

---

## Linux Primitives

Docker is just a friendly interface over Linux kernel features:

### Namespaces

Each namespace provides a container with an isolated view of a system resource:

| Namespace | Isolates |
|-----------|---------|
| `pid` | Process IDs — container processes can't see host PIDs |
| `net` | Network interfaces, routes, iptables rules |
| `mnt` | Mount points and filesystem |
| `uts` | Hostname and domain name |
| `ipc` | System V IPC, POSIX message queues |
| `user` | User and group IDs |
| `cgroup` | cgroup root directory |

### cgroups (Control Groups)

Limit and account for CPU, memory, I/O, and network resources:
- `memory.limit_in_bytes` — OOM kill if exceeded
- `cpu.cfs_quota_us` — CPU throttling
- `blkio.throttle.read_bps_device` — disk I/O limits

### Union Filesystems (overlay2)

Container images use layers. Each layer is a diff from the previous.
`overlay2` merges layers into a single unified view using:
- `lowerdir` — read-only image layers
- `upperdir` — read-write container layer
- `workdir` — overlay internal working directory

---

## Docker Architecture

```
docker CLI ──HTTP──► Docker daemon (dockerd)
                           │
              ┌────────────┼────────────┐
              │            │            │
           Images     Containers    Networks/Volumes
              │
         Docker Hub / Private Registry
```

- **daemon** (`dockerd`): background service that manages containers, images, networks
- **client** (`docker`): CLI that talks to daemon via REST API
- **registry**: stores and distributes images (Docker Hub, ECR, GCR, Harbor)
- **image**: read-only template with layers
- **container**: running instance of an image (adds writable layer)

---

## Docker CLI Essentials

```bash
# Images
docker pull nginx:1.25                     # Pull image
docker images                              # List local images
docker rmi nginx:1.25                      # Remove image
docker image prune                         # Remove dangling images
docker inspect nginx:1.25                  # Show image metadata

# Containers
docker run -d -p 8080:80 --name webserver nginx:1.25  # Run in background
docker run -it ubuntu:22.04 bash           # Interactive shell
docker ps                                  # Running containers
docker ps -a                               # All containers
docker stop webserver                      # Graceful stop (SIGTERM)
docker kill webserver                      # Force stop (SIGKILL)
docker rm webserver                        # Remove stopped container
docker rm -f webserver                     # Force remove running container

# Exec into running container
docker exec -it webserver bash
docker exec webserver nginx -t

# Logs
docker logs webserver
docker logs -f webserver                   # Follow
docker logs --tail 100 webserver

# Stats
docker stats                               # Live resource usage
docker top webserver                       # Processes in container

# Copy files
docker cp webserver:/etc/nginx/nginx.conf ./nginx.conf
docker cp ./config.json webserver:/app/config.json

# Build
docker build -t myapp:1.0 .
docker build -t myapp:1.0 -f Dockerfile.prod .
docker build --no-cache -t myapp:1.0 .

# Tag and push
docker tag myapp:1.0 registry.example.com/myapp:1.0
docker push registry.example.com/myapp:1.0
```

---

## Dockerfile

```dockerfile
# ── Base image ──────────────────────────────────────────────────────
FROM node:20-alpine

# ── Metadata ────────────────────────────────────────────────────────
LABEL maintainer="team@example.com"
LABEL version="1.0"

# ── Build arguments (available at build time only) ───────────────────
ARG NODE_ENV=production

# ── Environment variables (available at runtime) ─────────────────────
ENV NODE_ENV=${NODE_ENV} \
    PORT=3000 \
    APP_DIR=/app

# ── Working directory ────────────────────────────────────────────────
WORKDIR $APP_DIR

# ── Dependencies first (cached layer) ────────────────────────────────
COPY package*.json ./
RUN npm ci --only=production

# ── Application code ─────────────────────────────────────────────────
COPY . .

# ── Expose port (documentation only — doesn't publish) ───────────────
EXPOSE 3000

# ── Health check ─────────────────────────────────────────────────────
HEALTHCHECK --interval=30s --timeout=3s --start-period=10s --retries=3 \
  CMD wget -qO- http://localhost:3000/health || exit 1

# ── Non-root user ────────────────────────────────────────────────────
RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

# ── Start command ────────────────────────────────────────────────────
CMD ["node", "server.js"]
```

### Instruction Reference

| Instruction | Purpose |
|-------------|---------|
| `FROM` | Base image (must be first) |
| `RUN` | Execute command during build (creates a new layer) |
| `COPY` | Copy files from build context |
| `ADD` | Like COPY but also unpacks archives and fetches URLs (avoid) |
| `WORKDIR` | Set working directory for subsequent instructions |
| `ENV` | Set environment variable |
| `ARG` | Build-time variable (not persisted in image) |
| `EXPOSE` | Document which port the container uses |
| `CMD` | Default command (overridable at `docker run`) |
| `ENTRYPOINT` | Main process (not overridable without `--entrypoint`) |
| `USER` | Run subsequent instructions as this user |
| `HEALTHCHECK` | Command to test container health |
| `VOLUME` | Declare mount point (creates anonymous volume if not mounted) |

### CMD vs ENTRYPOINT

```dockerfile
# CMD: fully replaceable default
CMD ["node", "server.js"]
# docker run myapp python script.py   ← replaces CMD

# ENTRYPOINT: always runs, CMD becomes default args
ENTRYPOINT ["node"]
CMD ["server.js"]
# docker run myapp other.js           ← runs node other.js

# Shell form vs exec form
RUN apt-get update && apt-get install -y curl   # Shell form: /bin/sh -c "..."
RUN ["apt-get", "update"]                        # Exec form: no shell, proper signal handling
```

---

## Image Layers and Caching

Each `RUN`, `COPY`, `ADD` creates a layer. Layers are cached: if nothing before
a step changed, Docker reuses the cached layer.

**Order for best cache utilization**:

```dockerfile
# BAD: copying everything first invalidates cache on any file change
COPY . .
RUN npm ci

# GOOD: copy package files first (changes less often)
COPY package*.json ./
RUN npm ci          # ← only re-runs if package.json changed
COPY . .            # ← code changes don't invalidate npm ci
```

---

## Multi-Stage Builds

Build artifacts in one stage, copy only what's needed to the final image.

```dockerfile
# Stage 1: Build
FROM golang:1.21 AS builder
WORKDIR /build
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o /app/server .

# Stage 2: Run (tiny final image)
FROM scratch
COPY --from=builder /app/server /server
COPY --from=builder /etc/ssl/certs/ca-certificates.crt /etc/ssl/certs/
EXPOSE 8080
ENTRYPOINT ["/server"]
```

**Benefits**: final image has no build tools, Go compiler, or source code.
A Go binary in `scratch` is typically 5-20MB vs 900MB+ for `golang:1.21`.

---

## .dockerignore

```dockerignore
.git
.gitignore
node_modules
npm-debug.log
dist
coverage
*.test.js
.env
.env.*
Dockerfile*
docker-compose*
README.md
.vscode
.idea
```

---

## Volumes

```bash
# Named volume (managed by Docker)
docker volume create pgdata
docker run -v pgdata:/var/lib/postgresql/data postgres:15

# Bind mount (maps host path to container path)
docker run -v /opt/app/config:/app/config:ro myapp

# tmpfs (in-memory, not persisted)
docker run --tmpfs /tmp myapp

# Inspect
docker volume ls
docker volume inspect pgdata
docker volume prune          # Remove unused volumes
```

| Type | Data survives container stop | Data survives container rm | Best for |
|------|-----|-----|---------|
| Named volume | Yes | Yes | Databases, persistent data |
| Bind mount | Yes | Yes | Dev: live code reload |
| tmpfs | Yes | No | Secrets, temp files |
| Anonymous volume | Yes | No | Throw-away temp data |

---

## Networks

```bash
# Create and manage
docker network create mynet
docker network ls
docker network inspect mynet
docker network rm mynet

# Connect containers
docker run --network mynet --name db postgres:15
docker run --network mynet --name app myapp
# Containers on same network can reach each other by name: db, app
```

| Network | Description |
|---------|------------|
| `bridge` | Default; containers on same bridge can communicate |
| `host` | Container shares host network stack (no port mapping needed) |
| `none` | No networking |
| `overlay` | Multi-host networking (Docker Swarm) |
| `macvlan` | Container gets its own MAC address on the physical network |

---

## Docker Compose

```yaml
# docker-compose.yml
version: "3.9"

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
      args:
        NODE_ENV: production
    image: myapp:latest
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=postgresql://user:pass@db:5432/mydb
      - REDIS_URL=redis://cache:6379
    env_file:
      - .env.production
    depends_on:
      db:
        condition: service_healthy
      cache:
        condition: service_started
    restart: unless-stopped
    networks:
      - backend
    deploy:
      resources:
        limits:
          memory: 512M
          cpus: "0.5"

  db:
    image: postgres:15-alpine
    volumes:
      - pgdata:/var/lib/postgresql/data
    environment:
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
      POSTGRES_DB: mydb
    healthcheck:
      test: ["CMD-SHELL", "pg_isready -U user -d mydb"]
      interval: 10s
      timeout: 5s
      retries: 5
    networks:
      - backend

  cache:
    image: redis:7-alpine
    volumes:
      - redisdata:/data
    command: redis-server --appendonly yes
    networks:
      - backend

volumes:
  pgdata:
  redisdata:

networks:
  backend:
    driver: bridge
```

```bash
docker compose up -d           # Start all services in background
docker compose up --build      # Rebuild before starting
docker compose down            # Stop and remove containers
docker compose down -v         # Also remove volumes
docker compose logs -f app     # Follow app logs
docker compose exec app bash   # Shell into running app container
docker compose ps              # Status
docker compose pull            # Pull latest images
docker compose scale app=3     # Scale app to 3 instances
```

---

## Image Tagging Strategy

```bash
# Anti-pattern: latest is a moving target, not reproducible
docker pull myapp:latest

# Good: use immutable tags
myapp:1.2.3                    # Semantic version
myapp:1.2.3-alpine             # Version + variant
myapp:abc1234                  # Git commit SHA
myapp:main-abc1234             # Branch + SHA
```

---

## Container Security

```dockerfile
# Use distroless or minimal base images
FROM gcr.io/distroless/nodejs20-debian12

# Run as non-root
RUN addgroup -S app && adduser -S app -G app
USER app

# Read-only root filesystem
# docker run --read-only myapp
# Only works if the app doesn't write to rootfs
```

```bash
# Scan image for vulnerabilities
trivy image myapp:1.0
docker scout cves myapp:1.0

# Run with security flags
docker run \
  --read-only \
  --no-new-privileges \
  --cap-drop ALL \
  --cap-add NET_BIND_SERVICE \
  --security-opt no-new-privileges:true \
  --user 1000:1000 \
  myapp:1.0
```

---

## Resource Limits

```bash
docker run \
  --memory 512m \           # Memory limit (OOM kill if exceeded)
  --memory-swap 512m \      # Disable swap (same as memory = no swap)
  --cpus 0.5 \              # Half a CPU
  --cpu-shares 512 \        # Relative CPU weight (default 1024)
  --pids-limit 100 \        # Prevent fork bombs
  myapp:1.0
```

---

## Logging Drivers

```bash
# Default: json-file (logs stored at /var/lib/docker/containers/<id>/<id>-json.log)
docker run --log-driver json-file --log-opt max-size=10m --log-opt max-file=3 myapp

# Send to syslog
docker run --log-driver syslog myapp

# Send to AWS CloudWatch
docker run --log-driver awslogs \
  --log-opt awslogs-region=us-east-1 \
  --log-opt awslogs-group=/myapp/production \
  myapp
```

---

## Common Pitfalls

| Pitfall | Fix |
|---------|-----|
| Running as root | Add `USER` directive, use non-root UID |
| Storing secrets in `ENV` | Use Docker secrets, or inject at runtime from Vault/SSM |
| Using `latest` tag | Pin to digest or semantic version |
| Large images | Multi-stage builds, `.dockerignore`, distroless base |
| No `HEALTHCHECK` | Add healthcheck; Kubernetes and Compose depend on it |
| No resource limits | Always set `--memory` and `--cpus` in production |
| Not handling SIGTERM | Use exec form of CMD; handle signals in your app |
| PID 1 zombie problem | Use `tini` or `dumb-init` as init process |
