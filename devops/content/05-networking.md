# Networking & Protocols

Networking knowledge is essential for debugging production issues, designing resilient
architectures, and understanding how every component in a distributed system communicates.
This page covers the protocols, addressing, and tools you need as a DevOps practitioner.

---

## The OSI Model

The OSI model provides a framework for understanding how data travels from one application
to another across a network.

| Layer | Name | Protocols / Examples |
|-------|------|---------------------|
| 7 | Application | HTTP, HTTPS, DNS, FTP, SMTP, SSH |
| 6 | Presentation | TLS/SSL, MIME, compression |
| 5 | Session | RPC, NetBIOS, session establishment |
| 4 | Transport | TCP, UDP |
| 3 | Network | IP, ICMP, routing |
| 2 | Data Link | Ethernet, Wi-Fi, ARP, MAC addresses |
| 1 | Physical | Cables, switches, signals |

**TCP/IP model** (practical 4-layer version):

| TCP/IP Layer | Covers OSI Layers | Examples |
|-------------|-------------------|---------|
| Application | 5-7 | HTTP, DNS, SSH |
| Transport | 4 | TCP, UDP |
| Internet | 3 | IP, ICMP |
| Network Access | 1-2 | Ethernet, Wi-Fi |

---

## IP Addressing

### IPv4

32-bit address written as four octets: `192.168.1.100`

**Private ranges** (RFC 1918 — not routable on public internet):

| Range | CIDR | Typical Use |
|-------|------|------------|
| `10.0.0.0 – 10.255.255.255` | `10.0.0.0/8` | Large corporate networks |
| `172.16.0.0 – 172.31.255.255` | `172.16.0.0/12` | Docker default, mid-size nets |
| `192.168.0.0 – 192.168.255.255` | `192.168.0.0/16` | Home networks |

**CIDR notation**: `192.168.1.0/24` — the `/24` means 24 bits are the network portion.

| CIDR | Subnet Mask | Usable Hosts |
|------|-------------|-------------|
| /30 | 255.255.255.252 | 2 |
| /28 | 255.255.255.240 | 14 |
| /24 | 255.255.255.0 | 254 |
| /16 | 255.255.0.0 | 65,534 |
| /8 | 255.0.0.0 | 16,777,214 |

**Special addresses**:
- `127.0.0.1` / `127.0.0.0/8` — loopback
- `169.254.0.0/16` — link-local (APIPA, used for EC2 instance metadata)
- `0.0.0.0` — all interfaces / default route
- `255.255.255.255` — limited broadcast

### IPv6

128-bit address written in 8 groups of 4 hex digits: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Leading zeros can be omitted: `2001:db8:85a3::8a2e:370:7334`
- `::1` — loopback (equivalent to 127.0.0.1)
- `fe80::/10` — link-local addresses
- Why it matters: IPv4 exhaustion; cloud-native environments often assign IPv6

---

## TCP vs UDP

### TCP (Transmission Control Protocol)

- **Connection-oriented**: 3-way handshake before data exchange
- **Reliable**: acknowledgments, retransmission of lost packets
- **Ordered**: packets delivered in sequence
- **Flow control** and **congestion control**
- Higher overhead due to connection state

**3-way handshake**:
```
Client          Server
  |--SYN--------->|
  |<--SYN-ACK-----|
  |--ACK---------->|
  |  (connected)   |
```

**4-way teardown**:
```
Client          Server
  |--FIN--------->|
  |<--ACK---------|
  |<--FIN---------|
  |--ACK---------->|
  | (TIME_WAIT)    |
```

**Use TCP for**: HTTP/S, SSH, databases, any data where correctness matters.

### UDP (User Datagram Protocol)

- **Connectionless**: no handshake, fire-and-forget
- **Unreliable**: no acknowledgments, no retransmission
- **Unordered**: packets may arrive out of sequence
- Lower overhead, lower latency

**Use UDP for**: DNS, streaming video/audio, gaming, VoIP, QUIC/HTTP3.

---

## DNS

DNS translates human-readable names (`api.example.com`) into IP addresses.

### Resolution Process

