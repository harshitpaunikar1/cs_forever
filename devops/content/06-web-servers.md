# Web Servers & Proxies

Web servers and reverse proxies are the gatekeepers between the internet and your
applications. Nginx, HAProxy, Caddy, and Traefik sit at the edge and handle TLS
termination, request routing, load balancing, and more. This page covers how to
configure and operate them in production.

---

## What a Web Server Does

A web server performs one or more of these roles:

| Role | Description |
|------|-------------|
| **Static file serving** | Serve HTML, CSS, JS, images directly from disk |
| **Reverse proxy** | Forward requests to upstream application servers |
| **TLS termination** | Decrypt HTTPS, proxy HTTP internally |
| **Load balancing** | Distribute traffic across multiple backends |
| **Compression** | gzip/brotli response bodies to reduce bandwidth |
| **Caching** | Cache upstream responses, serve repeated requests faster |
| **Rate limiting** | Throttle clients sending too many requests |
| **Request routing** | Route based on Host header, URL path, method |

---

## Nginx

Nginx uses an event-driven, non-blocking architecture. A master process manages
worker processes, each handling thousands of concurrent connections.

### Installation

```bash
# Debian/Ubuntu
apt-get install nginx

# RHEL/CentOS
yum install nginx

# Start and enable
systemctl enable --now nginx
nginx -t            # Test config syntax
nginx -s reload     # Reload without downtime
```

### Config Structure

```
/etc/nginx/
├── nginx.conf           # Main config
├── conf.d/              # Drop-in server blocks (included by nginx.conf)
│   └── app.conf
├── sites-available/     # Debian-style (symlinked to sites-enabled)
└── sites-enabled/
```

```nginx
# /etc/nginx/nginx.conf
worker_processes auto;   # Number of worker processes (auto = CPU count)
worker_connections 1024; # Max connections per worker

events {}

http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile      on;
    keepalive_timeout 65;
    gzip on;

    include /etc/nginx/conf.d/*.conf;
}
```

### Server Blocks (Virtual Hosts)

```nginx
# /etc/nginx/conf.d/myapp.conf
server {
    listen 80;
    server_name example.com www.example.com;

    # Redirect HTTP to HTTPS
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    server_name example.com;

    ssl_certificate     /etc/letsencrypt/live/example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/example.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;

    # Security headers
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    add_header X-Content-Type-Options nosniff;
    add_header X-Frame-Options SAMEORIGIN;
    add_header X-XSS-Protection "1; mode=block";

    # Proxy to Node.js app
    location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_cache_bypass $http_upgrade;
        proxy_read_timeout 60s;
        proxy_connect_timeout 10s;
    }

    # Static files — bypass the app
    location /static/ {
        alias /var/www/myapp/static/;
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # Health check endpoint
    location /health {
        access_log off;
        return 200 "OK\n";
        add_header Content-Type text/plain;
    }
}
```

### Upstream and Load Balancing

```nginx
http {
    upstream app_servers {
        least_conn;                    # Algorithm (default: round_robin)
        server 10.0.0.1:8080 weight=3;
        server 10.0.0.2:8080 weight=1;
        server 10.0.0.3:8080 backup;   # Only used if others are down
        keepalive 32;                  # Keep 32 connections per worker
    }

    server {
        location / {
            proxy_pass http://app_servers;
        }
    }
}
```

### Rate Limiting

```nginx
http {
    # Define a zone: 10MB memory to track IPs, 10 req/sec limit
    limit_req_zone $binary_remote_addr zone=api_limit:10m rate=10r/s;
    limit_conn_zone $binary_remote_addr zone=conn_limit:10m;

    server {
        location /api/ {
            limit_req zone=api_limit burst=20 nodelay;
            limit_conn conn_limit 10;
        }
    }
}
```

### Gzip Compression

```nginx
http {
    gzip on;
    gzip_vary on;
    gzip_min_length 1024;
    gzip_comp_level 6;
    gzip_types
        text/plain text/css text/javascript
        application/json application/javascript
        application/xml image/svg+xml;
}
```

---

## Apache httpd

Apache is the older, more feature-rich alternative. Uses MPM (Multi-Processing Module):

| MPM | Model | Best for |
|-----|-------|---------|
| prefork | Process-per-connection | PHP with non-thread-safe modules |
| worker | Thread-per-connection | Moderate concurrency |
| event | Event-driven (like Nginx) | High concurrency |

