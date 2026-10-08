# 🌿 Git Version Control: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Git Architecture, The Three Trees (Working Dir, Staging, Repository), Git Object Model (Blobs, Trees, Commits), Merge vs Rebase, Disaster Recovery (Reflog, Detached HEAD), and Branch Governance.

---

## 📑 Table of Contents
- [What is Version Control & Why Git?](#why-git)
- [The Three Trees: Working Directory, Staging Index, Local Repository](#the-three-trees)
- [Git Internal Architecture & Object Model](#git-internals)
- [Branching & Merging: Fast-Forward vs 3-Way Merge](#branching--merging)
- [Git Merge vs Git Rebase Deep Dive](#merge-vs-rebase)
- [Emergency Recovery Playbook (git reflog, git revert, detached HEAD)](#emergency-recovery)
- [GitFlow Branch Governance & Pull Request Policies](#gitflow-governance)
- [Production Command Cheat Sheet & Interview Q&A](#command-cheatsheet--qa)

---

SECTION 5: GIT — COMPLETE GUIDE




Flow: VCS Basics → Git Basics → Working Areas → Commands → Branching → Merging → Remote Repos →
Undoing Changes → Advanced
1. What is Version Control System (VCS)?
Definition:
A Version Control System tracks and manages changes to files over time. It allows multiple developers to
collaborate on the same codebase, keep history of every change, and revert to any previous state.
Why DevOps needs VCS:
Every code change is tracked with who made it, when, and why
Multiple developers can work on same project without overwriting each other's work
Roll back to a stable version if something breaks
Foundation of CI/CD — pipelines trigger from code changes in VCS
2. Types of VCS
A) Local VCS
Tracks changes only on your local machine
No collaboration possible
Example: RCS (old, rarely used)
Problem: If your machine dies, everything is lost
B) Centralized VCS (CVCS)
One central server stores all versions
Developers pull from and push to that single server
Example: SVN (Subversion), CVS
Pros: Simple, single source of truth
Cons: Single point of failure — if server goes down, no one can work. No offline work.
C) Distributed VCS (DVCS)
Every developer has a full copy of the repository including complete history




Example: Git, Mercurial
Pros: Work offline, no single point of failure, faster operations, full history locally
Cons: Slightly more complex to learn
Git is a Distributed VCS — this is why it's the industry standard.
3. What is Git?
Definition:
Git is a free, open-source Distributed Version Control System created by Linus Torvalds in 2005. It tracks
changes in source code, supports non-linear development through branching, and enables team collaboration.
Key concepts:
Every change is a commit (a snapshot of your code at that point)
Branches let you work on features without affecting main code
Git is local first — most operations happen on your machine without internet
4. Git Workflow — The Four Areas
Understanding these four areas is the most important concept in Git:
Working Directory  →  Staging Area  →  Local Repository  →  Remote Repository
   (your files)      (git add)         (git commit)          (git push)
A) Working Directory
Where you actually write and edit your files
Files here are either tracked (Git knows about them) or untracked (new files Git hasn't seen)
Changes here are not saved to Git yet
B) Staging Area (Index)
A preparation zone before committing
You choose which changes to include in the next commit
Use git add  to move changes from working directory to staging area




Allows you to commit only specific changes, not everything
C) Local Repository
Your local Git database stored in the .git  folder
When you git commit , changes move from staging to local repo
Contains full history of all commits
Works completely offline
D) Remote Repository
A repository hosted on a server — GitHub, GitLab, Bitbucket, Azure Repos
Use git push  to send your local commits to remote
Use git pull  to get others' changes from remote
The central collaboration point for teams
5. Git Setup — First Time Configuration
# Set your identity (required before first commit)
git config --global user.name "DevOps & Cloud Engineer"
git config --global user.email "devops@example.com"
# Set default editor
git config --global core.editor vim
# Check all config
git config --list
# Initialize a new Git repo in current directory
git init
# Clone an existing remote repo to your machine
git clone https://github.com/username/repo.git
# Clone into a specific folder name
git clone https://github.com/username/repo.git my-folder




 
 
6. Basic Git Commands — Working Directory to Local Repo
Checking Status
git status              # see which files are modified, staged, or untracked
git status -s           # short status view
Tracking Files — git add (Working Directory → Staging Area)
git add filename.txt          # stage a specific file
git add .                     # stage ALL changes in current directory
git add *.js                  # stage all JS files
git add src/                  # stage all files in src folder
git add -p                    # interactively choose which changes to stage (patch mod
Committing — git commit (Staging Area → Local Repo)
git commit -m "Add login feature"           # commit with message
git commit -am "Fix bug"                    # add + commit tracked files in one step
git commit --amend -m "New message"         # fix last commit message (before push)
git commit --amend --no-edit               # add forgotten file to last commit
Viewing History
git log                          # full commit history
git log --oneline                # compact one-line view
git log --oneline --graph        # visual branch graph
git log --oneline -5             # last 5 commits
git log --author="DevOpsEngineer"         # commits by specific author
git log filename.txt             # history of a specific file
git show <commit-id>             # show details of a specific commit
Viewing Differences
git diff                         # changes in working directory (not staged)
git diff --staged                # changes in staging area (ready to commit)




git diff main feature-branch     # compare two branches
git diff <commit1> <commit2>     # compare two commits
7. Branching — Working in Isolation
What is a Branch?
A branch is an independent line of development. You create a branch to work on a feature or bug fix without
affecting the main codebase. When done, you merge it back.
Default branch: main  or master
Branch Commands
# View branches
git branch                    # list local branches
git branch -r                 # list remote branches
git branch -a                 # list all branches (local + remote)
# Create branch
git branch feature-login      # create new branch
git checkout -b feature-login # create AND switch to new branch (old way)
git switch -c feature-login   # create AND switch to new branch (new way)
# Switch branch
git checkout main             # switch to main branch (old way)
git switch main               # switch to main branch (new way)
# Rename branch
git branch -m old-name new-name
# Delete branch
git branch -d feature-login   # delete branch (safe — only if merged)
git branch -D feature-login   # force delete branch (even if not merged)
# Delete remote branch
git push origin --delete feature-login
Branch Workflow Example
# 1. Create feature branch from main
git switch main




git pull origin main          # make sure main is up to date
git switch -c feature-login   # create feature branch
# 2. Work on feature
# ... edit files ...
git add .
git commit -m "Add login page"
git commit -m "Add login API"
# 3. Push feature branch to remote
git push origin feature-login
# 4. Create Pull Request on GitHub/GitLab
# 5. After review, merge to main
8. Merging
What is Merging?
Merging combines changes from one branch into another. You typically merge a feature branch into main when
the feature is complete.
Types of Merges
A) Fast-Forward Merge
Happens when the target branch has no new commits since the feature branch was created. Git simply moves
the pointer forward. No merge commit created. Clean, linear history.
git switch main
git merge feature-login       # fast-forward if possible
Before:           After:
main: A-B         main: A-B-C-D
feature:   C-D
B) Three-Way Merge (2-Way Merge / Recursive Merge)
Happens when both branches have diverged — both have new commits. Git finds the common ancestor
commit and creates a new merge commit that combines both.




 
git switch main
git merge feature-login       # creates a merge commit
git merge --no-ff feature-login  # force merge commit even if fast-forward possible
Before:           After:
main: A-B-E       main: A-B-E---M  (M = merge commit)
feature:   C-D          \   C-D-/
C) Squash Merge
Combines all feature branch commits into a single commit on main. Keeps history clean.
git merge --squash feature-login
git commit -m "Add login feature"   # one clean commit
9. Merge Conflict
What is a Merge Conflict?
A merge conflict happens when two branches modify the same line of the same file differently. Git can't decide
which change to keep, so it asks you to resolve it manually.
When does it happen?
Two developers edit the same line in the same file
One developer deletes a file another developer modified
Both branches rename the same file differently
How to Resolve a Merge Conflict
# Step 1: Try to merge
git merge feature-login
# OUTPUT: CONFLICT (content): Merge conflict in app.js
# Step 2: Open the conflicted file — Git marks conflicts like this:
<<<<<<< HEAD (your current branch - main)
const port = 3000;
=======
const port = 8080;




