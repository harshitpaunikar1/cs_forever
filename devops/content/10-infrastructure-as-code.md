# Infrastructure as Code

Infrastructure as Code (IaC) means describing your infrastructure in files that
can be version-controlled, reviewed, and applied automatically — the same way
you treat application code. This makes infrastructure repeatable, auditable, and
less prone to configuration drift.

---

## Why IaC

| Without IaC | With IaC |
|-------------|---------|
| Click through cloud console | Commit a file |
| Undocumented, ad-hoc changes | Every change is a git commit with author and reason |
| "Works in prod, not in dev" | Environments are identical — same code creates both |
| Disaster recovery is scary | Restore entire infrastructure from files in minutes |
| Can't review infrastructure changes | PR reviews for infra changes before they apply |

---

## Declarative vs Imperative

**Declarative** (what): you describe the desired end state; the tool figures out how to get there.
- Terraform, CloudFormation, Pulumi (most modes)
- Tool handles ordering, dependency resolution, retry logic

**Imperative** (how): you write the steps to take.
- Shell scripts, AWS CLI commands
- You handle ordering and idempotency yourself

Modern IaC tools are declarative with escape hatches for imperative needs.

---

## Mutable vs Immutable Infrastructure

**Mutable**: update servers in place. SSH in, patch, upgrade.
- Config drift over time: servers diverge from their definitions
- Hard to reason about state

**Immutable**: never modify running infrastructure. Replace it.
- Build a new AMI or container image, deploy it, terminate the old one
- Every environment is always in a known state
- Enables blue-green deployments trivially

IaC encourages immutable infrastructure: it's easier to `terraform apply` a new instance
than to patch one in place.

---

## Terraform

Terraform is the most widely adopted IaC tool. It uses HCL (HashiCorp Configuration
Language) and supports hundreds of providers (AWS, GCP, Azure, Kubernetes, GitHub...).

### Installation

```bash
brew install terraform           # macOS
# Or download from releases.hashicorp.com

terraform version
tfenv install 1.6.0              # tfenv: manage multiple versions
```

### Core Workflow

```bash
terraform init       # Download providers and modules; initialize backend
terraform validate   # Check config syntax and semantics
terraform fmt        # Auto-format code
terraform plan       # Show what changes will be made (dry run)
terraform apply      # Apply the plan (prompts for confirmation)
terraform destroy    # Destroy all managed resources
```

### HCL Syntax

```hcl
# Provider configuration
terraform {
  required_version = ">= 1.6.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }

  backend "s3" {
    bucket         = "my-terraform-state"
    key            = "prod/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-locks"
    encrypt        = true
  }
}

provider "aws" {
  region = var.aws_region

  default_tags {
    tags = {
      Environment = var.environment
      ManagedBy   = "terraform"
    }
  }
}

# Resource: something to create/manage
resource "aws_vpc" "main" {
  cidr_block           = var.vpc_cidr
  enable_dns_support   = true
  enable_dns_hostnames = true

  tags = {
    Name = "${var.environment}-vpc"
  }
}

# Data source: read existing infrastructure (not managed by this config)
data "aws_ami" "ubuntu" {
  most_recent = true
  owners      = ["099720109477"]  # Canonical

  filter {
    name   = "name"
    values = ["ubuntu/images/hvm-ssd/ubuntu-jammy-22.04-amd64-server-*"]
  }
}

# Resource using outputs from other resources (implicit dependency)
resource "aws_subnet" "public" {
  count             = length(var.availability_zones)
  vpc_id            = aws_vpc.main.id   # <- implicit dependency
  cidr_block        = cidrsubnet(var.vpc_cidr, 8, count.index)
  availability_zone = var.availability_zones[count.index]
  map_public_ip_on_launch = true

  tags = {
    Name = "${var.environment}-public-${count.index + 1}"
  }
}
```

### Variables and Outputs