```apache
# VirtualHost configuration
<VirtualHost *:443>
    ServerName example.com
    DocumentRoot /var/www/html

    SSLEngine on
    SSLCertificateFile /etc/ssl/certs/example.crt
    SSLCertificateKeyFile /etc/ssl/private/example.key

    # Reverse proxy
    ProxyPreserveHost On
    ProxyPass / http://localhost:3000/
    ProxyPassReverse / http://localhost:3000/

    # Security
    Header always set X-Frame-Options SAMEORIGIN
    ServerTokens Prod         # Hide Apache version
    ServerSignature Off
</VirtualHost>
```

```bash
a2ensite example.com.conf     # Enable site
a2dissite 000-default.conf    # Disable default
a2enmod ssl proxy proxy_http  # Enable modules
apachectl configtest          # Test config
apachectl graceful            # Reload without dropping connections
```

---

## HAProxy

HAProxy excels at high-performance TCP and HTTP load balancing. Common in
database proxying (MySQL, PostgreSQL) and high-traffic frontends.

```haproxy
# /etc/haproxy/haproxy.cfg

global
    log stdout format raw local0
    maxconn 50000
    stats socket /run/haproxy/admin.sock mode 660 level admin

defaults
    log global
    mode http
    option httplog
    option dontlognull
    option forwardfor
    option http-server-close
    timeout connect 5s
    timeout client  30s
    timeout server  30s

# Stats dashboard
frontend stats
    bind *:8404
    stats enable
    stats uri /stats
    stats refresh 10s
    stats auth admin:password

# HTTP frontend
frontend http_front
    bind *:80
    redirect scheme https code 301 if !{ ssl_fc }

frontend https_front
    bind *:443 ssl crt /etc/haproxy/certs/
    default_backend app_back

    # Route by path
    acl is_api path_beg /api/
    use_backend api_back if is_api

backend app_back
    balance roundrobin
    option httpchk GET /health HTTP/1.1\r\nHost:\ localhost
    http-check expect status 200
    server web1 10.0.0.1:8080 check inter 2s
    server web2 10.0.0.2:8080 check inter 2s

backend api_back
    balance leastconn
    server api1 10.0.0.3:8080 check
    server api2 10.0.0.4:8080 check
```

---

## Caddy

Caddy's killer feature is automatic HTTPS via Let's Encrypt with zero configuration.

```caddyfile
# Caddyfile

# Automatic HTTPS for all named hosts
example.com {
    reverse_proxy localhost:3000

    # File server
    file_server /static/* {
        root /var/www
    }

    # Rate limiting (requires caddy-ratelimit plugin)
    rate_limit {
        zone dynamic {
            key {remote_host}
            events 100
            window 1m
        }
    }
}

# Multiple sites
api.example.com {
    reverse_proxy localhost:8080 localhost:8081 {
        lb_policy least_conn
        health_uri /health
        health_interval 10s
    }
}
```

```bash
caddy run --config /etc/caddy/Caddyfile   # Run in foreground
caddy reload                               # Reload config
caddy validate --config /etc/caddy/Caddyfile
```

---

## Traefik

Traefik integrates with Docker and Kubernetes via labels/annotations — it discovers
services automatically.

```yaml
# docker-compose.yml with Traefik
version: "3"
services:
  traefik:
    image: traefik:v3.0
    command:
      - "--api.insecure=true"
      - "--providers.docker=true"
      - "--entrypoints.web.address=:80"
      - "--entrypoints.websecure.address=:443"
      - "--certificatesresolvers.letsencrypt.acme.email=admin@example.com"
      - "--certificatesresolvers.letsencrypt.acme.storage=/acme.json"
      - "--certificatesresolvers.letsencrypt.acme.httpchallenge.entrypoint=web"
    ports:
      - "80:80"
      - "443:443"
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock:ro
      - ./acme.json:/acme.json

  app:
    image: myapp:latest
    labels:
      - "traefik.enable=true"
      - "traefik.http.routers.app.rule=Host(`example.com`)"
      - "traefik.http.routers.app.entrypoints=websecure"
      - "traefik.http.routers.app.tls.certresolver=letsencrypt"
      - "traefik.http.services.app.loadbalancer.server.port=3000"
      # Rate limiting middleware
      - "traefik.http.middlewares.ratelimit.ratelimit.average=100"
      - "traefik.http.routers.app.middlewares=ratelimit"
```

---

## TLS Certificate Management