>>>>>>> feature-login (incoming branch)
# Step 3: Manually edit the file to keep what you want:
const port = 3000;   # keep main's version
# OR
const port = 8080;   # keep feature's version
# OR combine both if needed
# Step 4: Remove the conflict markers <<<<<<<, =======, >>>>>>>
# Step 5: Stage the resolved file
git add app.js
# Step 6: Complete the merge
git commit -m "Merge feature-login — resolved port conflict"
# To abort a merge and go back to before
git merge --abort
10. Connecting to Remote Repository
What is a Remote?
A remote is a version of your repository hosted on a server (GitHub, GitLab, Azure Repos). origin  is the
default name for your remote.
Remote Commands
# View remotes
git remote -v                              # list remotes with URLs
git remote show origin                     # details about origin
# Add remote
git remote add origin https://github.com/devops/repo.git
# Change remote URL
git remote set-url origin https://github.com/devops/new-repo.git
# Remove remote
git remote remove origin




 
11. Push, Pull, Fetch — Syncing with Remote
git push — Local Repo → Remote
git push origin main                    # push main branch to origin
git push origin feature-login          # push feature branch
git push -u origin feature-login       # push and set upstream (track remote branch)
git push --force origin main           # force push (DANGEROUS — overwrites remote)
git push --force-with-lease            # safer force push (fails if remote has new com
git push origin --delete feature-login # delete remote branch
git push --tags                        # push all tags
git pull — Remote → Local (fetch + merge in one step)
git pull origin main                   # pull latest changes from main
git pull                               # pull from tracked upstream branch
git pull --rebase origin main          # pull and rebase instead of merge
git fetch — Download without Merging
git fetch origin                       # download all remote changes, don't merge
git fetch origin main                  # fetch specific branch
git fetch --all                        # fetch from all remotes
# After fetch, you can compare:
git diff main origin/main              # see what changed on remote
git merge origin/main                  # then manually merge when ready
Key Difference:
git pull  = git fetch  + git merge  — downloads AND merges automatically
git fetch  = downloads only, you decide when to merge — safer
git clone — Copy Remote Repo to Local
git clone https://github.com/devops/repo.git        # clone repo
git clone https://github.com/devops/repo.git myapp  # clone into specific folder




 
 
