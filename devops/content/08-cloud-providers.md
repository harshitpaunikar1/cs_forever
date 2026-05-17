# Cloud Providers

Cloud providers supply the compute, storage, networking, and managed services that
most modern systems run on. Understanding at least one major provider deeply — its
IAM model, core services, CLI, and design patterns — is expected of any DevOps
practitioner.

---

## Why Cloud vs On-Premises

| Factor | Cloud | On-Prem |
|--------|-------|---------|
| **Capital cost** | None (pay-as-you-go) | Large upfront hardware investment |
| **Elasticity** | Scale in minutes | Months to procure and rack servers |
| **Managed services** | Databases, queues, ML — fully managed | You maintain everything |
| **Global reach** | Regions on every continent | Expensive to replicate |
| **Availability** | Multi-AZ / multi-region built-in | Complex, costly to achieve |
| **Control** | Less control over hardware | Full hardware control |
| **Compliance** | Data residency choices, certifications | Full control of data location |

---

## Major Providers

| Provider | Strengths | Market Share |
|----------|-----------|-------------|
| **AWS** | Widest service catalog, largest ecosystem | ~32% |
| **Azure** | Enterprise + Microsoft integration, Active Directory | ~22% |
| **GCP** | Kubernetes (they invented it), BigQuery, ML/AI | ~11% |

**Recommendation for beginners**: pick AWS first. Most DevOps roles assume AWS
familiarity, it has the broadest tooling, and the concepts transfer to other providers.

---

## Shared Responsibility Model

Cloud security is a shared responsibility:

```
Provider responsible for:
  - Physical security of datacenters
  - Hypervisor / virtualization layer
  - Managed service software (RDS, Lambda runtime, etc.)
  - Network infrastructure

You responsible for:
  - What's IN your VMs (OS patching, installed software)
  - IAM configuration (who can do what)
  - Data encryption
  - Network configuration (security groups, VPC design)
  - Application code
```

---

## AWS Deep-Dive

### Global Infrastructure

- **Region**: geographic area containing 2+ Availability Zones (e.g., `us-east-1`, `eu-west-1`)
- **Availability Zone (AZ)**: one or more physically separate datacenters in a region (e.g., `us-east-1a`, `us-east-1b`)
- **Edge Location**: CDN PoP for CloudFront, Route 53; there are 400+ globally
- **Local Zone**: compute, storage, database services closer to end users (in cities)

**Best practice**: deploy across 2+ AZs for high availability, consider 2+ regions for disaster recovery.

---

### IAM (Identity and Access Management)

IAM controls who (or what) can do what to which AWS resources.

**Concepts**:

| Entity | What it is |
|--------|-----------|
| **User** | Person with long-term credentials (access key + password) |
| **Group** | Collection of users; policies attached to group apply to all members |
| **Role** | Identity with a trust policy — assumed by services, instances, or cross-account |
| **Policy** | JSON document defining allowed/denied actions on resources |

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
        "s3:GetObject",
        "s3:PutObject"
      ],
      "Resource": "arn:aws:s3:::my-bucket/*"
    }
  ]
}
```

**Policy types**:
- **Managed policies**: standalone, can be attached to multiple identities
- **Inline policies**: embedded in a specific user/group/role
- **Service Control Policies (SCP)**: organization-wide guardrails (AWS Organizations)

**Best practices**:
- Enable MFA for all human users
- Use roles instead of long-term access keys for services
- Principle of least privilege: grant only what is needed
- Rotate credentials regularly; use IAM Access Analyzer to find unused permissions
- Never use root account for day-to-day operations

```bash
# AWS CLI
aws configure                              # Set credentials and region
aws configure --profile prod               # Named profile
aws iam get-user                           # Current user info
aws iam list-attached-user-policies --user-name alice
aws sts assume-role \
  --role-arn arn:aws:iam::123:role/OpsRole \
  --role-session-name mysession
```

---

### EC2 (Elastic Compute Cloud)

Virtual machines in the cloud.

**Instance naming**: `t3.medium`, `c6g.xlarge`, `m5.2xlarge`
- First letter: family (t=burstable, c=compute, m=general, r=memory, p=GPU)
- Number: generation (higher = newer)
- Letter suffix: processor variant (g=Graviton/ARM, a=AMD)
- Size: nano, micro, small, medium, large, xlarge, 2xlarge, etc.

```bash
# Launch instance
aws ec2 run-instances \
  --image-id ami-0c55b159cbfafe1f0 \
  --instance-type t3.micro \
  --key-name my-key \
  --security-group-ids sg-abc123 \
  --subnet-id subnet-abc123 \
  --iam-instance-profile Name=MyInstanceProfile \
  --user-data file://cloud-init.sh \
  --tag-specifications 'ResourceType=instance,Tags=[{Key=Name,Value=webserver}]'