```hcl
# variables.tf
variable "aws_region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}

variable "environment" {
  description = "Deployment environment"
  type        = string
  validation {
    condition     = contains(["dev", "staging", "prod"], var.environment)
    error_message = "Environment must be dev, staging, or prod."
  }
}

variable "instance_count" {
  type    = number
  default = 2
}

variable "allowed_cidr_blocks" {
  type    = list(string)
  default = []
}

variable "tags" {
  type    = map(string)
  default = {}
}
```

```hcl
# outputs.tf
output "vpc_id" {
  value       = aws_vpc.main.id
  description = "ID of the created VPC"
}

output "public_subnet_ids" {
  value = aws_subnet.public[*].id
}

output "load_balancer_dns" {
  value     = aws_lb.main.dns_name
  sensitive = false
}
```

```hcl
# locals.tf
locals {
  common_tags = merge(var.tags, {
    Environment = var.environment
    Terraform   = "true"
  })

  # Conditional
  instance_type = var.environment == "prod" ? "t3.large" : "t3.micro"
}
```

```bash
# Override variables
terraform apply -var="environment=prod"
terraform apply -var-file="prod.tfvars"

# prod.tfvars
environment   = "prod"
aws_region    = "us-east-1"
instance_count = 4
```

### State

Terraform state tracks what resources it manages. **Never edit state files manually.**

```bash
terraform state list                     # List all resources in state
terraform state show aws_vpc.main        # Inspect a resource
terraform state mv aws_s3_bucket.old aws_s3_bucket.new  # Rename resource
terraform state rm aws_s3_bucket.logs    # Remove from state (doesn't delete resource)
terraform import aws_s3_bucket.logs my-logs-bucket  # Import existing resource
```

**Remote state (S3 backend)**:

```hcl
terraform {
  backend "s3" {
    bucket         = "acme-terraform-state"
    key            = "prod/network/terraform.tfstate"
    region         = "us-east-1"
    dynamodb_table = "terraform-state-locks"  # Prevents concurrent applies
    encrypt        = true
  }
}
```

**State locking**: DynamoDB table prevents two engineers from running `terraform apply` simultaneously.

### Modules

```hcl
# Using a module from the registry
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "5.1.2"

  name = "${var.environment}-vpc"
  cidr = "10.0.0.0/16"

  azs             = ["us-east-1a", "us-east-1b", "us-east-1c"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24", "10.0.3.0/24"]
  public_subnets  = ["10.0.101.0/24", "10.0.102.0/24", "10.0.103.0/24"]

  enable_nat_gateway = true
  single_nat_gateway = var.environment != "prod"  # Save money in non-prod
}

# Access module outputs
resource "aws_instance" "app" {
  subnet_id = module.vpc.private_subnets[0]
}
```

```hcl
# Creating a module: modules/ec2-instance/main.tf
variable "instance_type" {}
variable "ami_id" {}
variable "subnet_id" {}

resource "aws_instance" "this" {
  ami           = var.ami_id
  instance_type = var.instance_type
  subnet_id     = var.subnet_id
}

output "instance_id" {
  value = aws_instance.this.id
}
```

### Meta-Arguments

```hcl
# count: create multiple resources
resource "aws_instance" "web" {
  count         = 3
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"
  tags = {
    Name = "web-${count.index + 1}"
  }
}

# for_each: create from a map or set (better than count for stable identity)
resource "aws_s3_bucket" "env_buckets" {
  for_each = toset(["dev", "staging", "prod"])
  bucket   = "acme-${each.key}-data"
}

# lifecycle: control resource lifecycle
resource "aws_db_instance" "main" {
  # ...
  lifecycle {
    prevent_destroy = true                    # Refuse to destroy in terraform destroy
    create_before_destroy = true              # Create new before destroying old
    ignore_changes = [password, engine_version]  # Ignore external changes to these
  }
}

# depends_on: explicit dependency
resource "aws_ecs_service" "app" {
  depends_on = [aws_iam_role_policy_attachment.ecs_task]
}
```

### Expressions and Functions