git clone --branch develop repo.git               # clone specific branch
git clone --depth 1 repo.git                      # shallow clone (latest commit only
12. Undoing Changes
This is one of the most important topics in Git interviews.
A) git checkout — Discard Working Directory Changes
git checkout -- filename.txt      # discard changes in working directory (old way)
git restore filename.txt          # discard changes in working directory (new way)
git restore .                     # discard ALL working directory changes
⚠  Warning: This is permanent — you lose your unsaved changes.
B) git reset — Unstage or Go Back in History
Three modes:
# 1. git reset --soft <commit>
# Moves HEAD back to that commit
# Changes go back to STAGING AREA (staged, ready to recommit)
git reset --soft HEAD~1           # undo last commit, keep changes staged
git reset --soft <commit-id>
# 2. git reset --mixed <commit> (DEFAULT)
# Moves HEAD back to that commit
# Changes go back to WORKING DIRECTORY (unstaged)
git reset HEAD~1                  # undo last commit, unstage changes
git reset HEAD filename.txt       # unstage a specific file
# 3. git reset --hard <commit>
# Moves HEAD back to that commit
# ALL changes are DELETED permanently
git reset --hard HEAD~1           # undo last commit, DELETE all changes
git reset --hard <commit-id>      # go back to specific commit, delete everything afte
⚠  Warning: --hard  deletes your work permanently. Use with caution.
When to use which:




 
 