# Common operations
aws ec2 describe-instances --filters "Name=tag:Name,Values=webserver"
aws ec2 stop-instances --instance-ids i-abc123
aws ec2 terminate-instances --instance-ids i-abc123
```

**AMI (Amazon Machine Image)**: snapshot of OS + configuration. Base AMIs from AWS, community, or your own (baked with Packer).

**User data**: script or cloud-init config that runs once when an instance first starts.

**Instance profiles**: attach an IAM role to an EC2 instance — applications on the instance assume this role automatically via the metadata service (`169.254.169.254`).

**Auto Scaling Groups (ASG)**: automatically adjust the number of instances:
- Min/desired/max instance count
- Launch template or launch configuration
- Scaling policies: target tracking (keep CPU at 70%), step scaling, scheduled
- Health checks: EC2 status checks or ELB health checks

---

### VPC (Virtual Private Cloud)

Your private network in AWS.

```
VPC: 10.0.0.0/16
├── us-east-1a
│   ├── Public Subnet: 10.0.1.0/24  (Internet Gateway route)
│   └── Private Subnet: 10.0.2.0/24 (NAT Gateway route)
└── us-east-1b
    ├── Public Subnet: 10.0.3.0/24
    └── Private Subnet: 10.0.4.0/24
```

| Component | Purpose |
|-----------|---------|
| **Internet Gateway** | Allows public subnets to reach the internet |
| **NAT Gateway** | Allows private subnets to reach internet (outbound only) |
| **Route Table** | Rules for routing traffic out of a subnet |
| **Security Group** | Stateful firewall at the instance level |
| **NACL** | Stateless firewall at the subnet level |
| **VPC Peering** | Connect two VPCs privately |
| **Transit Gateway** | Hub-and-spoke connectivity for many VPCs |
| **PrivateLink** | Access AWS services / SaaS without going through internet |

**Security Groups vs NACLs**:

| | Security Group | NACL |
|--|---------------|------|
| Stateful | Yes (return traffic auto-allowed) | No (must allow both directions) |
| Applied to | Instance / ENI | Subnet |
| Default | Deny all inbound, allow all outbound | Allow all |
| Rules | Allow only | Allow and Deny |

---

### S3 (Simple Storage Service)

Object storage. Buckets hold objects (files) with keys (paths).

```bash
# CLI operations
aws s3 ls s3://my-bucket/
aws s3 cp file.txt s3://my-bucket/uploads/
aws s3 sync ./local-dir s3://my-bucket/backups/ --delete
aws s3 presign s3://my-bucket/report.pdf --expires-in 3600

# Storage classes (ordered by cost, lowest access frequency):
# STANDARD           → frequent access
# STANDARD_IA        → infrequent access, same durability
# INTELLIGENT_TIERING → auto-move between tiers
# GLACIER            → archives, 1-12 hour retrieval
# GLACIER DEEP       → lowest cost, 12-48 hour retrieval

# Lifecycle policy: auto-transition to cheaper storage
```

**Key S3 features**:
- 11 nines (99.999999999%) durability
- Versioning: keep all versions of every object
- Replication: cross-region (CRR) or same-region (SRR)
- Bucket policies: resource-based policies (allow public read, restrict to VPC, etc.)
- Server-side encryption: SSE-S3, SSE-KMS, SSE-C
- Block Public Access: account-level setting to prevent accidental public exposure

---

### RDS (Relational Database Service)

Managed relational databases: MySQL, PostgreSQL, MariaDB, Oracle, SQL Server.

**Multi-AZ**: synchronous standby replica in another AZ; automatic failover in ~60-120 seconds.

**Read Replicas**: asynchronous replicas for read scaling; can be promoted to standalone.

**Aurora**: AWS-built MySQL/PostgreSQL-compatible engine — 5x faster than MySQL, 3x faster than PostgreSQL, auto-scales storage, multi-writer option.

**Key settings**:
- Always use Multi-AZ in production
- Enable automated backups (1-35 day retention)
- Enable encryption at rest (KMS)
- Place in private subnets; use security groups to restrict access
- Enable Performance Insights for slow query monitoring

---

### Load Balancers

| Type | OSI Layer | Use Case |
|------|---------|---------|
| **ALB** (Application) | L7 | HTTP/HTTPS routing by path, host, headers |
| **NLB** (Network) | L4 | Ultra-low latency, TCP/UDP, static IPs |
| **GLB** (Gateway) | L3 | Third-party virtual appliances |

ALB features:
- Host-based and path-based routing
- Weighted target groups (canary deployments)
- Lambda target groups
- WebSocket support
- WAF integration

```bash
# Create ALB
aws elbv2 create-load-balancer \
  --name my-alb \
  --type application \
  --subnets subnet-abc subnet-def \
  --security-groups sg-abc
