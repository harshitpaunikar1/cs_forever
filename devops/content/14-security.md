# Security & Secrets Management

Security is not a phase that happens after development — it is woven into every
step of the DevOps lifecycle. This page covers the tools, practices, and mindset
of DevSecOps: shifting security left so problems are caught before they reach
production.

---

## Security Mindset

**Shift-left**: find and fix security issues as early as possible. The cost to fix a
vulnerability in production is 100× more than finding it in a code review.

**Defense in depth**: assume any single control will fail. Layer security controls
so that compromising one doesn't compromise everything.

**Principle of least privilege**: every user, service, and process should have only
the minimum permissions required to do its job.

**Zero trust**: never assume that being inside the network perimeter makes something
trustworthy. Authenticate and authorize every request.

---

## Threat Modeling (STRIDE)

A lightweight framework for identifying threats:

| Category | Examples |
|----------|---------|
| **S**poofing | Attacker impersonates a user or service |
| **T**ampering | Attacker modifies data in transit or at rest |
| **R**epudiation | User denies performing an action (no audit log) |
| **I**nformation Disclosure | Sensitive data exposed to unauthorized parties |
| **D**enial of Service | Service made unavailable |
| **E**levation of Privilege | User gains higher permissions than intended |

---

## Secret Management

### Never Hardcode Secrets

```bash
# BAD — secret in code
DATABASE_URL = "postgresql://admin:password123@db.internal/mydb"

# BAD — secret in environment (visible in process list, docker inspect)
ENV DB_PASSWORD=mypassword

# GOOD — read at runtime from secrets store
import boto3
client = boto3.client('secretsmanager')
secret = client.get_secret_value(SecretId='prod/myapp/db')
```

**What counts as a secret**: passwords, API keys, private keys, tokens, certificates,
connection strings with credentials.

### HashiCorp Vault

Vault is the most feature-rich secrets management platform.

```bash
# Installation
vault server -dev                    # Dev mode (not for production)

# Authentication
vault login                          # Interactive (token, LDAP, etc.)
vault login -method=aws              # AWS IAM auth

# KV Secrets Engine
vault secrets enable -path=secret kv-v2

vault kv put secret/myapp/db \
  username=admin \
  password=s3cret

vault kv get secret/myapp/db
vault kv get -field=password secret/myapp/db
vault kv list secret/myapp/

# Dynamic secrets: Vault generates short-lived DB credentials
vault secrets enable database
vault write database/config/mydb \
  plugin_name=postgresql-database-plugin \
  connection_url="postgresql://{{username}}:{{password}}@db:5432/mydb" \
  allowed_roles="app-role" \
  username="vault" \
  password="vaultpassword"

vault write database/roles/app-role \
  db_name=mydb \
  creation_statements="CREATE ROLE \"{{name}}\" WITH LOGIN PASSWORD '{{password}}' VALID UNTIL '{{expiration}}'; GRANT SELECT ON ALL TABLES IN SCHEMA public TO \"{{name}}\";" \
  default_ttl="1h" \
  max_ttl="24h"

# Get dynamic credentials (expire after 1h)
vault read database/creds/app-role
```

**Vault in Kubernetes**: use the Vault Agent Injector (sidecar) or the Vault Secrets Operator to inject secrets into pods without the app needing Vault client code.

### AWS Secrets Manager

```bash
# Store a secret
aws secretsmanager create-secret \
  --name prod/myapp/db \
  --secret-string '{"username":"admin","password":"s3cret"}'

# Read
aws secretsmanager get-secret-value --secret-id prod/myapp/db

# Rotation: AWS can auto-rotate RDS credentials
aws secretsmanager rotate-secret \
  --secret-id prod/myapp/db \
  --rotation-rules AutomaticallyAfterDays=30
```

### AWS Parameter Store

```bash
# Cheap alternative for non-sensitive config; SecureString uses KMS
aws ssm put-parameter \
  --name /prod/myapp/db-url \
  --type SecureString \
  --value "postgresql://admin:pass@db/mydb"

aws ssm get-parameter \
  --name /prod/myapp/db-url \
  --with-decryption
```

| | Secrets Manager | Parameter Store |
|--|----------------|-----------------|
| **Cost** | $0.40/secret/month | Free (standard) |
| **Auto-rotation** | Built-in | Manual |
| **Cross-account access** | Yes | Yes (with IAM) |
| **Best for** | Credentials needing rotation | Config + secrets |

### Kubernetes Secrets

```bash
# Create
kubectl create secret generic app-secrets \
  --from-literal=db-password=mysecretpassword

# Base64 is NOT encryption — it's just encoding
echo -n "mysecretpassword" | base64    # bXlzZWNyZXRwYXNzd29yZA==
```