Mode Changes go to Use when
--soft Staging area Want to recommit with different message
--mixed Working directory Want to re-edit before staging
--hard DELETED Want to completely undo, no going back
C) git revert — Safely Undo a Commit
git revert <commit-id>            # create a NEW commit that undoes the specified comm
git revert HEAD                   # revert last commit
git revert HEAD~3..HEAD           # revert last 3 commits
git revert --no-commit <commit-id> # revert without auto-committing
Key difference from reset:
git reset  — rewrites history (dangerous if already pushed)
git revert  — adds a new commit that undoes changes (safe, preserves history)
Rule: Use revert  for commits already pushed to remote. Use reset  only for local commits not yet
pushed.
D) git rm — Remove Files from Git
git rm filename.txt               # remove file from working dir AND staging
git rm --cached filename.txt      # remove from Git tracking only, keep file locally
git rm -r foldername/             # remove entire folder
# Common use: stop tracking a file (e.g., accidentally committed .env)
git rm --cached .env
echo ".env" >> .gitignore
git commit -m "Remove .env from tracking"
13. git stash — Save Work Temporarily
What is Stash?




Stash temporarily saves your uncommitted changes so you can switch branches or do something else, then
come back to your work.
git stash                         # stash current changes
git stash push -m "login work"   # stash with a name
git stash list                    # list all stashes
git stash pop                     # apply last stash and remove it from stash list
git stash apply                   # apply last stash but keep it in stash list
git stash apply stash@{2}         # apply specific stash
git stash drop stash@{0}          # delete specific stash
git stash clear                   # delete all stashes
Example:
# You're working on feature-login when urgent bug fix is needed
git stash                         # save your work
git switch main                   # switch to main
git switch -c hotfix-bug          # fix the bug
git commit -m "Fix critical bug"
git switch feature-login          # go back
git stash pop                     # restore your saved work
14. git cherry-pick — Pick Specific Commits
What is Cherry-pick?
Cherry-pick applies a specific commit from one branch to another. You pick only the commit you want, not the
entire branch.
git cherry-pick <commit-id>            # apply specific commit to current branch
git cherry-pick <commit1> <commit2>    # apply multiple commits
git cherry-pick A..B                   # apply range of commits
git cherry-pick --no-commit <commit-id> # apply changes without committing
git cherry-pick --abort                # abort cherry-pick if conflict
Example:
# You fixed a bug in feature branch and want that fix in main too
git log feature-branch --oneline
# abc1234 Fix null pointer bug
# def5678 Add new feature




git switch main
git cherry-pick abc1234     # apply only the bug fix to main, not the feature
When to use:
Bug fix in one branch needed in another
Pick specific features without merging entire branch
Backporting fixes to older release branches
15. git rebase — Rewrite History
What is Rebase?
Rebase moves or replays your commits on top of another branch. Creates a cleaner, linear history compared to
merge commits.
git rebase main               # rebase current branch onto main
git rebase --interactive HEAD~3  # interactive rebase — edit last 3 commits
git rebase --abort            # abort rebase
git rebase --continue         # continue after resolving conflict
Interactive rebase options:
git rebase -i HEAD~3
# Opens editor with:
# pick abc1234 First commit
# pick def5678 Second commit
# pick ghi9012 Third commit
# Change 'pick' to:
# squash  — combine with previous commit
# reword  — edit commit message
# drop    — delete commit
# edit    — pause to amend
Merge vs Rebase:
Merge Rebase
History Preserves full history with merge commits Creates clean linear history




Safety Safe for shared branches Never rebase shared/public branches
Use when Merging feature to main Keeping feature branch up to date with main
Rule: Never rebase commits that have been pushed to a shared remote branch.
16. git tag — Marking Releases
git tag                           # list all tags
git tag v1.0.0                    # create lightweight tag
git tag -a v1.0.0 -m "Release 1.0.0"  # create annotated tag (recommended)
git tag -a v1.0.0 <commit-id>    # tag a specific commit
git push origin v1.0.0           # push specific tag
git push origin --tags            # push all tags
git tag -d v1.0.0                 # delete local tag
git push origin --delete v1.0.0  # delete remote tag
Use in DevOps: Tag releases in CI/CD pipelines. When you tag a commit, the pipeline automatically builds and
deploys that version.
17. .gitignore — Excluding Files from Git
.gitignore tells Git which files to never track.
# Example .gitignore file:
node_modules/       # dependency folders
.env                # environment variables (NEVER commit secrets)
*.log               # log files
dist/               # build output
.DS_Store           # Mac system files
*.jar               # compiled Java files
target/             # Maven build folder
__pycache__/        # Python cache
# Check what's being ignored
git status --ignored
# If you accidentally committed something:




