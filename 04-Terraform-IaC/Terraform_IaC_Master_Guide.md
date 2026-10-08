# 🏗️ Terraform Infrastructure as Code: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Declarative IaC Principles, HCL Syntax, S3 Remote Backend with DynamoDB State Locking, Terraform 1.5+ Features (`import`, `moved`), AWS Provider v5.x Decoupled Resources, Modules, and Disaster Recovery.

---

## 📑 Table of Contents
- [What is Terraform & Why Do We Use It?](#1-what-is-terraform)
- [How Terraform Works (Desired State Architecture)](#2-how-terraform-works)
- [Terraform Workflow: Init, Plan, Apply, Destroy](#terraform-workflow)
- [State File Governance & S3 + DynamoDB Remote Backend](#state-file-architecture)
- [HCL Syntax & Core Blocks (Providers, Resources, Variables, Outputs)](#hcl-syntax)
- [Modern Terraform 1.5+ Features: import, moved, check](#modern-terraform-features)
- [Modular Architecture Best Practices](#modules-architecture)
- [Production Disaster Recovery & Troubleshooting](#troubleshooting-playbook)

---

SECTION 7: TERRAFORM — COMPLETE GUIDE
Infrastructure as Code (IaC) tool by HashiCorp. Write code to create cloud infrastructure.
1. What is Terraform?
Definition:
Terraform is an open-source Infrastructure as Code (IaC) tool by HashiCorp. It lets you define cloud
infrastructure (EC2, VPC, S3, etc.) in human-readable configuration files and manage it through code.
Why Terraform?
Before Terraform: Click through AWS Console manually to create resources. Hard to reproduce, no
version control, error-prone.
With Terraform: Write code once, run it anywhere. Version controlled, repeatable, consistent.
Key Principle — Desired State:
You declare WHAT you want (desired state). Terraform figures out HOW to create it and ensures the actual state
matches desired state.
You write:  "I want 3 EC2 instances"
Terraform:  Checks current state → Creates what's missing → Reports changes




2. How Terraform Works
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
Terraform Workflow:
Write (.tf files) → Init → Plan → Apply → Destroy
1. Write — create .tf  files declaring resources
2. Init — download provider plugins
3. Plan — preview what will be created/changed/destroyed
4. Apply — actually create the infrastructure
5. Destroy — tear down everything
3. Terraform Files
File Purpose




main.tf Main resource definitions
variables.tf Input variable declarations
outputs.tf Output value definitions
terraform.tfvars Variable values
providers.tf Provider configuration
backend.tf Remote state configuration
terraform.tfstate State file (auto-generated, don't edit)
.terraform/ Downloaded providers (auto-generated)
.terraform.lock.hcl Provider version lock file
4. Terraform Commands
# ── SETUP ──
terraform init                    # initialize — download providers, setup backend
terraform init -upgrade           # upgrade providers to latest versions
# ── PREVIEW ──
terraform plan                    # show what will be created/changed/destroyed
terraform plan -out=tfplan        # save plan to file
terraform plan -var="env=prod"    # pass variable on command line
terraform plan -destroy           # preview destroy
# ── APPLY ──
terraform apply                   # apply changes (asks for confirmation)
terraform apply -auto-approve     # apply without confirmation (CI/CD)
terraform apply tfplan            # apply saved plan
terraform apply -var="env=prod"   # apply with variable
# ── DESTROY ──
terraform destroy                 # destroy all resources (asks confirmation)
terraform destroy -auto-approve   # destroy without confirmation
terraform destroy -target=aws_instance.web  # destroy specific resource
# ── STATE ──
terraform show                    # show current state
terraform state list              # list all resources in state




terraform state show aws_instance.web  # show specific resource state
terraform state rm aws_instance.web    # remove resource from state (without destroyin
terraform state mv aws_instance.old aws_instance.new  # rename in state
terraform refresh                 # sync state with real infrastructure
# ── IMPORT ──
terraform import aws_instance.web i-1234567890  # import existing resource into state
# ── VALIDATE & FORMAT ──
terraform validate                # check configuration syntax
terraform fmt                     # format .tf files
terraform fmt -recursive          # format all files recursively
# ── WORKSPACE ──
terraform workspace list          # list workspaces
terraform workspace new dev       # create new workspace
terraform workspace select prod   # switch workspace
terraform workspace show          # current workspace
terraform workspace delete dev    # delete workspace
# ── OUTPUT ──
terraform output                  # show all outputs
terraform output vpc_id           # show specific output
# ── GRAPH ──
terraform graph                   # generate dependency graph
terraform graph | dot -Tpng > graph.png  # visualize as image
5. Provider Configuration
# providers.tf
terraform {
  required_version = ">= 1.0"
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"        # any 5.x version
    }
    azurerm = {
      source  = "hashicorp/azurerm"
      version = "~> 3.0"
    }
  }




  # Remote state in S3 (for teams)
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}
# AWS Provider
provider "aws" {
  region     = "us-east-1"
  access_key = var.aws_access_key    # from variable
  secret_key = var.aws_secret_key    # from variable
  # Better: use AWS CLI profile or IAM role
  # profile = "default"
}
6. Resource Block — How to Create Infrastructure
Syntax:
resource "provider_resourcetype" "local_name" {
  argument1 = value1
  argument2 = value2
}
Examples:
# EC2 Instance
resource "aws_instance" "web" {
  ami           = "ami-0c55b159cbfafe1f0"
  instance_type = "t2.micro"
  key_name      = "my-key"
  tags = {
    Name = "WebServer"
    Env  = "Production"
  }
}
# S3 Bucket
resource "aws_s3_bucket" "mybucket" {




  bucket = "devops-my-bucket-2024"
  tags = {
    Name = "MyBucket"
  }
}
# Security Group
resource "aws_security_group" "web_sg" {
  name        = "web-sg"
  description = "Allow HTTP and SSH"
  vpc_id      = aws_vpc.main.id    # reference another resource
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
}
7. Creating a VPC — Complete Example
# main.tf — Complete VPC Setup
# ── VPC ──
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  enable_dns_support   = true




  tags = {
    Name = "main-vpc"
  }
}
# ── PUBLIC SUBNET ──
resource "aws_subnet" "public" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "us-east-1a"
  map_public_ip_on_launch = true    # auto-assign public IP
  tags = {
    Name = "public-subnet"
  }
}
# ── PRIVATE SUBNET ──
resource "aws_subnet" "private" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.2.0/24"
  availability_zone = "us-east-1b"
  tags = {
    Name = "private-subnet"
  }
}
# ── INTERNET GATEWAY ──
resource "aws_internet_gateway" "igw" {
  vpc_id = aws_vpc.main.id
  tags = {
    Name = "main-igw"
  }
}
# ── ROUTE TABLE (for public subnet) ──
resource "aws_route_table" "public_rt" {
  vpc_id = aws_vpc.main.id
  route {
    cidr_block = "0.0.0.0/0"
    gateway_id = aws_internet_gateway.igw.id
  }
  tags = {
    Name = "public-rt"




  }
}
# ── ASSOCIATE ROUTE TABLE WITH PUBLIC SUBNET ──
resource "aws_route_table_association" "public_rta" {
  subnet_id      = aws_subnet.public.id
  route_table_id = aws_route_table.public_rt.id
}
# ── SECURITY GROUP ──
resource "aws_security_group" "web_sg" {
  name   = "web-sg"
  vpc_id = aws_vpc.main.id
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
    Name = "web-sg"
  }
}
# ── EC2 INSTANCE IN PUBLIC SUBNET ──
resource "aws_instance" "web" {
  ami                    = var.ami_id
  instance_type          = var.instance_type
  subnet_id              = aws_subnet.public.id
  vpc_security_group_ids = [aws_security_group.web_sg.id]
  key_name               = var.key_name
  tags = {




    Name = "web-server"
  }
}
8. Variables
Why variables?
Avoid hardcoding values. Reuse same code for different environments (dev, staging, prod).
Declaring Variables (variables.tf)
# variables.tf
variable "region" {
  description = "AWS region"
  type        = string
  default     = "us-east-1"
}
variable "instance_type" {
  description = "EC2 instance type"
  type        = string
  default     = "t2.micro"
}
variable "ami_id" {
  description = "AMI ID for EC2"
  type        = string
  # no default — must be provided
}
variable "key_name" {
  description = "SSH key pair name"
  type        = string
}
variable "allowed_ports" {
  description = "List of allowed ports"
  type        = list(number)
  default     = [80, 443, 22]
}
variable "tags" {




  description = "Common tags"
  type        = map(string)
  default = {
    Project     = "MyApp"
    Environment = "dev"
    Owner       = "DevOpsEngineer"
  }
}
variable "db_password" {
  description = "Database password"
  type        = string
  sensitive   = true    # won't show in logs or output
}
Variable Types
Type Example
string "us-east-1"
number 3
bool true
list(string) ["a", "b", "c"]
map(string) {key = "value"}
object complex type
Using Variables (main.tf)
provider "aws" {
  region = var.region
}
resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = var.instance_type
  key_name      = var.key_name
  tags          = var.tags
}




Providing Variable Values
Method 1 — terraform.tfvars file (most common):
# terraform.tfvars
region        = "us-east-1"
instance_type = "t3.medium"
ami_id        = "ami-0c55b159cbfafe1f0"
key_name      = "my-keypair"
db_password   = "supersecret"
Method 2 — Command line:
terraform apply -var="region=us-east-1" -var="instance_type=t3.medium"
Method 3 — Environment variables:
export TF_VAR_region="us-east-1"
export TF_VAR_instance_type="t3.medium"
terraform apply
Method 4 — Different .tfvars for environments:
terraform apply -var-file="dev.tfvars"
terraform apply -var-file="prod.tfvars"
9. Outputs
Why outputs?
Display useful information after apply. Share values between modules.
# outputs.tf
output "vpc_id" {
  description = "ID of the VPC"
  value       = aws_vpc.main.id
}
output "public_subnet_id" {




  description = "ID of public subnet"
  value       = aws_subnet.public.id
}
output "instance_public_ip" {
  description = "Public IP of web server"
  value       = aws_instance.web.public_ip
}
output "instance_dns" {
  description = "Public DNS of web server"
  value       = aws_instance.web.public_dns
}
output "db_password" {
  value     = var.db_password
  sensitive = true            # won't show in terminal
}
terraform output                    # show all outputs
terraform output vpc_id             # show specific output
terraform output -json              # output as JSON
10. Terraform State
What is State?
Terraform keeps a state file ( terraform.tfstate ) that maps your configuration to real infrastructure. It
tracks what exists so Terraform knows what to create, update, or delete.
// terraform.tfstate (simplified)
{
  "resources": [
    {
      "type": "aws_instance",
      "name": "web",
      "instances": [
        {
          "attributes": {
            "id": "i-1234567890",
            "ami": "ami-0c55b159cbfafe1f0",
            "public_ip": "54.123.456.789"
          }




        }
      ]
    }
  ]
}
Local State vs Remote State:
Local State Remote State
Location terraform.tfstate on your machine S3, Terraform Cloud
Team use ❌  Not safe for teams ✅  Multiple people can work
Locking No Yes (prevents conflicts)
Backup Manual Automatic
Remote State in S3 (for teams):
# backend.tf
terraform {
  backend "s3" {
    bucket         = "my-terraform-state-bucket"
    key            = "prod/vpc/terraform.tfstate"
    region         = "us-east-1"
    encrypt        = true
    dynamodb_table = "terraform-locks"    # for state locking
  }
}
11. Workspaces
What is a Workspace?
Workspaces let you manage multiple environments (dev, staging, prod) with the same configuration but
separate state files.
default workspace  → terraform.tfstate
dev workspace      → terraform.tfstate.d/dev/terraform.tfstate
prod workspace     → terraform.tfstate.d/prod/terraform.tfstate




# Workspace commands
terraform workspace list              # list all workspaces
terraform workspace new dev           # create dev workspace
terraform workspace new staging       # create staging workspace
terraform workspace new prod          # create prod workspace
terraform workspace select dev        # switch to dev
terraform workspace show              # current workspace
terraform workspace delete dev        # delete workspace
Using workspace in configuration:
# Use workspace name to set different values
resource "aws_instance" "web" {
  instance_type = terraform.workspace == "prod" ? "t3.large" : "t2.micro"
  tags = {
    Name        = "web-${terraform.workspace}"
    Environment = terraform.workspace
  }
}
# Or use locals
locals {
  instance_type = {
    dev     = "t2.micro"
    staging = "t2.medium"
    prod    = "t3.large"
  }
}
resource "aws_instance" "web" {
  instance_type = local.instance_type[terraform.workspace]
}
Workspace workflow:
# Deploy to dev
terraform workspace select dev
terraform apply -var-file="dev.tfvars"
# Deploy to prod
terraform workspace select prod
terraform apply -var-file="prod.tfvars"




12. Modules
What is a Module?
A module is a reusable package of Terraform code. Instead of rewriting the same VPC code for every project,
write it once as a module and use it everywhere.
Without modules:           With modules:
project1/                  modules/
  main.tf (vpc code)         vpc/
  main.tf (ec2 code)           main.tf
project2/                      variables.tf
  main.tf (vpc code AGAIN)     outputs.tf
  main.tf (ec2 code AGAIN)
                           project1/
                             main.tf (calls vpc module)
                           project2/
                             main.tf (calls vpc module)
Creating a Module
# modules/vpc/main.tf
resource "aws_vpc" "main" {
  cidr_block = var.cidr_block
  tags = {
    Name = var.vpc_name
  }
}
resource "aws_subnet" "public" {
  vpc_id     = aws_vpc.main.id
  cidr_block = var.public_subnet_cidr
}
# modules/vpc/variables.tf
variable "cidr_block" {
  type = string
}
variable "vpc_name" {
  type = string
}
variable "public_subnet_cidr" {




  type = string
}
# modules/vpc/outputs.tf
output "vpc_id" {
  value = aws_vpc.main.id
}
output "subnet_id" {
  value = aws_subnet.public.id
}
Using a Module
# main.tf (in your project)
# Local module
module "vpc" {
  source             = "./modules/vpc"    # path to module
  cidr_block         = "10.0.0.0/16"
  vpc_name           = "prod-vpc"
  public_subnet_cidr = "10.0.1.0/24"
}
# Public registry module (Terraform Registry)
module "vpc" {
  source  = "terraform-aws-modules/vpc/aws"
  version = "5.0.0"
  name = "my-vpc"
  cidr = "10.0.0.0/16"
  azs             = ["us-east-1a", "us-east-1b"]
  private_subnets = ["10.0.1.0/24", "10.0.2.0/24"]
  public_subnets  = ["10.0.4.0/24", "10.0.5.0/24"]
  enable_nat_gateway = true
}
# Use module outputs
resource "aws_instance" "web" {
  subnet_id = module.vpc.subnet_id
}




terraform init      # downloads modules
terraform plan
terraform apply
13. Terraform Meta-Arguments
# count — create multiple resources
resource "aws_instance" "web" {
  count         = 3
  ami           = var.ami_id
  instance_type = "t2.micro"
  tags = {
    Name = "web-${count.index}"    # web-0, web-1, web-2
  }
}
# for_each — create resources from map or set
resource "aws_s3_bucket" "buckets" {
  for_each = toset(["dev", "staging", "prod"])
  bucket   = "myapp-${each.key}"
}
# depends_on — explicit dependency
resource "aws_instance" "web" {
  depends_on = [aws_vpc.main, aws_subnet.public]
  # ...
}
# lifecycle — control resource behavior
resource "aws_instance" "web" {
  # ...
  lifecycle {
    create_before_destroy = true    # create new before destroying old
    prevent_destroy       = true    # never allow destroy (production DBs)
    ignore_changes        = [tags]  # ignore changes to tags
  }
}




14. Data Sources
What is a Data Source?
Data sources let you fetch information about existing infrastructure (not managed by Terraform) and use it in
your config.
# Fetch existing VPC
data "aws_vpc" "existing" {
  id = "vpc-12345678"
}
# Fetch latest Amazon Linux AMI automatically
data "aws_ami" "amazon_linux" {
  most_recent = true
  owners      = ["amazon"]
  filter {
    name   = "name"
    values = ["amzn2-ami-hvm-*-x86_64-gp2"]
  }
}
# Use data source
resource "aws_instance" "web" {
  ami           = data.aws_ami.amazon_linux.id    # always latest AMI
  instance_type = "t2.micro"
  subnet_id     = data.aws_vpc.existing.id
}
15. Locals
What are Locals?
Local values are like variables but computed within the configuration. Used to avoid repetition.
locals {
  env         = terraform.workspace
  app_name    = "myapp"
  common_tags = {
    Project     = local.app_name
    Environment = local.env
    Owner       = "DevOpsEngineer"




    ManagedBy   = "Terraform"
  }
}
resource "aws_instance" "web" {
  ami           = var.ami_id
  instance_type = "t2.micro"
  tags          = local.common_tags    # reuse common tags everywhere
}
resource "aws_s3_bucket" "data" {
  bucket = "${local.app_name}-${local.env}-data"
  tags   = local.common_tags
}
16. Terraform Interview Q&A
Q: What is the difference between terraform plan and terraform apply?
plan  shows what WILL happen (preview). apply  actually makes the changes.
Q: What is terraform state and why is it important?
State file tracks the mapping between your config and real infrastructure. Without it, Terraform doesn't know
what exists and would try to recreate everything.
Q: What happens if you delete the state file?
Terraform loses track of existing resources. Running apply would try to create duplicates. You'd need to import
resources back using terraform import .
Q: What is the difference between count and for_each?
count  creates resources by number. for_each  creates resources from a map or set — better because
resources have meaningful names not just indexes.
Q: How do you manage secrets in Terraform?
Use environment variables (TF_VAR_), mark variables as sensitive=true, use AWS Secrets Manager or HashiCorp
Vault, never hardcode in .tf files.
Q: What is a Terraform module?
Reusable, self-contained package of Terraform code. Like a function in programming — write once, use many
times.
Q: How does Terraform handle dependencies?
Automatically through resource references (implicit dependency). You can also use depends_on  for explicit
dependency.




17. Quick Reference — Terraform
# ESSENTIAL WORKFLOW
terraform init          # always first
terraform fmt           # format code
terraform validate      # check syntax
terraform plan          # preview
terraform apply         # create/update
terraform destroy       # tear down
# STATE
terraform state list
terraform state show <resource>
terraform output
# WORKSPACES
terraform workspace new dev
terraform workspace select prod
terraform workspace list
# IMPORT EXISTING RESOURCE
terraform import aws_instance.web i-1234567890


---

## 🚀 Modern Terraform 1.5+ & AWS Provider v5.x Best Practices

### 1. Decoupled S3 Resources (Provider v5.x)
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
```

### 2. Declarative `import` and `moved` Blocks
```hcl
import {
  to = aws_security_group.app_sg
  id = "sg-0123456789abcdef0"
}

moved {
  from = aws_instance.web
  to   = aws_instance.api_server
}
```