```
Browser → Local DNS cache
       → /etc/hosts
       → Recursive resolver (from /etc/resolv.conf or DHCP)
         → Root nameserver (knows TLD servers)
         → TLD nameserver (.com, .org, etc.)
         → Authoritative nameserver (returns A record)
```

### Record Types

| Type | Purpose | Example |
|------|---------|---------|
| `A` | Name → IPv4 | `api.example.com → 1.2.3.4` |
| `AAAA` | Name → IPv6 | `api.example.com → 2001:db8::1` |
| `CNAME` | Alias to another name | `www → example.com` |
| `MX` | Mail server | `example.com → mail.example.com` |
| `TXT` | Arbitrary text | SPF, DKIM, domain verification |
| `NS` | Authoritative nameservers | `example.com NS ns1.cloudflare.com` |
| `SOA` | Zone authority info | Serial, refresh, retry, expire |
| `PTR` | Reverse DNS (IP → name) | `1.2.3.4 → api.example.com` |
| `SRV` | Service location | Used by Kubernetes, SIP, XMPP |

### TTL

Time-to-live: how long resolvers cache the record. Lower TTL means faster propagation
of changes but more DNS queries. Before a migration, lower TTL to 60s; after, raise it back.

### Key Files

```bash
cat /etc/hosts            # Static local overrides (checked before DNS)
cat /etc/resolv.conf      # Nameserver IPs and search domains
cat /etc/nsswitch.conf    # Resolution order: files, dns, mdns
```

---

## HTTP

### Methods

| Method | Semantics | Idempotent | Safe |
|--------|-----------|-----------|------|
| GET | Retrieve resource | Yes | Yes |
| POST | Create / submit | No | No |
| PUT | Replace resource | Yes | No |
| PATCH | Partial update | No | No |
| DELETE | Remove resource | Yes | No |
| HEAD | GET without body | Yes | Yes |
| OPTIONS | Describe capabilities | Yes | Yes |

### Status Codes

| Range | Meaning |
|-------|---------|
| 1xx | Informational (100 Continue, 101 Switching Protocols) |
| 2xx | Success (200 OK, 201 Created, 204 No Content) |
| 3xx | Redirection (301 Moved Permanently, 302 Found, 304 Not Modified) |
| 4xx | Client Error (400 Bad Request, 401 Unauthorized, 403 Forbidden, 404 Not Found, 429 Too Many Requests) |
| 5xx | Server Error (500 Internal Server Error, 502 Bad Gateway, 503 Service Unavailable, 504 Gateway Timeout) |

### HTTP/1.1 vs HTTP/2 vs HTTP/3

| Feature | HTTP/1.1 | HTTP/2 | HTTP/3 |
|---------|---------|--------|--------|
| Transport | TCP | TCP | QUIC (UDP) |
| Multiplexing | No (HOL blocking) | Yes (streams) | Yes (no HOL blocking) |
| Header compression | No | HPACK | QPACK |
| Server push | No | Yes | Yes |
| Connection | Keep-alive | Single connection | Single connection |

---

## HTTPS and TLS

### TLS Handshake (TLS 1.3, simplified)

```
Client                    Server
  |--ClientHello----------->|  (supported ciphers, TLS version)
  |<--ServerHello-----------|  (chosen cipher, certificate)
  |<--Certificate-----------|
  |  [verify cert against CA chain]
  |--ClientKeyExchange----->|
  |  [derive shared secret] |
  |--Finished-------------->|
  |<--Finished--------------|
  |  (encrypted application data)
```

### Certificate Chain

```
Root CA (self-signed, in OS/browser trust store)
  └── Intermediate CA (signed by Root)
        └── Server Certificate (signed by Intermediate)
```

### Key Concepts

- **SNI (Server Name Indication)**: TLS extension that sends the hostname in the ClientHello, allowing a single IP to serve multiple certificates
- **OCSP Stapling**: server attaches a pre-fetched certificate revocation status, avoiding client OCSP lookups
- **mTLS (Mutual TLS)**: both client and server present certificates — used for service-to-service auth in microservices
- **HSTS**: `Strict-Transport-Security` header tells browsers to always use HTTPS