```hcl
# Conditionals
instance_type = var.env == "prod" ? "t3.large" : "t3.micro"

# For expressions
public_ips = [for s in aws_instance.web : s.public_ip]
name_map   = {for s in aws_instance.web : s.id => s.tags.Name}

# String interpolation
name = "${var.environment}-${var.app_name}-db"

# Common functions
length(var.subnets)
join(",", var.security_group_ids)
split(",", "a,b,c")
upper(var.environment)
cidrsubnet("10.0.0.0/16", 8, 1)    # "10.0.1.0/24"
lookup(var.instance_types, var.env, "t3.micro")
flatten([[1, 2], [3, 4]])           # [1, 2, 3, 4]
```

---

## Pulumi

Pulumi is IaC using real programming languages: TypeScript, Python, Go, Java, C#.

```typescript
// index.ts
import * as aws from "@pulumi/aws";
import * as pulumi from "@pulumi/pulumi";

const config = new pulumi.Config();
const env = config.require("environment");

const vpc = new aws.ec2.Vpc("main", {
    cidrBlock: "10.0.0.0/16",
    enableDnsHostnames: true,
    tags: { Environment: env },
});

const subnet = new aws.ec2.Subnet("public", {
    vpcId: vpc.id,
    cidrBlock: "10.0.1.0/24",
    mapPublicIpOnLaunch: true,
});

export const vpcId = vpc.id;
export const subnetId = subnet.id;
```

```bash
pulumi new aws-typescript     # Scaffold new project
pulumi up                     # Preview + apply
pulumi preview                # Preview only
pulumi destroy                # Destroy all resources
pulumi stack select prod      # Switch stack (equivalent to Terraform workspace)
```

**When to choose Pulumi over Terraform**: when you want full programming language capabilities (loops over APIs, testing frameworks, TypeScript types).

---

## AWS CloudFormation

AWS-native IaC using JSON or YAML templates.

```yaml
# template.yml
AWSTemplateFormatVersion: '2010-09-09'
Description: Basic EC2 instance

Parameters:
  Environment:
    Type: String
    AllowedValues: [dev, staging, prod]

Conditions:
  IsProd: !Equals [!Ref Environment, prod]

Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: ami-0c55b159cbfafe1f0
      InstanceType: !If [IsProd, t3.large, t3.micro]
      Tags:
        - Key: Environment
          Value: !Ref Environment

Outputs:
  InstanceId:
    Value: !Ref MyInstance
```

```bash
# Deploy
aws cloudformation deploy \
  --template-file template.yml \
  --stack-name myapp-prod \
  --parameter-overrides Environment=prod \
  --capabilities CAPABILITY_IAM

aws cloudformation describe-stacks --stack-name myapp-prod
aws cloudformation describe-stack-events --stack-name myapp-prod
```

---

## Best Practices

### Project Structure

```
infra/
├── modules/
│   ├── vpc/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── ecs-service/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
├── environments/
│   ├── dev/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── terraform.tfvars
│   ├── staging/
│   └── prod/
└── shared/
    └── state-backend/
```

### CI/CD for Terraform

Use **Atlantis** or GitHub Actions to automate Terraform runs:

```yaml
# .github/workflows/terraform.yml
on:
  pull_request:
    paths: ['infra/**']

jobs:
  plan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: hashicorp/setup-terraform@v3
      - run: terraform init
        working-directory: infra/environments/prod
      - run: terraform plan -out=plan.tfplan
        working-directory: infra/environments/prod
      - name: Comment plan on PR
        uses: actions/github-script@v7
        with:
          script: |
            // Post plan output as PR comment
```

### Security Scanning

```bash
# tfsec: static analysis for Terraform
tfsec .

# checkov: security and compliance
checkov -d . --framework terraform

# infracost: cost estimation
infracost breakdown --path .
```

### Golden Rules

1. **One state file per environment per component** — avoid giant monolithic state
2. **Lock provider versions** — `~> 5.0` allows patch upgrades, prevents breaking changes
3. **Remote state with locking** — never use local state in a team
4. **Don't store secrets in Terraform** — use data sources to read from Secrets Manager/Vault
5. **Review plans before applying** — always `terraform plan` and read it
6. **Tag everything** — `Environment`, `Team`, `CostCenter`, `ManagedBy=terraform`
7. **Test with `terraform validate` and linting in CI** — catch errors before review