git rm --cached filename
echo "filename" >> .gitignore
git commit -m "Remove accidentally committed file"
18. Git Branching Strategies
A) Gitflow
Classic strategy with long-lived branches:
main  — production code only
develop  — integration branch
feature/*  — new features
release/*  — release preparation
hotfix/*  — urgent production fixes
B) GitHub Flow (Recommended for DevOps)
Simpler, faster:
main  — always deployable
feature/*  — short-lived feature branches
Create PR → review → merge to main → deploy
C) Trunk Based Development
Everyone commits directly to main  (trunk)
Very short-lived branches (hours, not days)
Heavy use of feature flags
Used by high-velocity teams like Google
19. Pull Request (PR) Workflow
# 1. Create feature branch
git switch -c feature-payment
# 2. Make changes and commit




git add .
git commit -m "Add payment gateway"
# 3. Push to remote
git push -u origin feature-payment
# 4. Create PR on GitHub/GitLab/Azure Repos
# — Add description of what changed and why
# — Link to task/ticket (in your Azure DevOps project you used PR templates)
# — Request reviewers
# 5. After review and approval — merge to main
# 6. Delete feature branch
git branch -d feature-payment
git push origin --delete feature-payment
20. Common Git Interview Questions
Q: What is HEAD in Git?
HEAD is a pointer to the current commit you're on. Usually points to the tip of your current branch. When you
checkout a branch, HEAD moves to that branch's latest commit.
Q: What is detached HEAD?
When HEAD points directly to a commit instead of a branch. Happens when you git checkout . Any
commits made in detached HEAD state can be lost. Create a branch to save work: git switch -c new-
branch
Q: Difference between git pull and git fetch?
git fetch  downloads changes but doesn't merge. git pull  downloads AND merges. Use fetch when
you want to review changes before merging.
Q: How do you squash commits?
git rebase -i HEAD~3    # interactively squash last 3 commits
# change 'pick' to 'squash' for commits to combine
Q: How do you find which commit introduced a bug?
git bisect start
git bisect bad              # current commit is bad
git bisect good <commit-id> # last known good commit




# Git checks out commits between — you test each one
git bisect good/bad         # mark each until bug is found
git bisect reset            # end bisect
21. Quick Reference — Most Used Git Commands
# DAILY WORKFLOW
git status                          # check what's changed
git add .                           # stage all changes
git commit -m "message"             # commit
git push origin branch-name         # push to remote
git pull origin main                # get latest changes
# BRANCHING
git switch -c feature-name          # create and switch to new branch
git switch main                     # go back to main
git merge feature-name              # merge feature into current branch
git branch -d feature-name          # delete branch after merge
# UNDOING
git restore filename                # discard working directory changes
git reset HEAD filename             # unstage a file
git reset --soft HEAD~1             # undo last commit, keep changes staged
git reset --hard HEAD~1             # undo last commit, DELETE changes
git revert <commit-id>              # safely undo pushed commit
# REMOTE
git remote -v                       # view remotes
git fetch origin                    # download without merging
git pull origin main                # download and merge
git push origin branch-name         # upload to remote
git clone <url>                     # copy remote repo locally
# INSPECTION
git log --oneline --graph           # visual history
git diff                            # see unstaged changes
git show <commit-id>                # see commit details
git blame filename                  # who changed each line
# ADVANCED
git stash                           # save work temporarily
git stash pop                       # restore saved work
git cherry-pick <commit-id>         # apply specific commit




git rebase main                     # rebase onto main
git tag -a v1.0.0 -m "Release"     # create release tag