**Encrypt secrets at rest in etcd**:

```yaml
# kube-apiserver flag:
--encryption-provider-config=/etc/kubernetes/encryption-config.yaml

# encryption-config.yaml
apiVersion: apiserver.config.k8s.io/v1
kind: EncryptionConfiguration
resources:
  - resources: [secrets]
    providers:
      - aescbc:
          keys:
            - name: key1
              secret: <base64-encoded-32-byte-key>
      - identity: {}
```

**External Secrets Operator**: sync secrets from Vault/AWS Secrets Manager into Kubernetes Secrets automatically.

---

## Supply Chain Security

### Dependency Scanning

```bash
# npm
npm audit
npm audit --fix

# Python
pip-audit

# Go
govulncheck ./...

# Snyk (multi-language)
snyk test
snyk monitor

# GitHub Dependabot: add .github/dependabot.yml
version: 2
updates:
  - package-ecosystem: npm
    directory: /
    schedule:
      interval: weekly
```

### Container Image Scanning

```bash
# Trivy (most popular, free)
trivy image myapp:1.0
trivy image --exit-code 1 --severity CRITICAL myapp:1.0
trivy fs .                              # Scan filesystem
trivy repo https://github.com/org/repo # Scan git repo

# Grype
grype myapp:1.0
grype dir:.

# Use in CI
- name: Scan image
  uses: aquasecurity/trivy-action@master
  with:
    image-ref: myapp:${{ github.sha }}
    exit-code: 1
    severity: CRITICAL,HIGH
    ignore-unfixed: true
```

### SBOM (Software Bill of Materials)

```bash
# Generate SBOM with Syft
syft myapp:1.0 -o spdx-json > sbom.spdx.json
syft myapp:1.0 -o cyclonedx-json > sbom.cyclonedx.json

# Verify
cosign verify-attestation --type sbom myapp:1.0
```

### Signing Container Images (Sigstore / cosign)

```bash
# Install cosign
brew install cosign

# Keyless signing (uses OIDC, no key management)
cosign sign myregistry.com/myapp:1.0

# Verify
cosign verify myregistry.com/myapp:1.0 \
  --certificate-identity=ci@myorg.github.com \
  --certificate-oidc-issuer=https://token.actions.githubusercontent.com

# In GitHub Actions
- name: Sign image
  uses: sigstore/cosign-installer@v3
  run: |
    cosign sign --yes ${{ env.IMAGE }}:${{ github.sha }}
```

---

## Static Analysis (SAST)

```bash
# Semgrep: fast, powerful, many built-in rules
semgrep --config=auto .
semgrep --config=p/owasp-top-ten .

# In CI
- uses: returntocorp/semgrep-action@v1
  with:
    publishToken: ${{ secrets.SEMGREP_APP_TOKEN }}

# CodeQL (GitHub Advanced Security)
- uses: github/codeql-action/analyze@v2
  with:
    languages: javascript, python

# Language-specific
bandit -r . -ll                 # Python
gosec ./...                     # Go
nodejsscan --directory .        # Node.js
```

### Secrets Scanning

```bash
# detect-secrets (Yelp)
detect-secrets scan > .secrets.baseline
detect-secrets audit .secrets.baseline

# truffleHog
trufflehog git https://github.com/org/repo
trufflehog filesystem .

# GitHub secret scanning: automatic for public repos and GH Advanced Security
# Scans for known secret patterns (AWS keys, GitHub tokens, etc.)

# Pre-commit hook
- repo: https://github.com/Yelp/detect-secrets
  rev: v1.4.0
  hooks:
    - id: detect-secrets
```

---

## Infrastructure Security

### IAM and Least Privilege

```json
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject"
      ],
      "Resource": "arn:aws:s3:::my-bucket/uploads/*",
      "Condition": {
        "StringEquals": {
          "aws:RequestedRegion": "us-east-1"
        }
      }
    }
  ]
}
```

**Tools for analyzing IAM**:
- AWS IAM Access Analyzer: identifies over-permissive policies
- `aws iam get-account-authorization-details` + analysis
- CloudTrail + Athena: query which permissions are actually used

### Encryption

```bash
# Encryption at rest
# S3: enable bucket-level encryption
aws s3api put-bucket-encryption \
  --bucket my-bucket \
  --server-side-encryption-configuration '{"Rules":[{"ApplyServerSideEncryptionByDefault":{"SSEAlgorithm":"aws:kms"}}]}'

# EBS: encrypt volumes
aws ec2 create-volume \
  --encrypted \
  --kms-key-id arn:aws:kms:us-east-1:123:key/abc

# Encryption in transit
# Always use TLS 1.2+ between services
# Never allow plain HTTP internally in production
# Use certificate pinning for sensitive mobile applications
```

