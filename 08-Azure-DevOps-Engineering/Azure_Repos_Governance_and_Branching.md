# 📘 Azure Repos Governance, Pull Request Policies, Branch Protections

> *Comprehensive Azure DevOps engineering documentation and hands-on guide.*

---

```text
SUMMARY OF AZURE REPOS VIDEO CONTENT

========================================================
OVERVIEW
========================================================
This video is part of an Azure DevOps full course and focuses on Azure Repos, explaining concepts, 
configuration, and practical usage using a demo project called Parts Unlimited. The tutorial demonstrates 
Git-based workflows, source control management, and collaboration practices using Azure Repos.

========================================================
INTRODUCTION TO SOURCE CONTROL & AZURE REPOS
========================================================

Azure Repos:
- A source control system within Azure DevOps used to track and manage code changes.
- Enables collaboration, version history tracking, and code organization.

Key Benefits:
- Track code snapshots and history
- Roll back changes
- Review code before merging
- Organize and maintain codebase efficiently

Historical Context:
- Before version control, developers shared code via shared drives, causing collaboration 
    and conflict issues.

========================================================
GIT VS TFVC (TEAM FOUNDATION VERSION CONTROL)
========================================================

Azure Repos supports two version control systems:

1. Git (Distributed Version Control)
- Developers clone entire repositories locally.
- Supports offline development.
- Changes synced later with remote repositories.
- Widely adopted in startups and enterprises.
- Flexible and collaboration-friendly.

2. TFVC (Centralized Version Control)
- Only one version downloaded locally.
- Full history stored on server.
- Uses file locking.
- Less popular due to conflict resolution challenges.

Note:
- The video primarily focuses on Git workflows.

========================================================
CONFIGURING GIT CLIENT (VS CODE DEMO)
========================================================

Setup Steps:
- Configure credential helper to save credentials.
- Set global username and email.
- Clone repository from Azure Repos.
- Authenticate using Microsoft account.

Workflow Demonstrated:
- Modify code
- Stage changes
- Commit locally
- Sync/push to remote repository

Key Point:
- Commit messages help collaborators understand changes.

========================================================
COMMIT, STAGING, AND SYNCING
========================================================

Concepts:
- Changes appear in staging area before commit.
- Only staged files are committed.
- Sync pushes commits to remote repository.
- Selective staging allows partial commits.

Commit History:
- Shows author information.
- Displays added lines (green).
- Displays deleted lines (red).

========================================================
BRANCHES AND BRANCH MANAGEMENT
========================================================

Purpose of Branches:
- Isolate development without affecting main codebase.

Key Concepts:
- Local Branches: Exist on developer machine.
- Remote Branches: Stored in Azure Repos.

Example Workflow:
- Create dev branch from master.
- Develop features safely.
- Merge into master after review.

Branch Operations:
- Create branches
- Delete local/remote branches
- Prune unused remote references

========================================================
BRANCH MANAGEMENT IN AZURE REPOS UI
========================================================

Features Demonstrated:
- Create branches
- Delete and restore branches
- Lock branches (read-only during code freeze)
- Create tags (e.g., release version 1.1)
- Create, rename, and delete repositories

========================================================
PULL REQUEST (PR) WORKFLOW
========================================================

Purpose:
- Control and review code before merging into main branches.

Process:
1. Developer creates feature branch.
2. Makes and pushes changes.
3. Creates pull request.
4. Reviewers evaluate code.
5. Approve / reject / suggest changes.
6. Merge PR after approval.
7. Linked work items marked complete.

Benefits:
- Improves code quality.
- Encourages collaboration and review.

========================================================
BRANCH AND PULL REQUEST POLICIES
========================================================

Policies enforce standards and security.

Examples:
- Minimum reviewer requirement (e.g., 2 reviewers).
- Prevent self-approval.
- Require linked work items before merge.
- Auto-add mandatory reviewers.

Configuration:
- Managed in Azure DevOps Project Settings.

========================================================
TIMELINE OF KEY DEMONSTRATIONS
========================================================

00:00 - 02:00
- Introduction to Azure Repos and source control.

02:00 - 05:00
- Git vs TFVC comparison.

05:00 - 09:00
- Git client configuration in VS Code.

07:00 - 10:30
- Clone repo and make first commit.

10:30 - 14:00
- Managing staged  vs unstaged changes.

14:00 - 17:00
- Branch concepts and creation.

17:00 - 21:30
- Deleting and pruning branches.

21:30 - 25:30
- Branch management in Azure Repos UI.

25:30 - 28:00
- Creating and deleting repositories.

28:00 - 31:30
- Pull request workflow.

31:30 - 33:45
- Branch and PR policies.

========================================================
KEY INSIGHTS
========================================================

- Azure Repos integrates Git for distributed collaboration.
- Git enables offline work and local history tracking.
- Branching strategies are essential for parallel development.
- Pull requests enforce review and code quality.
- Branch policies maintain governance and standards.
- Repository management can be done via VS Code or Azure portal.
- Tags help mark releases and important milestones.
- Hands-on practice is essential for mastery.

========================================================
TERMINOLOGY TABLE
========================================================

Azure Repos:
Cloud-hosted Git/TFVC repository service in Azure DevOps.

Git:
Distributed version control system supporting local clones and offline work.

TFVC:
Centralized version control system with server-side history.

Branch:
Separate development line to isolate changes.

Commit:
Snapshot of code changes.

Staging Area:
Intermediate step before committing.

Pull Request (PR):
Request to merge changes after review.

Tag:
Label attached to a specific commit (often release marker).

Branch Policies:
Rules enforcing review and collaboration standards.

Sync:
Operation pushing local commits to remote repository.

========================================================
RECOMMENDATIONS FOR USERS
========================================================

- Practice cloning, branching, committing, and pull requests.
- Understand local vs remote branches.
- Use branch policies to maintain quality.
- Use tags to mark releases.
- Explore both Azure Repos UI and Git clients like VS Code.









SUMMARY – AZURE DEVOPS PULL REQUEST (PR) TEMPLATE TUTORIAL

========================================================
OVERVIEW
========================================================
This tutorial explains how to create and use Pull Request (PR) templates in Azure DevOps 
repositories. PR templates help standardize the pull request process by automatically populating 
the PR description with predefined content, improving clarity, consistency, and collaboration 
during code reviews.

========================================================
CORE CONCEPTS
========================================================

Pull Request (PR) Template:
- A predefined markdown file used to auto-fill the PR description when creating a pull request.
- Stored inside the repository.
- Helps developers provide consistent context for reviewers.

Purpose of PR Templates:
- Reduce manual writing during PR creation.
- Ensure important details are always included.
- Improve communication and review efficiency.

Typical Information Included:
- Type of PR (Feature / Bugfix / Enhancement)
- Summary of changes
- Related work items or issues
- Screenshots (if UI changes)
- Unit testing details
- Documentation updates
- Post-deployment tasks

========================================================
STEP-BY-STEP WORKFLOW
========================================================

Step 1:
Access Azure DevOps organization and open a project with an existing repository.

Step 2:
At the root of the repository, create a folder:

    .azuredevops

IMPORTANT:
Azure DevOps recognizes PR templates only when placed in this folder.

Step 3:
Inside the folder, create the file:

    pull_request_template.md

Step 4:
Add template content using Markdown.

Step 5:
Commit the template file to the main (default) branch.

Step 6:
Create a new feature branch from main.

Step 7:
Make code changes and commit.

Step 8:
Create a Pull Request from feature branch → main branch.

Step 9:
PR creation page automatically loads template content.

Step 10:
Developer fills or updates template fields.

Step 11:
Reviewers review, approve/reject, and PR is merged.

Optional:
Delete feature branch after merge.

========================================================
EXAMPLE PR TEMPLATE (MARKDOWN)
========================================================

File: .azuredevops/pull_request_template.md

--------------------------------------------------------
## What type of PR is this?
- [ ] Feature
- [ ] Bugfix
- [ ] Enhancement
- [ ] Refactor

## Description of changes
Explain what was changed and why.

## Related Work Item / Issue
Link Azure Boards item or ticket.

## Screenshots (if applicable)
Attach screenshots or UI proof.

## Unit Testing
Describe tests added or explain why none were added.

## Documentation
Mention documentation updates if required.

## Post-deployment tasks
List any required manual steps after deployment.
--------------------------------------------------------

NOTE:
Template content is fully customizable based on team needs.

========================================================
GIT COMMANDS (PRACTICAL FLOW)
========================================================

Clone repository:
    git clone <repo-url>

Create feature branch:
    git checkout -b feature/my-feature

Create template folder and file:
    mkdir .azuredevops
    touch .azuredevops/pull_request_template.md

Add files:
    git add .

Commit changes:
    git commit -m "Added PR template"

Push branch:
    git push origin feature/my-feature

Create PR:
- Go to Azure DevOps → Repos → Pull Requests
- Create new PR from feature branch → main

========================================================
KEY INSIGHTS
========================================================

- The folder name ".azuredevops" is mandatory.
- Template must be a markdown (.md) file.
- Once merged into main branch, template auto-loads for all future PRs.
- Standardized PR descriptions improve code review quality.
- Reviewers quickly understand:
    * What changed
    * Why it changed
    * How it was tested

========================================================
ADDITIONAL NOTES
========================================================

- Demo uses a sample Java project.
- Template creation can be done via:
    * Azure DevOps Web UI
    * VS Code
    * Any Git client
- Source branch deletion after merge is optional but recommended.
- Template acts as a starting point and should evolve with team needs.

========================================================
COMMON MISTAKES (IMPORTANT)
========================================================

1. Wrong folder location
   ❌ pull_request_template.md in root
   ✔ .azuredevops/pull_request_template.md

2. Not merged into main branch
   Template works only after it exists in default branch.

3. Wrong file name
   Must be exactly:
   pull_request_template.md

========================================================
KEYWORDS
========================================================

Azure DevOps
Pull Request (PR)
PR Template
Markdown
Repository
Feature Branch
Code Review
Automated PR Description
Code Merge
Source Branch Deletion

========================================================
CONCLUSION
========================================================

PR templates in Azure DevOps provide a structured and standardized way to create pull requests.
 By adding a markdown template inside the .azuredevops folder, teams ensure consistent documentation,
clearer communication, and faster code reviews. The feature improves collaboration and helps maintain 
development quality across projects.
```
