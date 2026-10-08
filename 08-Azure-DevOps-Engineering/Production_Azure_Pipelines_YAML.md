# 🚀 Production Azure DevOps Pipelines YAML Template

```yaml
# ==============================================================================
# Azure DevOps Multi-Stage CI/CD Pipeline
# Author: Akhil B M (github.com/AkhilNikhil)
# Architecture: Build -> Automated Test -> Artifact Staging -> Self-Hosted Deploy
# ==============================================================================

name: $(Date:yyyyMMdd)$(Rev:.r)

trigger:
  branches:
    include:
      - main
      - release/*
  paths:
    exclude:
      - docs/*
      - README.md
      - .gitignore

pr:
  branches:
    include:
      - main

variables:
  - template: variables/dev-vars.yml
  - name: buildConfiguration
    value: 'Release'
  - name: artifactName
    value: 'drop'

stages:
  # ----------------------------------------------------------------------------
  # STAGE 1: Build & Package
  # ----------------------------------------------------------------------------
  - stage: Build
    displayName: '🔨 Build & Package'
    jobs:
      - job: BuildJob
        displayName: 'Compile & Package Application'
        pool:
          name: $(agentPool)
          demands:
            - agent.name -equals $(agentName)
        steps:
          - template: templates/build-stage.yml
            parameters:
              buildConfig: $(buildConfiguration)

  # ----------------------------------------------------------------------------
  # STAGE 2: Automated Testing & Quality Gate
  # ----------------------------------------------------------------------------
  - stage: Test
    displayName: '🧪 Automated Testing & Code Quality'
    dependsOn: Build
    condition: succeeded()
    jobs:
      - job: TestJob
        displayName: 'Run Unit Tests & Quality Verification'
        pool:
          name: $(agentPool)
        steps:
          - template: templates/test-stage.yml
            parameters:
              failOnFailedTests: true

  # ----------------------------------------------------------------------------
  # STAGE 3: Multi-Node Deployment (Self-Hosted Linux Target)
  # ----------------------------------------------------------------------------
  - stage: Deploy
    displayName: '🚀 Multi-Node Deployment'
    dependsOn: Test
    condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
    jobs:
      - deployment: DeployWebNode
        displayName: 'Deploy to Target VM Host'
        pool:
          name: $(agentPool)
        environment: 'production-vm-nodes'
        strategy:
          runOnce:
            deploy:
              steps:
                - template: templates/deploy-stage.yml
                  parameters:
                    deployPath: '/opt/webapps'
                    servicePort: 80

```