### Audit Logging

```bash
# AWS CloudTrail: all API calls
aws cloudtrail create-trail \
  --name my-trail \
  --s3-bucket-name audit-logs \
  --include-global-service-events \
  --is-multi-region-trail \
  --enable-log-file-validation

# VPC Flow Logs: all network traffic
aws ec2 create-flow-logs \
  --resource-type VPC \
  --resource-ids vpc-abc123 \
  --traffic-type ALL \
  --log-destination-type cloud-watch-logs \
  --log-group-name /aws/vpc/flowlogs
```

---

## Container and Kubernetes Security

### Pod Security Standards

```yaml
# Enforce restricted policy at namespace level
apiVersion: v1
kind: Namespace
metadata:
  name: production
  labels:
    pod-security.kubernetes.io/enforce: restricted
    pod-security.kubernetes.io/warn: restricted
```

**Restricted profile requirements**:
- Must drop ALL capabilities
- Must not run as root
- Must not allow privilege escalation
- Must have a read-only root filesystem (recommended)
- Must use `seccompProfile: RuntimeDefault` or `Localhost`

```yaml
# Secure pod spec
spec:
  securityContext:
    runAsNonRoot: true
    runAsUser: 1000
    fsGroup: 1000
    seccompProfile:
      type: RuntimeDefault
  containers:
    - name: app
      securityContext:
        allowPrivilegeEscalation: false
        readOnlyRootFilesystem: true
        capabilities:
          drop: [ALL]
      volumeMounts:
        - name: tmp
          mountPath: /tmp    # writeable temp dir
  volumes:
    - name: tmp
      emptyDir: {}
```

### Falco (Runtime Security)

Falco detects abnormal behavior in containers at runtime:

```yaml
# Example Falco rules
- rule: Shell spawned in a container
  desc: A shell was spawned in a container
  condition: spawned_process and container and shell_procs
  output: "Shell spawned in container (user=%user.name container=%container.id)"
  priority: WARNING

- rule: Write to sensitive directory
  desc: Write to /etc or /usr in a container
  condition: open_write and container and sensitive_dir
  output: "Write to sensitive dir in container (file=%fd.name)"
  priority: ERROR
```

---

## Network Security Policies

```yaml
# Deny all ingress by default, then allow specific traffic
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny
  namespace: production
spec:
  podSelector: {}    # Apply to all pods
  policyTypes:
    - Ingress
    - Egress

---
# Allow specific traffic
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-api-to-db
  namespace: production
spec:
  podSelector:
    matchLabels:
      app: postgres
  ingress:
    - from:
        - podSelector:
            matchLabels:
              app: myapp
      ports:
        - protocol: TCP
          port: 5432
```

---

## Workload Identity

In cloud environments, avoid giving applications long-lived credentials.
Use identity-based auth instead:

```yaml
# AWS IRSA (IAM Roles for Service Accounts) — EKS
apiVersion: v1
kind: ServiceAccount
metadata:
  name: myapp
  namespace: production
  annotations:
    eks.amazonaws.com/role-arn: arn:aws:iam::123456789:role/myapp-role
```

```hcl
# Terraform: IAM role trust policy for IRSA
data "aws_iam_policy_document" "myapp_trust" {
  statement {
    actions = ["sts:AssumeRoleWithWebIdentity"]
    principals {
      type        = "Federated"
      identifiers = [aws_iam_openid_connect_provider.eks.arn]
    }
    condition {
      test     = "StringEquals"
      variable = "${aws_iam_openid_connect_provider.eks.url}:sub"
      values   = ["system:serviceaccount:production:myapp"]
    }
  }
}
```

---

## Incident Response

1. **Detection**: alert fires, anomaly detected, customer reports
2. **Containment**: isolate affected systems, revoke compromised credentials, block IP
3. **Investigation**: determine scope, root cause, attack vector
4. **Eradication**: remove malware, close the vulnerability, rotate all credentials
5. **Recovery**: restore from known-good backups, verify integrity, monitor closely
6. **Lessons learned**: blameless postmortem, update runbooks, fix the root cause

---

## Security Benchmarks

```bash
# CIS Benchmark for Linux
apt-get install -y lynis
lynis audit system

# Docker Bench Security
docker run --rm --net host --pid host --userns host --cap-add audit_control \
  -v /etc:/etc:ro -v /usr/bin/containerd:/usr/bin/containerd:ro \
  -v /var/lib:/var/lib:ro -v /var/run/docker.sock:/var/run/docker.sock:ro \
  docker/docker-bench-security

# Kubernetes CIS Benchmark
kube-bench

# Terraform/IaC scanning
checkov -d .
tfsec .
```
