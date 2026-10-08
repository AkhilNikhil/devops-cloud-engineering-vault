# 🌿 Git Source Control: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Distributed Version Control Internals, The 4 Git Working Areas, Branching Strategies (GitFlow, Trunk-Based), Fast-Forward vs Three-Way Merge, Rebase vs Merge, Safe Undoing (`reset`, `revert`, `restore`), Stashing, Cherry-Picking, Interactive Rebase & Squashing, Reflog Recovery, and Senior Interview Playbooks.

---

## 📑 Table of Contents
- [1. Version Control Concepts: Centralized vs Distributed](#1-version-control-concepts-centralized-vs-distributed)
- [2. The 4 Git Working Areas & Data Flow](#2-the-4-git-working-areas--data-flow)
- [3. Essential Initial Setup & Configuration](#3-essential-initial-setup--configuration)
- [4. Core Daily Commands (`status`, `add`, `commit`, `log`, `diff`)](#4-core-daily-commands-status-add-commit-log-diff)
- [5. Branching Strategies & Merge Workflows](#5-branching-strategies--merge-workflows)
- [6. `git merge` vs `git rebase` Deep Dive](#6-git-merge-vs-git-rebase-deep-dive)
- [7. Undoing Mistakes Safely (`restore`, `reset`, `revert`)](#7-undoing-mistakes-safely-restore-reset-revert)
- [8. Advanced Power Tools: Stash, Cherry-Pick, & Squashing](#8-advanced-power-tools-stash-cherry-pick--squashing)
- [9. Disaster Recovery with `git reflog`](#9-disaster-recovery-with-git-reflog)
- [10. Senior DevOps Interview Q&A](#10-senior-devops-interview-qa)

---

## 1. Version Control Concepts: Centralized vs Distributed

### Centralized (CVCS) vs Distributed (DVCS)

| Attribute | Centralized VCS (SVN, Perforce, CVS) | Distributed VCS (Git, Mercurial) |
| :--- | :--- | :--- |
| **Repository Storage** | Single central server holds full history | Every developer laptop holds the **entire** repository history |
| **Offline Work** | ❌ Cannot commit, view history, or branch offline | ✅ Full local commits, logs, branches, and diffs with zero internet |
| **Speed** | Slow (Every action requires network round-trip) | Extremely Fast (All operations execute locally on disk) |
| **Single Point of Failure**| High (If central server dies, work stalls) | Low (Any developer laptop acts as a full backup of the repo) |

---

## 2. The 4 Git Working Areas & Data Flow

### Architecture Diagram
```text
┌────────────────────┐          ┌────────────────────┐          ┌────────────────────┐          ┌────────────────────┐
│ Working Directory  │──git add─►│   Staging Area     │─git commit►│  Local Repository │──git push─►│ Remote Repository  │
│  (Untracked/Dirty) │◄─restore─│     (Index)        │◄──reset───│     (.git HEAD)    │◄─git fetch─│ (GitHub / GitLab)  │
└────────────────────┘          └────────────────────┘          └────────────────────┘          └────────────────────┘
```

### The 4 State Zones
* **1. Working Directory**: The physical filesystem folder where you edit and create files. Files here are either *untracked* or *modified*.
* **2. Staging Area (Index)**: A preparation buffer caching exact changes queued for the next commit snapshot (`git add`).
* **3. Local Repository**: Committed immutable snapshots stored inside `.git/objects` on your machine.
* **4. Remote Repository**: Hosted cloud server (GitHub, GitLab, Bitbucket) used for team collaboration (`git push`, `git fetch`).

---

## 3. Essential Initial Setup & Configuration

```bash
# Configure global author identity (Included in all commit metadata)
git config --global user.name "DevOps Engineer"
git config --global user.email "devops@example.com"

# Set default initial branch name to main
git config --global init.defaultBranch main

# Set default diff/merge editor to vim or nano
git config --global core.editor "vim"

# Verify all configured settings
git config --list
```

---

## 4. Core Daily Commands (`status`, `add`, `commit`, `log`, `diff`)

```bash
# Initialize a new Git repository in current folder
git init

# Clone existing remote repository
git clone https://github.com/your-org/my-app.git

# Inspect working tree status (untracked, modified, staged files)
git status -s

# Stage changes
git add file.py          # Stage single file
git add .                # Stage all modified and untracked files in directory
git add -p               # Interactive staging: review and stage specific code chunks

# Commit staged changes with descriptive message
git commit -m "feat(auth): implement JWT token verification middleware"

# Inspect commit history
git log --oneline -n 10                # Compact one-line view of last 10 commits
git log --graph --oneline --all        # Visual ASCII branch graph
git log -p file.py                     # View full line-by-line diff history for specific file

# Inspect differences
git diff                               # Diff between Working Directory and Staging Area
git diff --staged                      # Diff between Staging Area and last commit (HEAD)
git diff HEAD~1 HEAD                   # Compare last commit with previous commit
```

---

## 5. Branching Strategies & Merge Workflows

### Branch Management CLI
```bash
# List branches (* indicates currently active branch)
git branch -a

# Create a new feature branch and switch to it
git switch -c feature/login-api        # Modern Git 2.23+ syntax
git checkout -b feature/login-api      # Traditional syntax

# Switch between existing branches
git switch main

# Delete a merged branch
git branch -d feature/login-api

# Force delete an unmerged branch
git branch -D feature/abandoned-poc
```

### Enterprise Branching Models
* **Trunk-Based Development (DevOps Standard)**:
  * Developers merge short-lived feature branches (< 1 day) directly into `main`.
  * Enforces frequent CI runs, fast feedback loops, and zero long-lived merge hell.
* **GitFlow (Traditional Enterprise)**:
  * Uses dedicated long-lived branches: `main` (production), `develop` (integration), `feature/*`, `release/*`, `hotfix/*`.

---

## 6. `git merge` vs `git rebase` Deep Dive

### Comparison Matrix

| Feature | `git merge` | `git rebase` |
| :--- | :--- | :--- |
| **History Shape** | Non-linear (Preserves exact branch divergence graph) | Perfectly linear (Replays commits on top of target branch) |
| **Merge Commit** | Creates a 2-parent merge commit (`Merge branch 'feature'`) | Creates **no** merge commit (Clean fast-forward) |
| **Commit Hashes** | Preserves original commit SHAs | Re-writes new commit SHAs for replayed commits |
| **Golden Rule** | Safe for public, shared team branches | **Never rebase a public branch that others have pulled!** |

### Visual Comparison
```text
[GIT MERGE]
      A---B---C (feature)
     /         D---E-----------M (main - Merge commit M created)

[GIT REBASE]
              A'--B'--C' (feature commits re-written on top of E)
             /
D---E-------+ (main)
```

### Execution Commands
```bash
# Merge feature branch into main
git switch main
git merge feature/login-api

# Rebase feature branch onto latest main
git switch feature/login-api
git rebase main

# Abort an ongoing merge or rebase during conflict
git merge --abort
git rebase --abort
```

---

## 7. Undoing Mistakes Safely (`restore`, `reset`, `revert`)

### Decision Matrix: How to Undo in Git

| Scenario | Recommended Command | Impact on Git History |
| :--- | :--- | :--- |
| **Discard unstaged file edits in working directory** | `git restore <file>` | Zero history impact; reverts file to last staged/committed state |
| **Unstage a file without losing its edits** | `git restore --staged <file>` | Removes file from index back to working directory |
| **Undo local unpushed commits (Keep changes in working dir)**| `git reset --mixed HEAD~1` | Moves HEAD back 1 commit; keeps edits unstaged in working directory |
| **Undo local unpushed commits (Keep changes staged)** | `git reset --soft HEAD~1` | Moves HEAD back 1 commit; keeps edits staged in index |
| **Nuclear undo: Completely destroy last local commit & edits**| `git reset --hard HEAD~1` | Destroys commit and discards all code modifications |
| **Undo a commit that is ALREADY pushed to GitHub / remote** | `git revert <commit-sha>` | **Safe for teams**: Appends a brand new commit that inverts changes |

---

## 8. Advanced Power Tools: Stash, Cherry-Pick, & Squashing

### 1. `git stash` (Temporary Shelf)
* Temporarily shelves uncommitted modifications so you can switch branches to handle urgent hotfixes without committing broken work:
```bash
# Save uncommitted changes to stash with message
git stash save "WIP: halfway through refactoring payment gateway"

# List all stashed entries
git stash list

# Re-apply latest stashed changes and remove from stash list
git stash pop

# Discard latest stashed entry
git stash drop
```

### 2. `git cherry-pick` (Selective Commit Copy)
* Copies an exact specific commit from another branch and applies it to your current active branch:
```bash
# Apply commit c1a2b3 onto current branch
git cherry-pick c1a2b3
```

### 3. Interactive Rebase & Squashing (`rebase -i`)
* Cleans up messy local histories (e.g., *"fix typo"*, *"wip"*, *"debug"*) into a single polished commit before opening a Pull Request:
```bash
# Interactively squash the last 3 commits
git rebase -i HEAD~3

# In the interactive editor, change 'pick' to 'squash' (or 's') on secondary commits:
# pick a1b2c3d feat(user): add user registration endpoint
# squash e4f5g6h fix typo in validator
# squash j7k8l9m add unit test coverage
```

---

## 9. Disaster Recovery with `git reflog`

### What is Reflog?
* Git's local safety net; records **every single time HEAD moves** (commits, checkouts, hard resets, merges, rebases).
* Even if you run `git reset --hard` and accidentally delete your work, commits remain in `.git/objects` for ~30 days.

### Emergency Recovery Procedure
```bash
# 1. View historical log of HEAD movements
git reflog

# Sample Output:
# 7b2c1a0 HEAD@{0}: reset: moving to HEAD~1  <-- Accidentally destroyed work!
# 9a8b7c6 HEAD@{1}: commit: feat: completed payment module <-- Target commit!

# 2. Resurrect destroyed work by resetting to pre-disaster HEAD state:
git reset --hard 9a8b7c6
# Or resurrect into a brand new branch:
git branch recovered-work 9a8b7c6
```

---

## 10. Senior DevOps Interview Q&A

### Q1: What is `HEAD` in Git, and what does a "Detached HEAD" state mean?
* **`HEAD`**: A pointer representing the current active snapshot. Normally points to a branch reference (e.g., `HEAD -> refs/heads/main`).
* **Detached HEAD**: Occurs when you checkout a specific commit hash or tag directly (`git checkout a1b2c3d`) instead of a branch.
* In this state, `HEAD` points directly to a commit SHA. New commits created here are not attached to any branch and will become orphaned and garbage collected unless anchored to a new branch (`git switch -c new-branch`).

### Q2: What is the exact difference between `git fetch` and `git pull`?
* **`git fetch`**: Downloads remote commits, branches, and tags into local remote-tracking branches (`origin/main`) without modifying your local working files. 100% safe to run anytime.
* **`git pull`**: Combination of two commands: `git fetch` followed immediately by `git merge FETCH_HEAD` (or `git rebase` if configured). Mutates your local working directory and can trigger merge conflicts.

### Q3: Why is `git push --force-with-lease` safer than `git push --force`?
* **`--force`**: Blindly overwrites the remote branch with your local history. If a teammate pushed a commit in the meantime, their work is permanently destroyed.
* **`--force-with-lease`**: Checks if the remote ref matches your local tracking branch before overwriting. If someone else pushed commits to the remote that you have not fetched, the push is safely rejected!