```

---

### CloudWatch

AWS monitoring and observability service.

```bash
# Publish custom metric
aws cloudwatch put-metric-data \
  --namespace MyApp \
  --metric-name OrdersProcessed \
  --value 42 \
  --dimensions Environment=Production

# Get metrics
aws cloudwatch get-metric-statistics \
  --namespace AWS/EC2 \
  --metric-name CPUUtilization \
  --dimensions Name=InstanceId,Value=i-abc \
  --start-time 2024-01-01T00:00:00Z \
  --end-time 2024-01-02T00:00:00Z \
  --period 3600 \
  --statistics Average

# Create alarm
aws cloudwatch put-metric-alarm \
  --alarm-name HighCPU \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --evaluation-periods 2 \
  --period 300 \
  --statistic Average \
  --alarm-actions arn:aws:sns:us-east-1:123:ops-alerts
```

---

### Route 53

AWS DNS service. Routing policies:

| Policy | What it does |
|--------|-------------|
| **Simple** | Returns one or more values for a record |
| **Failover** | Primary/secondary based on health checks |
| **Geolocation** | Route based on user's geographic location |
| **Latency** | Route to region with lowest latency |
| **Weighted** | Split traffic by percentage |
| **Multivalue Answer** | Up to 8 healthy records returned |

---

### Secrets Management

| Service | Use case |
|---------|---------|
| **Secrets Manager** | Database credentials, API keys; automatic rotation; charges per secret |
| **Parameter Store** | Config values; SecureString uses KMS; free tier available |
| **KMS** | Manage encryption keys; used by both above services |

---

## GCP Highlights

| AWS | GCP Equivalent |
|-----|----------------|
| EC2 | Compute Engine |
| EKS | GKE (Google invented Kubernetes) |
| Lambda | Cloud Functions / Cloud Run |
| S3 | Cloud Storage |
| RDS | Cloud SQL / AlloyDB |
| BigQuery | — (unique; serverless data warehouse) |
| IAM | IAM with service accounts |
| CloudWatch | Cloud Monitoring / Cloud Logging |

**GCP differentiators**:
- GKE is the most mature managed Kubernetes
- BigQuery for large-scale analytics (petabyte-scale, serverless)
- Anthos: run GCP services on-prem or other clouds
- Sustained use discounts: automatically apply for long-running VMs

---

## Azure Highlights

| AWS | Azure Equivalent |
|-----|-----------------|
| EC2 | Virtual Machines |
| EKS | AKS (Azure Kubernetes Service) |
| Lambda | Azure Functions |
| S3 | Blob Storage |
| RDS | Azure SQL / Cosmos DB |
| IAM | Azure Active Directory (Entra ID) |
| CloudWatch | Azure Monitor |
| CodePipeline | Azure DevOps Pipelines |

**Azure differentiators**:
- Azure AD (Entra ID): dominant identity provider for enterprises
- Hybrid cloud: strong on-prem + Azure integration
- Microsoft ecosystem: Teams, Office 365, Power Platform integration
- Azure DevOps: end-to-end ALM (repos, pipelines, boards, artifacts)

---

## Cost Optimization

| Strategy | Typical Savings |
|----------|---------------|
| Right-sizing | 20-40% — match instance size to actual workload |
| Reserved Instances / Savings Plans | 30-60% vs on-demand (1 or 3 year commitment) |
| Spot/Preemptible Instances | 60-90% for fault-tolerant, interruptible workloads |
| S3 lifecycle policies | 60-90% — auto-transition to Glacier |
| Auto Scaling | Avoid over-provisioning for peak — scale down at night |
| Delete unused resources | EBS volumes, snapshots, load balancers, idle NAT gateways |

---

## AWS Well-Architected Framework

Six pillars for designing good cloud architectures:

| Pillar | Key Questions |
|--------|-------------|
| **Operational Excellence** | How do you enable, run, and manage workloads? |
| **Security** | How do you protect data and systems? |
| **Reliability** | How do you recover from failures? |
| **Performance Efficiency** | How do you use resources efficiently? |
| **Cost Optimization** | How do you avoid unnecessary expense? |
| **Sustainability** | How do you minimize environmental impact? |

Use the **AWS Well-Architected Tool** in the console to review workloads against these pillars.
