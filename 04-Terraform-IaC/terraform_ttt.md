# 📝 terraform ttt

```text
terraform ttt




/*

# Terraform EC2 & Multi-Stage Notes (Summary Document)

---

## 1. Terraform Workflow

1. `terraform init` → Initialize project & download provider
2. `terraform fmt` → Format code (optional)
3. `terraform validate` → Validate syntax
4. `terraform plan` → Preview changes
5. `terraform apply` → Create resources
6. `terraform destroy` → Delete all created resources

*Tip:* Use `-auto-approve` to skip confirmation.

---




## 2. AWS Credentials for Terraform

**If running locally:**

* `aws configure` → Set access key & secret key
* OR set environment variables:
  export AWS_ACCESS_KEY_ID="YOUR_KEY"
  export AWS_SECRET_ACCESS_KEY="YOUR_SECRET"





**If running on EC2:**

* Attach **IAM Role** to EC2
* Role needs proper permissions (AdministratorAccess for full access)
* Check role with `aws sts get-caller-identity`



---

## 3. IAM Roles & Permissions

| Policy              | Can create EC2 | Can create VPC | Recommended |
| ------------------- | -------------- | -------------- | ----------- |
| AmazonEC2FullAccess | ✔              | ❌              | No          |
| AmazonVPCFullAccess | ❌              | ✔              | No          |
| AdministratorAccess | ✔              | ✔              | ✅           |
| Custom (EC2+VPC)    | ✔              | ✔              | Good        |

---



## 4. AMI IDs

* AMI IDs **are region-specific**
* Amazon Linux 2 examples:

  * ap-south-1: ami-0f5daaa3a7fb3378d
  * eu-north-1: ami-052efd3df9dad4825
* Find AMI IDs:

  1. AWS Console → EC2 → AMIs → Public Images
  2. AWS CLI:
     aws ec2 describe-images --owners amazon --filters "Name=name,Values=amzn2-ami-hvm-*-x86_64-gp2" --region eu-north-1 --query "Images[*].[ImageId,Name]" --output table

---

## 5. Common EC2 Errors & Fixes

1. **InvalidAMIID.NotFound** → AMI does not exist in the region

   * Fix: Use region-specific AMI
2. **Unsupported: requested configuration not supported** → Instance type not available in region

   * Fix: Use supported types (t3.micro, t3a.micro)
3. **No valid credentials** → Terraform cannot authenticate

   * Fix: AWS CLI config, env vars, or IAM role

---

## 6. Minimal Terraform Code for EC2 (eu-north-1)

```hcl
provider "aws" {
  region = "eu-north-1"
}

resource "aws_instance" "T1" {
  ami           = "ami-052efd3df9dad4825"  # Amazon Linux 2
  instance_type = "t3.micro"

  tags = {
    Name = "Test-EC2"
  }
}
```

---

## 7. Delete Terraform Resources

```bash
terraform destroy -auto-approve
rm -rf terraform.tfstate terraform.tfstate.backup .terraform/
```

---

## 8. Multi-Stage Dockerfile (Quick Reference)

```dockerfile
# Stage 1 - Builder
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# Stage 2 - Production
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

*/

```