```bash
# Inspect a certificate
openssl s_client -connect api.example.com:443 -servername api.example.com
openssl x509 -in cert.pem -text -noout

# Check expiration
echo | openssl s_client -connect api.example.com:443 2>/dev/null \
  | openssl x509 -noout -dates
```

---

## Well-Known Ports

| Port | Protocol | Service |
|------|---------|---------|
| 21 | TCP | FTP |
| 22 | TCP | SSH |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 80 | TCP | HTTP |
| 443 | TCP | HTTPS |
| 3306 | TCP | MySQL |
| 5432 | TCP | PostgreSQL |
| 6379 | TCP | Redis |
| 8080 | TCP | HTTP (alt) |
| 8443 | TCP | HTTPS (alt) |
| 9090 | TCP | Prometheus |
| 9200 | TCP | Elasticsearch |
| 27017 | TCP | MongoDB |

---

## Networking Commands

```bash
# Connectivity
ping 8.8.8.8                           # ICMP echo
ping -c 4 google.com                   # 4 packets
traceroute google.com                  # Path to host
tracepath google.com                   # Like traceroute, no root required
mtr google.com                         # Real-time traceroute

# DNS
nslookup api.example.com              # Basic DNS query
dig api.example.com                   # Detailed DNS query
dig api.example.com MX                # Query MX records
dig @8.8.8.8 api.example.com         # Query specific nameserver
dig +trace api.example.com           # Show full resolution chain
dig -x 1.2.3.4                       # Reverse DNS lookup
host api.example.com                 # Simple lookup

# Ports and connections
netstat -tlnp                         # Listening TCP ports with PID
ss -tlnp                              # Modern replacement for netstat
lsof -i :8080                         # What's using port 8080
lsof -i tcp:443                       # Connections on port 443
nc -zv host 443                       # Test TCP connectivity (netcat)
nc -l 9999                            # Listen on port 9999 (simple server)

# Network interfaces
ip addr                               # Show interfaces and IPs (modern)
ip addr show eth0                     # Specific interface
ip route                              # Show routing table
ip route get 8.8.8.8                 # Which interface to reach host
ifconfig                              # Old equivalent

# HTTP
curl -v https://api.example.com/health         # Verbose: show headers
curl -s -o /dev/null -w "%{http_code}" URL     # Just status code
curl -X POST -H "Content-Type: application/json" -d '{"key":"val"}' URL
curl --resolve api.example.com:443:1.2.3.4 https://api.example.com  # Override DNS
wget -q -O - http://example.com/file   # Download to stdout

# Packet capture
tcpdump -i eth0 port 80                # Capture HTTP traffic
tcpdump -i eth0 host 1.2.3.4          # Traffic to/from specific host
tcpdump -w capture.pcap                # Write to file (open in Wireshark)
```

---

## Firewalls

### iptables

```bash
# List rules
iptables -L -n -v                      # All chains
iptables -L INPUT -n -v --line-numbers # INPUT chain with line numbers

# Allow incoming SSH
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Allow established connections
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT

# Drop everything else
iptables -A INPUT -j DROP

# Save rules
iptables-save > /etc/iptables/rules.v4
```

### ufw (Uncomplicated Firewall — Ubuntu)

```bash
ufw status                    # Current status
ufw enable                    # Enable firewall
ufw allow 22/tcp              # Allow SSH
ufw allow 80,443/tcp          # Allow HTTP and HTTPS
ufw allow from 10.0.0.0/8    # Allow from subnet
ufw deny 3306/tcp             # Block MySQL from outside
ufw delete allow 80/tcp       # Remove a rule
```

### Cloud Security Groups (AWS example)

Security groups are stateful (return traffic is automatically allowed):

```
Inbound rules:
  Type    | Protocol | Port | Source
  HTTP    | TCP      | 80   | 0.0.0.0/0
  HTTPS   | TCP      | 443  | 0.0.0.0/0
  SSH     | TCP      | 22   | 10.0.0.0/8 (VPN only)
  Custom  | TCP      | 8080 | sg-webapp (only from app tier)
```

---

## NAT

**Source NAT (SNAT / masquerade)**: Changes source IP of outbound packets.
Used when private hosts need to reach the internet through one public IP.