### Let's Encrypt with Certbot

```bash
# Install Certbot
apt-get install certbot python3-certbot-nginx

# Obtain and install certificate
certbot --nginx -d example.com -d www.example.com

# Standalone (no web server running)
certbot certonly --standalone -d example.com

# Wildcard (requires DNS challenge)
certbot certonly --manual --preferred-challenges=dns -d "*.example.com"

# Auto-renew (certbot installs a systemd timer)
systemctl status certbot.timer
certbot renew --dry-run    # Test renewal

# Certificate locations
ls /etc/letsencrypt/live/example.com/
# cert.pem      — server certificate
# chain.pem     — intermediate chain
# fullchain.pem — cert + chain (use this for nginx ssl_certificate)
# privkey.pem   — private key
```

### TLS Best Practices

```nginx
# Strong TLS configuration
ssl_protocols TLSv1.2 TLSv1.3;
ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384;
ssl_prefer_server_ciphers off;    # TLS 1.3 chooses cipher; for 1.2 use on
ssl_session_timeout 1d;
ssl_session_cache shared:MozSSL:10m;
ssl_session_tickets off;

# OCSP stapling
ssl_stapling on;
ssl_stapling_verify on;
resolver 8.8.8.8 8.8.4.4 valid=300s;
```

---

## Security Hardening

```nginx
# Hide Nginx version
server_tokens off;

# Prevent clickjacking
add_header X-Frame-Options SAMEORIGIN always;

# Prevent MIME type sniffing
add_header X-Content-Type-Options nosniff always;

# Content Security Policy
add_header Content-Security-Policy "default-src 'self'; script-src 'self' 'unsafe-inline'; style-src 'self' 'unsafe-inline'" always;

# HSTS (only add after HTTPS is confirmed working)
add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload" always;

# Limit request methods
if ($request_method !~ ^(GET|HEAD|POST|PUT|DELETE|OPTIONS)$) {
    return 405;
}

# Block common vulnerability scanners
if ($http_user_agent ~* (nikto|scanner|sqlmap|nmap)) {
    return 444;  # Close connection without response
}

# Limit request size
client_max_body_size 10M;
```

---

## Logging

```nginx
# Custom log format with response time and upstream
log_format detailed '$remote_addr - $remote_user [$time_local] '
                    '"$request" $status $body_bytes_sent '
                    '"$http_referer" "$http_user_agent" '
                    '$request_time $upstream_response_time';

access_log /var/log/nginx/access.log detailed;
error_log /var/log/nginx/error.log warn;
```

```bash
# Analyze access logs
awk '{print $1}' access.log | sort | uniq -c | sort -rn | head -10  # Top IPs
awk '{print $9}' access.log | sort | uniq -c | sort -rn             # Status codes
awk '$9 == "500" {print $7}' access.log | sort | uniq -c            # URLs with 500s
```

---

## Nginx Full Example: Node.js App with HTTPS

```nginx
# /etc/nginx/conf.d/nodeapp.conf

upstream node_app {
    least_conn;
    server 127.0.0.1:3000;
    server 127.0.0.1:3001;
    keepalive 16;
}

server {
    listen 80 default_server;
    server_name _;
    return 301 https://$host$request_uri;
}

server {
    listen 443 ssl http2;
    server_name myapp.example.com;

    ssl_certificate /etc/letsencrypt/live/myapp.example.com/fullchain.pem;
    ssl_certificate_key /etc/letsencrypt/live/myapp.example.com/privkey.pem;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:10m;

    # Headers
    server_tokens off;
    add_header Strict-Transport-Security "max-age=31536000" always;
    add_header X-Frame-Options SAMEORIGIN always;
    add_header X-Content-Type-Options nosniff always;

    # Compression
    gzip on;
    gzip_types text/plain application/json application/javascript text/css;
    gzip_min_length 1024;

    # Rate limiting
    limit_req_zone $binary_remote_addr zone=global:10m rate=30r/s;
    limit_req zone=global burst=50 nodelay;

    # Static files
    location /assets/ {
        root /opt/myapp/public;
        expires 1y;
        add_header Cache-Control "public, immutable";
        access_log off;
    }

    # App
    location / {
        proxy_pass http://node_app;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto https;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        proxy_read_timeout 60s;
        proxy_send_timeout 60s;
        proxy_buffering off;
    }

    location /health {
        proxy_pass http://node_app;
        access_log off;
    }
}
```
