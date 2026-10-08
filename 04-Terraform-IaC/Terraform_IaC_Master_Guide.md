# 🏗️ Terraform Infrastructure as Code: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Declarative IaC Principles, HCL Syntax, S3 Remote Backend with DynamoDB State Locking, Terraform 1.5+ Features (`import`, `moved`), AWS Provider v5.x Decoupled Resources, Modules, and Disaster Recovery.

---

## 📑 Table of Contents
- [1. What is Terraform & Core Principles](#1-what-is-terraform)
- [2. How Terraform Works & Architecture](#2-how-terraform-works)
- [3. Core Terraform Files](#3-terraform-files)
- [4. Essential Terraform CLI Commands](#4-terraform-commands)
- [5. Provider & Backend Configuration](#5-provider-configuration)
- [6. Resource Blocks & Syntax](#6-resource-block--how-to-create-infrastructure)
- [7. Complete Production VPC Walkthrough](#7-creating-a-vpc--complete-example)
- [8. Variables: Declaration, Types, & Injection](#8-variables)
- [9. Outputs & Value Sharing](#9-outputs)
- [10. State File Governance & Remote Backend](#10-terraform-state)
- [11. Workspaces & Multi-Environment Strategy](#11-workspaces)
- [12. Reusable Modular Architecture](#12-modules)
- [13. Meta-Arguments (`count`, `for_each`, `depends_on`, `lifecycle`)](#13-terraform-meta-arguments)
- [14. Data Sources](#14-data-sources)
- [15. Local Values (`locals`)](#15-locals)
- [16. High-Frequency Interview Q&A](#16-terraform-interview-qa)
- [17. Quick Reference Cheatsheet](#17-quick-reference--terraform)
- [18. Modern Terraform 1.5+ & AWS Provider v5.x Best Practices](#18-modern-terraform-15--aws-provider-v5x-best-practices)

---

## 1. What is Terraform?

### Core Definition
* **Tool Classification**: Open-source Infrastructure as Code (IaC) tool created by HashiCorp.
* **Declarative Approach**: Define cloud resources (AWS, Azure, GCP) using human-readable HashiCorp Configuration Language (HCL).
* **Automated Lifecycle**: Manages full resource lifecycles—provisioning, modifying, and tearing down infrastructure through code.

### Why DevOps Teams Use Terraform
* **Before Terraform (Manual Provisioning)**:
  * Engineers clicked through web consoles (AWS Management Console, Azure Portal).
  * Configurations were hard to reproduce across environments.
  * Lacked version control, peer reviews, and audit trails.
  * Prone to human error, configuration drift, and orphaned resources.
* **With Terraform (Automated IaC)**:
  * **Write Once, Deploy Anywhere**: Codified configurations deploy consistently across regions and accounts.
  * **Version Controlled**: Code lives in Git with PR reviews, change histories, and automated CI/CD checks.
  * **Repeatability**: Spin up identical Dev, Staging, and Production environments in minutes.
  * **Predictability**: Dry-run preview (`plan`) detects changes before impacting live cloud resources.

### The Desired State Principle
* **Declarative vs Imperative**:
  * You declare **WHAT** end state you desire (e.g., *"I want 3 EC2 instances in a private subnet"*).
  * Terraform computes **HOW** to achieve it and figures out the sequence of API calls.
* **State Reconciliation Engine**:
  * Evaluates current actual state against declared configuration.
  * Identifies missing, modified, or extraneous cloud resources.
  * Generates an execution plan to transition actual state into desired state.

---

## 2. How Terraform Works

### System Architecture
```text
┌─────────────────────────────────────────────────────┐
│                    You (Developer)                   │
│              Write .tf configuration files           │
└────────────────────────┬────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────┐
│                  Terraform Core                      │
│                                                     │
│  ┌─────────────┐      ┌──────────────────────────┐  │
│  │   terraform  │      │    State File            │  │
│  │    plan      │      │  (terraform.tfstate)     │  │
│  │   apply      │      │  tracks what exists      │  │
│  │   destroy    │      └──────────────────────────┘  │
│  └─────────────┘                                    │
└────────────────────────┬────────────────────────────┘
                         │ API calls
          ┌──────────────┼──────────────┐
          ▼              ▼              ▼
      ┌───────┐      ┌───────┐      ┌───────┐
      │  AWS  │      │ Azure │      │  GCP  │
      │Provider│     │Provider│     │Provider│
      └───────┘      └───────┘      └───────┘
```

### 5-Step Core Lifecycle Workflow
* **1. Write**: Author `.tf` files declaring providers, resources, variables, and outputs.
* **2. Init (`terraform init`)**: Initialize working directory, download provider plugins, and configure backend.
* **3. Plan (`terraform plan`)**: Generate and preview execution plan comparing desired state vs actual state.
* **4. Apply (`terraform apply`)**: Execute API calls to build, update, or reconfigure cloud infrastructure.
* **5. Destroy (`terraform destroy`)**: Safely tear down all tracked resources when decommissioning.

---

## 3. Terraform Files

| File Name | Purpose | Git Versioned? |
| :--- | :--- | :--- |
| `main.tf` | Primary resource declarations and core architecture | Yes |
| `variables.tf` | Input variable declarations, data types, and default values | Yes |
| `outputs.tf` | Return values (IDs, public IPs, DNS endpoints) exposed after apply | Yes |
| `terraform.tfvars` | Concrete environment variable assignments (non-sensitive) | Yes (or `.env` ignored) |
| `providers.tf` | Cloud provider requirements, versions, and configurations | Yes |
| `backend.tf` | Remote state configuration (S3 bucket, DynamoDB lock table) | Yes |
| `terraform.tfstate` | Active snapshot of tracked cloud infrastructure | **No** (Store in S3 backend) |
| `.terraform/` | Directory holding downloaded provider plugins and modules | **No** (Ignored) |
| `.terraform.lock.hcl` | Dependency lock file pinning exact provider checksums | **Yes** (Must commit) |

---

## 4. Terraform Commands

### Workspace Setup & Initialization
```bash
# Initialize working directory, download provider binaries, configure state backend
terraform init

# Upgrade provider plugins to the latest compatible versions within constraints
terraform init -upgrade

# Reconfigure backend or change remote backend storage settings
terraform init -reconfigure
```

### Execution Preview & Planning
```bash
# Preview what resources will be created (+), modified (~), or destroyed (-)
terraform plan

# Save the execution plan to a file for deterministic apply in CI/CD pipelines
terraform plan -out=tfplan

# Pass or override an input variable directly via CLI
terraform plan -var="environment=production"

# Preview destruction of all managed resources without deleting them
terraform plan -destroy
```

### Provisioning & Applying Changes
```bash
# Review plan interactively and prompt for manual confirmation ('yes')
terraform apply

# Automatically approve and apply changes without prompt (Used in automated CI/CD)
terraform apply -auto-approve

# Apply a pre-generated, validated plan file deterministically
terraform apply tfplan

# Apply with specific variable overrides
terraform apply -var="instance_type=t3.medium"
```

### Infrastructure Teardown
```bash
# Destroy all resources managed by the current configuration (with confirmation prompt)
terraform destroy

# Force non-interactive destroy in CI/CD teardown jobs
terraform destroy -auto-approve

# Target and destroy only a specific resource without impacting the rest
terraform destroy -target=aws_instance.web
```

### State Management & Inspection
```bash
# Display human-readable view of current state
terraform show

# List all resource identifiers tracked inside the state file
terraform state list

# Inspect all attributes of a single specific tracked resource
terraform state show aws_instance.web

# Remove a resource from state tracking without deleting it from cloud provider
terraform state rm aws_instance.web

# Rename or move a resource address within the state file
terraform state mv aws_instance.old_name aws_instance.new_name

# Sync state file with actual cloud reality to detect drift
terraform refresh
```

### Code Formatting, Validation & Import
```bash
# Verify syntax, attribute validity, and internal consistency of configurations
terraform validate

# Rewrite configurations to follow canonical HCL style guidelines
terraform fmt

# Recursively format all files across subdirectories and modules
terraform fmt -recursive

# Import an existing unmanaged cloud resource into Terraform state
terraform import aws_instance.web i-0123456789abcdef0
```

### Workspaces & Outputs
```bash
# List all existing state workspaces
terraform workspace list

# Create and switch to a new environment workspace
terraform workspace new dev

# Switch active workspace context
terraform workspace select prod

# Print all output values
terraform output

# Retrieve a single output value
terraform output vpc_id -raw

# Export outputs in JSON format for external automation scripts
terraform output -json
```

---

## 5. Provider Configuration

### Declaring Providers & Remote Backend (`providers.tf`)
```hcl
terraform {
  required_version = ">= 1.5.0"

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }

  # Production S3 Remote Backend with DynamoDB State Locking
  backend "s3" {
    bucket         = "devops-terraform-state-bucket"
    key            = "prod/vpc/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-state-locks"
  }
}

# AWS Provider Authentication (Best Practice: Use IAM Roles or AWS CLI Profiles)
provider "aws" {
  region = var.aws_region

  default_tags {
    tags = {
      ManagedBy   = "Terraform"
      Environment = var.environment
      Repository  = "cloud-infrastructure-vault"
    }
  }
}
```

---

## 6. Resource Block — How to Create Infrastructure

### Block Syntax Anatomy
```hcl
resource "<PROVIDER>_<TYPE>" "<LOCAL_NAME>" {
  <ARGUMENT_1> = <VALUE_1>
  <ARGUMENT_2> = <VALUE_2>
}
```

### Common Resource Examples

#### 1. EC2 Compute Instance
```hcl
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"
  key_name      = "devops-keypair"

  tags = {
    Name = "web-production-server"
  }
}
```

#### 2. S3 Storage Bucket
```hcl
resource "aws_s3_bucket" "app_storage" {
  bucket = "enterprise-app-storage-vault"

  tags = {
    Name = "AppStorageBucket"
  }
}
```

#### 3. Security Group with Ingress / Egress
```hcl
resource "aws_security_group" "web_sg" {
  name        = "web-tier-security-group"
  description = "Allow inbound HTTP/HTTPS and SSH; allow all outbound"
  vpc_id      = aws_vpc.main.id

  ingress {
    description = "Allow HTTP"
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "Allow HTTPS"
    from_port   = 443
    to_port     = 443
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    description = "Allow Bastion SSH"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["10.0.0.0/16"]
  }

  egress {
    description = "Allow all outbound traffic"
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }
}
```

---

## 7. Creating a VPC — Complete Example

### End-to-End Modular Network (`main.tf`)
```hcl
# 1. Virtual Private Cloud (VPC)
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true

  tags = {
    Name = "production-vpc"
  }
}

# 2. Public Subnet
resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true

  tags = {
    Name = "public-subnet-1a"
  }
}

# 3. Private Subnet
resource "aws_subnet" "private" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1b"

  tags = {
    Name = "private-subnet-1b"
  }
}

# 4. Internet Gateway (IGW)
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id

  tags = {
    Name = "production-igw"
  }
}

# 5. Public Route Table with Default Route to IGW
resource "aws_route_table" "public_rt" {
  vpc_id = aws_vpc.main.id

  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }

  tags = {
    Name = "public-route-table"
  }
}

# 6. Associate Public Subnet to Public Route Table
resource "aws_route_table_association" "public_rta" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public_rt.id
}

# 7. Security Group for Web Tier
resource "aws_security_group" "web_sg" {
  name        = "web-server-sg"
  description = "Allow HTTP and SSH"
  vpc_id      = aws_vpc.main.id

  ingress {
    from_port   = 80
    to_port     = 80
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  ingress {
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = {
    Name = "web-server-sg"
  }
}

# 8. Web Server EC2 in Public Subnet
resource "aws_instance" "web" {
  ami                    = var.ami_id
  instance_type          = var.instance_type
  subnet_id              = aws_subnet.public.id
  vpc_security_group_ids = [aws_security_group.web_sg.id]
  key_name               = var.key_name

  tags = {
    Name = "production-web-server"
  }
}
```

---

## 8. Variables

### Why Use Variables?
* **Eliminate Hardcoding**: Avoid embedding account IDs, AMI strings, or instance sizing in code.
* **Environment Reusability**: Run identical codebase across Dev, QA, Staging, and Production by swapping variable files.
* **Security**: Pass sensitive secrets (passwords, tokens) securely without committing them to Git.

### Variable Declarations (`variables.tf`)
```hcl
variable "aws_region" {
  description = "Target deployment region"
  type        = string
  default     = "us-east-1"
}

variable "instance_type" {
  description = "EC2 sizing profile"
  type        = string
  default     = "t3.micro"
}

variable "ami_id" {
  description = "Base Amazon Machine Image ID"
  type        = string
  # No default value forces caller to supply it
}

variable "allowed_ports" {
  description = "List of ingress firewall ports"
  type        = list(number)
  default     = [80, 443, 22]
}

variable "common_tags" {
  description = "Mandatory enterprise tags"
  type        = map(string)
  default = {
    Project     = "CloudVault"
    Environment = "Production"
    ManagedBy   = "Terraform"
  }
}

variable "database_password" {
  description = "Master database password"
  type        = string
  sensitive   = true   # Prevents secret from rendering in stdout plans, diffs, and CLI logs
}
```

### Supported Data Types
| Data Type | Example Value | Description |
| :--- | :--- | :--- |
| `string` | `"us-east-1"` | Single alphanumeric text string |
| `number` | `3` or `80.5` | Integer or float numerical value |
| `bool` | `true` or `false` | Boolean toggle flag |
| `list(string)` | `["10.0.1.0/24", "10.0.2.0/24"]` | Ordered list of identical types |
| `map(string)` | `{ env = "prod", tier = "backend" }` | Key-value string dictionary |
| `object(...)` | `{ name = string, port = number }` | Complex heterogeneous schema |

### 4 Ways to Provide Variable Values (Order of Precedence)
* **1. Command-Line Flag (`-var`)**: `terraform apply -var="instance_type=t3.xlarge"` *(Highest precedence)*.
* **2. Environment-Specific Files**: `terraform apply -var-file="prod.tfvars"`.
* **3. `terraform.tfvars` File**: Automatically loaded default values for the project.
* **4. Environment Variables**: `export TF_VAR_instance_type="t3.large"` *(Lowest CLI precedence)*.

---

## 9. Outputs

### Purpose & Benefits
* **Post-Apply Visibility**: Prints critical connection endpoints (VPC IDs, Public IPs, ALB DNS) directly in CLI stdout upon successful provisioning.
* **Inter-Module Integration**: Passes outputs computed by child modules (e.g., `module.vpc.subnet_ids`) as inputs to downstream compute modules.

### Defining Outputs (`outputs.tf`)
```hcl
output "vpc_id" {
  description = "Resource ID of the created VPC"
  value       = aws_vpc.main.id
}

output "web_public_ip" {
  description = "Public IPv4 address of the web server"
  value       = aws_instance.web.public_ip
}

output "database_endpoint" {
  description = "RDS private database connection string"
  value       = aws_db_instance.db.endpoint
  sensitive   = true  # Masks endpoint from plain text terminal output
}
```

---

## 10. Terraform State

### What is the State File?
* **Single Source of Truth**: `terraform.tfstate` maps declared configuration blocks to real-world cloud resource IDs and attributes.
* **Performance Cache**: Stores metadata so Terraform does not have to perform slow live API queries on thousands of cloud resources during every plan.
* **Dependency Tracker**: Records dependency trees so resources are deleted or recreated in the exact correct order.

### Local State vs Remote State Comparison

| Feature | Local State (`terraform.tfstate`) | Remote State (AWS S3 + DynamoDB) |
| :--- | :--- | :--- |
| **Storage Location** | Local developer laptop filesystem | Centralized encrypted AWS S3 bucket |
| **Team Collaboration** | ❌ Prone to collisions, state overwrites, and divergence | ✅ Team shares a single synchronized state |
| **State Locking** | ❌ None (Concurrent applies corrupt the state file) | ✅ DynamoDB locks state during active applies |
| **Encryption** | ❌ Stored unencrypted on developer disk | ✅ Encrypted at rest (AES-256 or AWS KMS) |
| **Backup & Recovery** | ❌ Manual and high risk of catastrophic loss | ✅ S3 Object Versioning enables point-in-time recovery |

### Production Remote Backend (`backend.tf`)
```hcl
terraform {
  backend "s3" {
    bucket         = "devops-terraform-state-bucket"
    key            = "production/infrastructure.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-state-locks"
  }
}
```

---

## 11. Workspaces

### What are Workspaces?
* Separate isolated state instances created from the **same configuration code**.
* Enables quick deployment of parallel environments (`dev`, `staging`, `prod`) without duplicating `.tf` files.

### Workspace CLI Commands
```bash
# Display all existing workspaces (* marks currently active workspace)
terraform workspace list

# Create a brand new workspace and switch context to it
terraform workspace new dev

# Switch between existing workspaces
terraform workspace select prod

# View current active workspace name
terraform workspace show
```

### Dynamic Configuration Using Workspaces
```hcl
locals {
  instance_type_map = {
    dev     = "t3.micro"
    staging = "t3.small"
    prod    = "t3.large"
  }
}

resource "aws_instance" "app" {
  ami           = var.ami_id
  instance_type = local.instance_type_map[terraform.workspace]

  tags = {
    Name        = "app-${terraform.workspace}"
    Environment = terraform.workspace
  }
}
```

---

## 12. Modules

### What is a Module?
* **Reusable Code Container**: Self-contained package of `.tf` files grouped into a directory.
* **DRY Principle (Don't Repeat Yourself)**: Author network or cluster configurations once, then instantiate them across multiple projects and teams.

### Standard Module Directory Structure
```text
modules/
└── vpc/
    ├── main.tf       # Resource definitions for VPC, Subnets, Gateways
    ├── variables.tf  # Input parameters exposed to consumers
    └── outputs.tf    # Values exported back to the calling root module
```

### Consuming a Module in Root `main.tf`
```hcl
module "production_network" {
  source = "./modules/vpc"  # Local module path (or remote Git repository URL)

  vpc_cidr            = "10.100.0.0/16"
  public_subnet_cidr  = "10.100.1.0/24"
  private_subnet_cidr = "10.100.2.0/24"
  environment         = "production"
}

# Consume output exported by the module
resource "aws_instance" "api" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.medium"
  subnet_id     = module.production_network.private_subnet_id
}
```

---

## 13. Terraform Meta-Arguments

### 1. `count`
* Provisions multiple resource copies based on an integer counter.
```hcl
resource "aws_instance" "workers" {
  count         = 3
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"

  tags = {
    Name = "k8s-worker-node-${count.index + 1}"
  }
}
```

### 2. `for_each`
* Iterates over a map or set of strings to provision uniquely keyed resources.
* **Advantage over `count`**: Deleting an item in the middle of a `for_each` list does not force recreation of subsequent resources.
```hcl
resource "aws_s3_bucket" "environment_buckets" {
  for_each = toset(["logs", "backups", "artifacts"])
  bucket   = "enterprise-cloud-vault-${each.key}"
}
```

### 3. `depends_on`
* Enforces explicit resource creation ordering when Terraform cannot infer dependencies automatically.
```hcl
resource "aws_instance" "db" {
  # Forces EC2 creation to wait until S3 bucket and IAM role attachments exist
  depends_on = [aws_s3_bucket.app_storage, aws_iam_role_policy_attachment.db_policy]
}
```

### 4. `lifecycle`
* Customizes how Terraform handles resource updates, recreation, and teardown.
```hcl
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t3.micro"

  lifecycle {
    # 1. Spin up new replacement instance before tearing down existing instance
    create_before_destroy = true

    # 2. Prevent accidental destruction of critical databases or production storage
    prevent_destroy = true

    # 3. Ignore cloud-side changes made by Autoscaling or external tools
    ignore_changes = [tags, ami]
  }
}
```

---

## 14. Data Sources

### Purpose
* Read-only mechanism to query existing cloud resources not managed in the current Terraform configuration.

### Practical Query Examples
```hcl
# 1. Fetch default or pre-existing enterprise VPC ID
data "aws_vpc" "shared_vpc" {
  filter {
    name   = "tag:Name"
    values = ["enterprise-core-vpc"]
  }
}

# 2. Dynamically fetch the latest official Amazon Linux 2 AMI
data "aws_ami" "latest_amazon_linux" {
  most_recent = true
  owners      = ["amazon"]

  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
}

# 3. Deploy EC2 using dynamically discovered AMI and VPC
resource "aws_instance" "app" {
  ami           = data.aws_ami.latest_amazon_linux.id
  instance_type = "t3.micro"
  subnet_id     = tolist(data.aws_subnets.shared_subnets.ids)[0]
}
```

---

## 15. Local Values (`locals`)

### Purpose
* Assign names to computed HCL expressions to avoid repeating complex logic throughout configurations.

### Implementation
```hcl
locals {
  app_name = "taskflow"
  env      = terraform.workspace

  common_tags = {
    Application = local.app_name
    Environment = local.env
    ManagedBy   = "Terraform"
    CostCenter  = "Engineering-DevOps"
  }
}

resource "aws_s3_bucket" "app_data" {
  bucket = "${local.app_name}-${local.env}-app-data-bucket"
  tags   = local.common_tags
}
```

---

## 16. Terraform Interview Q&A

### Q1: What is the exact difference between `terraform plan` and `terraform apply`?
* **`terraform plan`**:
  * Read-only preview operation.
  * Compares desired configuration against state file and live cloud APIs.
  * Shows exact delta (`+` Add, `~` Change in-place, `-` Destroy, `-/+` Destroy and Recreate).
  * Makes zero mutations to real infrastructure.
* **`terraform apply`**:
  * Execution operation.
  * Prompts operator confirmation (unless `-auto-approve` or plan file is passed).
  * Executes concurrent cloud provider API calls to reconcile actual state with desired state.
  * Commits resulting resource IDs and metadata to the state backend.

### Q2: Why is Terraform State important, and what happens if it is deleted?
* **Role**: Acts as the single mapping layer connecting HCL resource blocks (`aws_instance.web`) to real AWS physical IDs (`i-0a1b2c3d4e5f`).
* **Consequences of Deletion**:
  * Terraform forgets all existing infrastructure exists.
  * Running `apply` will attempt to create identical resources from scratch, causing naming collisions and API errors.
* **Recovery Procedure**:
  * Restore `terraform.tfstate` from S3 Object Versioning.
  * If unrecoverable, run `terraform import` on every existing cloud resource to rebuild state tracking.

### Q3: When should you choose `for_each` over `count`?
* **`count`**: Index-based (`[0]`, `[1]`, `[2]`). If item `[0]` is removed, Terraform shifts subsequent indices down and destroys/recreates every resource whose index shifted.
* **`for_each`**: Map/key-based (`["east"]`, `["west"]`). Removing a key only removes that specific instance while leaving all others untouched.
* **Senior Recommendation**: Use `for_each` for all non-trivial collections and multi-resource provisioning.

### Q4: How do you securely handle sensitive secrets in Terraform?
* **Never commit plaintext secrets**: Add `.tfvars` containing secrets to `.gitignore`.
* **Mark variables as sensitive**: Use `sensitive = true` in `variable` and `output` blocks to redact values from console logs.
* **Environment variables**: Pass secrets via `TF_VAR_<name>` in secure CI/CD runners (GitHub Actions Secrets, Jenkins Credentials).
* **Cloud Vaults**: Read secrets dynamically via data sources from AWS Secrets Manager, SSM Parameter Store, or HashiCorp Vault.

### Q5: How does Terraform determine the order of resource creation?
* **Implicit Dependencies**: Terraform analyzes resource attribute references (e.g., `subnet_id = aws_subnet.public.id`) and builds a directed acyclic graph (DAG) automatically.
* **Explicit Dependencies**: Use `depends_on = [aws_resource.target]` when dependencies exist outside of direct attribute references (e.g., waiting for an IAM role policy attachment to propagate before launching an EC2 instance).

---

## 17. Quick Reference — Terraform

### Essential Daily Workflow
* `terraform init` — Initialize directory and download provider plugins.
* `terraform fmt -recursive` — Format all `.tf` files to canonical HCL style.
* `terraform validate` — Validate configuration syntax and schema.
* `terraform plan -out=tfplan` — Generate dry-run preview and write execution artifact.
* `terraform apply tfplan` — Apply validated plan with zero deviation.
* `terraform destroy` — Decommission and delete all tracked resources.

### State & Workspace Quick Commands
* `terraform state list` — List all tracked resources in state.
* `terraform state show <resource>` — Inspect specific resource attributes.
* `terraform output` — View all exported output variables.
* `terraform workspace new <name>` — Create new isolated environment workspace.
* `terraform workspace select <name>` — Switch active workspace context.
* `terraform import <resource> <id>` — Bring unmanaged cloud resource into state.

---

## 18. Modern Terraform 1.5+ & AWS Provider v5.x Best Practices

### 1. Decoupled S3 Resources (Provider v5.x)
* In AWS Provider v5.x, monolithic S3 bucket attributes are deprecated. Separate resources manage versioning, encryption, and public access blocks:
```hcl
resource "aws_s3_bucket" "vault_storage" {
  bucket = "enterprise-cloud-vault-storage"
}

resource "aws_s3_bucket_versioning" "vault_storage_versioning" {
  bucket = aws_s3_bucket.vault_storage.id
  versioning_configuration {
    status = "Enabled"
  }
}

resource "aws_s3_bucket_server_side_encryption_configuration" "vault_storage_crypto" {
  bucket = aws_s3_bucket.vault_storage.id
  rule {
    apply_server_side_encryption_by_default {
      sse_algorithm = "AES256"
    }
  }
}

resource "aws_s3_bucket_public_access_block" "vault_storage_pab" {
  bucket = aws_s3_bucket.vault_storage.id

  block_public_acls       = true
  block_public_policy     = true
  ignore_public_acls      = true
  restrict_public_buckets = true
}
```

### 2. Declarative `import` and `moved` Blocks (Terraform 1.5+)
* Codify resource migrations and refactoring directly in `.tf` files instead of running imperative CLI commands:
```hcl
# Declarative import block (Terraform 1.5+)
import {
  to = aws_security_group.app_sg
  id = "sg-0123456789abcdef0"
}

# Declarative refactoring block (renaming resources without recreation)
moved {
  from = aws_instance.web
  to   = aws_instance.api_server
}
```
