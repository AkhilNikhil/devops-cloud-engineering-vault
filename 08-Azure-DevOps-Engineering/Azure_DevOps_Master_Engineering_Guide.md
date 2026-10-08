# 🔷 Azure DevOps Engineering: The Definitive Master Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers The 5 Core Azure DevOps Services (Boards, Repos, Pipelines, Test Plans, Artifacts), YAML Multi-Stage Pipelines, Microsoft-Hosted vs Self-Hosted Agents, Service Connections (ARM / Workload Identity), Branch Policies & Pull Request Governance, Variable Groups & Key Vault Integration, Environment Approvals & Gates, and Scenario Interview Playbooks.

---

## 📑 Table of Contents
- [1. Azure DevOps Platform Architecture & Organization Hierarchy](#1-azure-devops-platform-architecture--organization-hierarchy)
- [2. Azure Boards: Agile Project & Work Item Management](#2-azure-boards-agile-project--work-item-management)
- [3. Azure Repos & Enterprise Branch Governance](#3-azure-repos--enterprise-branch-governance)
- [4. Multi-Stage YAML Pipelines Architecture](#4-multi-stage-yaml-pipelines-architecture)
- [5. Complete Production Azure Pipelines YAML Blueprint](#5-complete-production-azure-pipelines-yaml-blueprint)
- [6. Pipeline Agents: Microsoft-Hosted vs Self-Hosted](#6-pipeline-agents-microsoft-hosted-vs-self-hosted)
- [7. Service Connections & Cloud Authentication](#7-service-connections--cloud-authentication)
- [8. Variable Groups & Azure Key Vault Secrets Integration](#8-variable-groups--azure-key-vault-secrets-integration)
- [9. Environments, Approval Gates, & Deployment Strategies](#9-environments-approval-gates--deployment-strategies)
- [10. Azure Artifacts: Package Feeds & Versioning](#10-azure-artifacts-package-feeds--versioning)
- [11. Senior DevOps Scenario Interview Q&A](#11-senior-devops-scenario-interview-qa)

---

## 1. Azure DevOps Platform Architecture & Organization Hierarchy

### Organizational Structure
```text
┌─────────────────────────────────────────────────────────────┐
│                 Azure DevOps Organization                   │
│               (e.g., dev.azure.com/my-org)                  │
└──────────────────────────────┬──────────────────────────────┘
                               │
       ┌───────────────────────┴───────────────────────┐
       ▼                                               ▼
┌──────────────────────────────┐       ┌──────────────────────────────┐
│       Project: E-Commerce    │       │     Project: Infrastructure  │
│                              │       │                              │
│   • Azure Boards             │       │   • Azure Boards             │
│   • Azure Repos              │       │   • Azure Repos              │
│   • Azure Pipelines          │       │   • Azure Pipelines          │
│   • Azure Test Plans         │       │   • Azure Test Plans         │
│   • Azure Artifacts          │       │   • Azure Artifacts          │
└──────────────────────────────┘       └──────────────────────────────┘
```

### The 5 Core Azure DevOps Services
* **1. Azure Boards**: Agile work tracking, Kanban boards, sprint backlogs, team capacity planning, and custom reporting queries.
* **2. Azure Repos**: Unlimited cloud-hosted private Git repositories with enterprise pull request review policies and branch locks.
* **3. Azure Pipelines**: Language-agnostic, cloud-native CI/CD supporting multi-stage YAML pipelines running on Linux, macOS, and Windows.
* **4. Azure Test Plans**: Manual test case management, exploratory testing browser extensions, and automated test reporting suites.
* **5. Azure Artifacts**: Secure package feeds for hosting and sharing NuGet, npm, Maven, and Python packages with upstream caching.

---

## 2. Azure Boards: Agile Project & Work Item Management

### Work Item Hierarchy (Agile & Scrum Process)
* **Epic**: High-level strategic initiative spanning multiple sprints or quarters (e.g., *"Customer Payment Gateway Modernization"*).
* **Feature**: Significant business deliverable nested under an Epic (e.g., *"Apple Pay & Google Pay Integration"*).
* **User Story / Product Backlog Item (PBI)**: End-user capability delivering discrete value (e.g., *"As a shopper, I want to checkout via Apple Pay"*).
* **Task**: Technical work item completed by an individual engineer within a single day (e.g., *"Implement Apple Pay webhook listener endpoint"*).
* **Bug**: Defect tracking unexpected application behavior with reproduction steps and severity ratings.

---

## 3. Azure Repos & Enterprise Branch Governance

### Branch Protection Policies
* In enterprise settings, **direct commits to `main` and `release/*` are strictly blocked**.
* Changes must merge via Pull Requests satisfying mandatory gates:
  * **Minimum Number of Reviewers**: Require at least 2 senior engineers to approve.
  * **Linked Work Items**: Mandatory association with an active Azure Boards User Story/Task.
  * **Build Validation Pipeline**: PR branch must successfully compile and pass unit tests before merge button is enabled.
  * **Comment Resolution**: All reviewer comments and discussion threads must be explicitly resolved.
  * **Reset Code Approvals**: Automatically revokes approvals if new commits are pushed to the PR branch.

### Standard Pull Request Template (`.azuredevops/pull_request_template.md`)
```markdown
## Description of Changes
- Implemented JWT token verification middleware.

## Linked Work Item
- Fixes AB#1234

## Verification Checklist
- [x] Unit tests pass locally.
- [x] Code conforms to project linting standards.
- [x] No plaintext credentials or secrets introduced.
```

---

## 4. Multi-Stage YAML Pipelines Architecture

### Pipeline Hierarchy: Stages -> Jobs -> Steps
```text
┌─────────────────────────────────────────────────────────────┐
│                 Pipeline (root azure-pipelines.yml)         │
│                                                             │
│   ┌─────────────────────────────────────────────────────┐   │
│   │ Stage 1: Build & Test (Runs on Linux agent)         │   │
│   │   Job 1: Unit Tests & Static Analysis               │   │
│   │     Step 1: Checkout                                │   │
│   │     Step 2: npm test                                │   │
│   │   Job 2: Build & Push Docker Image                  │   │
│   │     Step 1: Docker Build & Push to ACR              │   │
│   └──────────────────────────┬──────────────────────────┘   │
│                              │ dependsOn: Build (Success)   │
│                              ▼                              │
│   ┌─────────────────────────────────────────────────────┐   │
│   │ Stage 2: Deploy to Production (Deployment Job)      │   │
│   │   Environment: 'production' (Requires Manual Gate)   │   │
│   │   Step 1: Download Artifact                         │   │
│   │   Step 2: Deploy to Azure Kubernetes Service (AKS)  │   │
│   └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

---

## 5. Complete Production Azure Pipelines YAML Blueprint

```yaml
trigger:
  branches:
    include:
      - main
      - release/*
  paths:
    exclude:
      - README.md
      - docs/*

pr:
  branches:
    include:
      - main

pool:
  vmImage: 'ubuntu-22.04'

variables:
  - group: Production-Secrets-Vault
  - name: dockerRegistryServiceConnection
    value: 'Acr-Service-Connection'
  - name: imageRepository
    value: 'taskflow-backend'
  - name: containerRegistry
    value: 'myenterpriseacr.azurecr.io'
  - name: tag
    value: '$(Build.BuildId)-$(Build.SourceVersion)'

stages:
  # ==========================================
  # STAGE 1: Build, Test, & Containerize
  # ==========================================
  - stage: BuildAndTest
    displayName: 'Build, Test, and Scan'
    jobs:
      - job: TestAndScan
        displayName: 'Unit Tests & Quality Gate'
        steps:
          - task: NodeTool@0
            inputs:
              versionSpec: '18.x'
            displayName: 'Install Node.js'

          - script: |
              npm ci
              npm run test -- --coverage
            displayName: 'Run Automated Tests'

          - task: Docker@2
            displayName: 'Build & Push Docker Image'
            inputs:
              command: buildAndPush
              containerRegistry: $(dockerRegistryServiceConnection)
              repository: $(imageRepository)
              dockerfile: '$(Build.SourcesDirectory)/Dockerfile'
              tags: |
                $(tag)
                latest

  # ==========================================
  # STAGE 2: Deploy to Production
  # ==========================================
  - stage: DeployProd
    displayName: 'Deploy to Production AKS'
    dependsOn: BuildAndTest
    condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
    jobs:
      - deployment: DeployAKS
        displayName: 'Deploy to Azure Kubernetes'
        environment: 'production-k8s-cluster' # Protected Environment with Approval Gate
        strategy:
          runOnce:
            deploy:
              steps:
                - task: KubernetesManifest@0
                  displayName: 'Deploy Kubernetes Manifests'
                  inputs:
                    action: deploy
                    kubernetesServiceConnection: 'Aks-Production-Connection'
                    namespace: 'production'
                    manifests: |
                      $(Pipeline.Workspace)/manifests/deployment.yaml
                      $(Pipeline.Workspace)/manifests/service.yaml
                    containers: |
                      $(containerRegistry)/$(imageRepository):$(tag)
```

---

## 6. Pipeline Agents: Microsoft-Hosted vs Self-Hosted

### Comparison Matrix

| Attribute | Microsoft-Hosted Agents | Self-Hosted Agents |
| :--- | :--- | :--- |
| **Maintenance** | Zero (Microsoft provisions, patches, updates OS) | Customer maintains OS, security patches, tooling |
| **Cleanliness** | **100% Ephemeral**: Fresh VM per job, wiped after | Reusable filesystem (requires manual workspace cleanup) |
| **Private VNet Access**| Cannot access private corporate networks natively | Sits inside private VPC/VNet; direct access to private DBs |
| **Build Caching** | No persistent disk cache across jobs | Fast local Docker layer and dependency caching |
| **Cost Model** | Billed by pipeline concurrency minutes | Billed for underlying VM compute infrastructure |
| **Custom Hardware** | Standard cloud VM sizes | Custom GPUs, high RAM, or specialized on-prem silicon |

---

## 7. Service Connections & Cloud Authentication

### How Pipelines Talk to Cloud Providers
* A **Service Connection** securely stores cloud credentials, tokens, or federated trust certificates in Azure DevOps project settings.
* **Modern Golden Standard**: **Workload Identity Federation (OIDC)**:
  * Eliminates long-lived secrets or client secret expiration issues.
  * Azure DevOps exchanges an ephemeral OpenID Connect (OIDC) token with Microsoft Entra ID (Azure AD) to assume a Service Principal role dynamically.

---

## 8. Variable Groups & Azure Key Vault Secrets Integration

### Secure Secret Injection
* **Variable Groups**: Centralized key-value collections shared across multiple pipelines.
* **Key Vault Linking**: Instead of typing secrets into Azure DevOps UI:
  1. Store database passwords and certificates inside Azure Key Vault.
  2. Toggle **Link secrets from an Azure key vault as variables** in the Variable Group.
  3. Azure DevOps fetches the secret dynamically at runtime without exposing plain text in logs.

---

## 9. Environments, Approval Gates, & Deployment Strategies

### Environment Protection Controls
* **Manual Approval**: Designated lead engineers must review deployment diff and click *"Approve"* before production stage runs.
* **Business Hours Only**: Gate that blocks releases on weekends or outside operational windows (`09:00 - 17:00 UTC`).
* **Query Work Items Check**: Automatically blocks deployment if open Priority 1 (P1) bugs exist on the board.
* **REST API Health Gate**: Queries APM endpoint (Datadog, Dynatrace, Azure Monitor); rolls back if error rate spikes.

---

## 10. Azure Artifacts: Package Feeds & Versioning

### Purpose & Benefits
* **Internal Package Sharing**: Publish private npm libraries, NuGet packages, or Python wheels across development teams.
* **Upstream Sources**: Caches public open-source packages from npmjs.org or NuGet.org internally; shields organization from upstream supply chain disruptions.

---

## 11. Senior DevOps Scenario Interview Q&A

### Q1: You need the `main` branch to only accept code through PRs with 2 approvals and zero failing builds. How do you implement this in Azure DevOps?
* Navigate to **Project Settings > Repositories > Policies > Branches > `main`**.
* Enable **Require a minimum number of reviewers**: Set to `2`, and check *"Prohibit most recent pusher from approving their own changes"*.
* Enable **Build Validation**: Select the CI pipeline (`azure-pipelines.yml`) to automatically build and test PR code.
* Enable **Check for linked work items**: Set to *"Required"*.
* Enable **Check for comment resolution**: Set to *"Required"*.

### Q2: A production deployment must only run if staging passes and a human signs off. How is this configured in YAML?
* Create a dedicated **Environment** named `production` under **Pipelines > Environments**.
* Add an **Approval Check** on the `production` environment assigning the designated Engineering Leads.
* In the YAML pipeline, define the production stage with `dependsOn: Staging` and set `environment: 'production'`.
* Azure Pipelines will pause execution upon reaching the production deployment job and notify approvers via email/Teams.

### Q3: How do you prevent credentials from expiring in Azure DevOps Service Connections?
* Transition from legacy Client Secret authentication to **Workload Identity Federation (OIDC)**.
* Azure DevOps establishes a trust relationship with Microsoft Entra ID (Azure AD) using cryptographic tokens, completely eliminating passwords, client secrets, and expiration maintenance.