**Destination NAT (DNAT / port forwarding)**: Changes destination IP of inbound packets.
Used to forward port 80 on a public IP to an internal web server.

```bash
# Enable IP forwarding
echo 1 > /proc/sys/net/ipv4/ip_forward

# NAT masquerade (source NAT for internet access)
iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE

# Port forward (DNAT): public:80 → internal:8080
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 10.0.0.5:8080
```

---

## Load Balancing

### L4 vs L7

| | L4 (Transport) | L7 (Application) |
|---|--------------|------------------|
| Sees | IP + port | HTTP headers, paths, cookies |
| Can route by | IP, port | URL path, Host header, request content |
| TLS | Passthrough or terminate | Terminate and re-encrypt |
| Performance | Faster (less processing) | Slower (more processing) |
| Examples | AWS NLB, HAProxy TCP mode | AWS ALB, Nginx, Traefik |

### Algorithms

| Algorithm | How it works | Best for |
|-----------|-------------|---------|
| Round Robin | Cycle through backends equally | Uniform request cost |
| Least Connections | Send to backend with fewest active connections | Variable request cost |
| IP Hash | Hash client IP to pick backend | Session stickiness |
| Weighted | Assign more traffic to more capable backends | Mixed capacity backends |
| Random | Random selection | Simple, stateless services |

### Health Checks

Passive (detect failures from real traffic errors) vs Active (probe endpoints periodically).

```nginx
# Nginx upstream health check
upstream app {
    server 10.0.0.1:8080;
    server 10.0.0.2:8080;
    keepalive 32;
}
```

---

## VPN

| Type | Protocol | Use Case |
|------|---------|---------|
| WireGuard | UDP/51820 | Modern, fast, simple config; preferred for new setups |
| OpenVPN | UDP/TCP | Widely supported, mature |
| IPSec/IKEv2 | UDP/500, 4500 | Site-to-site, mobile clients |
| AWS Site-to-Site VPN | IPSec | Connect on-prem datacenter to AWS VPC |
| AWS Client VPN | OpenVPN | Developers accessing private resources |

---

## CDN Concepts

A CDN (Content Delivery Network) caches content at edge nodes geographically close to users.

- **Edge node / PoP (Point of Presence)**: data center at the "edge" of the internet
- **Origin**: the backend server the CDN fetches from on cache miss
- **Cache-Control**: HTTP header that controls caching behavior (`max-age`, `no-cache`, `no-store`, `s-maxage`)
- **Cache invalidation**: purging cached content when origin changes
- **Cache hit ratio**: fraction of requests served from cache (higher = less load on origin)

```
Cache-Control: public, max-age=3600, s-maxage=86400
# Public: shared caches (CDN) may cache
# max-age=3600: browser cache 1 hour
# s-maxage=86400: CDN cache 24 hours
```

---

## Service Mesh

In microservices, a service mesh moves networking concerns out of application code
into a sidecar proxy (typically Envoy).

- **Sidecar pattern**: a proxy container runs alongside each service pod
- **mTLS between services**: identity-based encryption automatically applied
- **Traffic management**: circuit breaking, retries, timeouts, traffic shifting
- **Observability**: automatic metrics, traces, and access logs per service
- **Examples**: Istio, Linkerd, Consul Connect

---

## Troubleshooting Network Issues

**Systematic approach: work up the OSI stack**

```bash
# 1. Is the host reachable at L3?
ping 10.0.0.5

# 2. Is the route correct?
ip route get 10.0.0.5
traceroute 10.0.0.5

# 3. Is the port open at L4?
nc -zv 10.0.0.5 8080
telnet 10.0.0.5 8080

# 4. Is the service responding at L7?
curl -v http://10.0.0.5:8080/health

# 5. Check DNS
dig api.internal
nslookup api.internal
# Check /etc/resolv.conf for nameserver

# 6. Check firewall / security groups
iptables -L -n -v
# In AWS: check security groups and NACLs

# 7. Check the service itself
ss -tlnp | grep 8080    # Is anything listening on this port?
journalctl -u myservice # Check service logs
```
