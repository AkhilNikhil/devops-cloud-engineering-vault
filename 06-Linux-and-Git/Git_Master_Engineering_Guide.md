# 🌿 Git Source Control: The Definitive Master Engineering Guide

> **Authoritative Master Reference & Senior Technical Interview Playbook**  
> Covers Distributed Version Control Architecture, The 4 Git Working Areas, Conventional Commits, Complete Branching Strategies (GitFlow vs Trunk-Based), Merging vs Rebasing, Safe Undoing (`restore`, `reset`, `revert`), Stashing, Cherry-Picking, Interactive Rebase & Squashing, Disaster Recovery with `git reflog`, and Complete CLI Command Reference.

---

## 📑 Table of Contents
- [1. Version Control Architecture: Centralized vs Distributed](#1-version-control-architecture-centralized-vs-distributed)
- [2. The 4 Git Working Areas & Data Flow](#2-the-4-git-working-areas--data-flow)
- [3. Complete Git Command Reference (Categorized)](#3-complete-git-command-reference-categorized)
- [4. Branching Strategies & Merge Workflows](#4-branching-strategies--merge-workflows)
- [5. `git merge` vs `git rebase` Deep Dive](#5-git-merge-vs-git-rebase-deep-dive)
- [6. Undoing Changes Safely: `restore` vs `reset` vs `revert`](#6-undoing-changes-safely-restore-vs-reset-vs-revert)
- [7. Advanced Power Tools: Stash, Cherry-Pick, & Squashing](#7-advanced-power-tools-stash-cherry-pick--squashing)
- [8. Disaster Recovery with `git reflog`](#8-disaster-recovery-with-git-reflog)
- [9. Senior DevOps Interview Q&A](#9-senior-devops-interview-qa)

---

## 1. Version Control Architecture: Centralized vs Distributed

### Centralized (CVCS) vs Distributed (DVCS)

| Attribute | Centralized VCS (SVN, Perforce) | Distributed VCS (Git, Mercurial) |
| :--- | :--- | :--- |
| **Repository Storage** | Single central server holds full history | Every developer machine holds the **entire** repository history |
| **Offline Work** | ❌ Cannot commit, view history, or branch offline | ✅ Full local commits, logs, branches, and diffs with zero internet |
| **Performance** | Slow (Every action requires network round-trip) | Extremely Fast (All operations execute locally on disk) |
| **Single Point of Failure**| High (If central server fails, all engineering halts)| Low (Any developer laptop acts as a full backup of the repo) |

---

## 2. The 4 Git Working Areas & Data Flow

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
* **4. Remote Repository**: Central shared repository hosted on GitHub, GitLab, or AWS CodeCommit (`git push`).

---

## 3. Complete Git Command Reference (Categorized)

### 1. Setup & Configuration
* `git init` — Initialize a new Git repository in the current directory.
* `git clone <repo_url>` — Clone a remote repository to local machine.
* `git config --global user.name "Akhil B M"` — Set global commit author name.
* `git config --global user.email "akhil@example.com"` — Set global commit author email.
* `git config --list` — List all active global and local Git configurations.

### 2. Daily Workflow: Staging & Commits
* `git status` — Check status of tracked and untracked files in working tree.
* `git add <file>` — Stage a specific file for the next commit.
* `git add .` — Stage all modified and new files in the current directory.
* `git add -p` — Interactive patch staging; stage specific chunks/hunks within a file.
* `git commit -m "feat: implement user authentication"` — Commit staged changes with message.
* `git commit --amend` — Modify the previous commit message or include newly staged files.

### 3. Inspection & Diffs
* `git log --oneline --graph --all` — View compact visualized commit history.
* `git log --author="Akhil"` — Filter commit history by author name.
* `git diff` — View unstaged changes between working directory and staging index.
* `git diff --staged` — View staged changes ready to be committed.
* `git diff commitA..commitB` — Compare differences between two specific commit hashes.

### 4. Branching & Merging
* `git branch -a` — List all local and remote tracking branches.
* `git branch <branch-name>` — Create a new branch.
* `git checkout -b <branch-name>` / `git switch -c <name>` — Create and switch to new branch.
* `git branch -d <branch-name>` — Safely delete merged branch.
* `git branch -D <branch-name>` — Force delete unmerged branch.
* `git merge <branch-name>` — Merge specified branch into the current checked-out branch.
* `git merge --abort` — Abort a merge conflict and restore previous state.

### 5. Remote Repositories & Syncing
* `git remote -v` — List all configured remote repository URLs.
* `git remote add origin <url>` — Add remote repository alias.
* `git fetch origin` — Download new remote branches and commits without merging.
* `git pull origin main` — Fetch and immediately merge changes from remote branch.
* `git push -u origin feature-auth` — Push local branch to remote and set upstream tracking.
* `git push --force-with-lease` — Safe force push; verifies no one else pushed new commits before overwriting.

---

## 4. Branching Strategies & Merge Workflows

### 1. Trunk-Based Development (Modern Cloud Standard)
* Developers merge small, frequent commits into a single `main` branch multiple times per day.
* Relies on automated CI/CD test pipelines and feature flags to protect production.
* Minimizes painful merge conflicts and accelerates deployment frequency.

### 2. GitFlow (Legacy Enterprise Standard)
* Uses dedicated long-lived branches: `main` (production), `develop` (integration), `feature/*`, `release/*`, `hotfix/*`.
* Structured for scheduled release cycles; higher maintenance overhead.

---

## 5. `git merge` vs `git rebase` Deep Dive

```text
Feature Branch: A ──► B ──► C
Main Branch:    X ──► Y ──► Z

GIT MERGE (Three-Way Merge Commit):
Main: X ──► Y ──► Z ──────────► M (Merge Commit)
                   \           /
                    A ──► B ──► C

GIT REBASE (Linear Rewriting):
Main: X ──► Y ──► Z ──► A' ──► B' ──► C' (Zero Merge Commits)
```

### Point-by-Point Comparison

| Feature | `git merge` | `git rebase` |
| :--- | :--- | :--- |
| **Commit History** | Preserves exact chronological history and adds a merge commit | Rewrites commit history linearly onto the tip of target branch |
| **Traceability** | High: Shows exactly when feature branches were integrated | Clean: Linear commit graph, easy to audit with `git log` |
| **Safety** | Non-destructive: Does not alter existing commit hashes | Destructive: Generates **brand new commit hashes** |
| **Golden Rule** | Use whenever merging branches into public shared branches | **NEVER rebase commits that have already been pushed to a public shared branch!** |

---

## 6. Undoing Changes Safely: `restore` vs `reset` vs `revert`

### 1. `git restore` (Discard Working Directory Changes)
* `git restore <file>` — Discards unstaged modifications in working directory.
* `git restore --staged <file>` — Unstages a file back to modified state without losing code.

### 2. `git reset` (Move HEAD Pointer Backwards)
* **`--soft`**: Moves `HEAD` back to specified commit. Leaves all changes staged in the index.
* **`--mixed` (Default)**: Moves `HEAD` back; unstages changes into working directory.
* **`--hard`**: **Destructive!** Moves `HEAD` back and permanently wipes all working directory changes!

### 3. `git revert` (Safe Inverse Commit)
* Creates a **brand new commit** that introduces the exact mathematical inverse of the target commit.
* Does not rewrite history; **safe to use on shared production branches**.

---

## 7. Advanced Power Tools: Stash, Cherry-Pick, & Squashing

> **💡 Simple Analogy (Easy to Remember)**:  
> A desk drawer. You are halfway through writing code, but your manager calls with an urgent production bug. You toss your half-finished work into the desk drawer (`git stash`), fix the bug on `main`, and then pull your work back out of the drawer (`git stash pop`).

### 1. `git stash` (Temporary Shelf)
* `git stash` — Saves modified working directory state and reverts to clean HEAD.
* `git stash list` — List all stashed changes.
* `git stash pop` — Re-applies the most recent stash and deletes it from stash list.
* `git stash apply` — Re-applies stash without deleting it.
* `git stash drop` — Deletes specific stash.

### 2. `git cherry-pick <commit-hash>`
* Selects a single specific commit from another branch and copies it onto your current branch.
* Ideal for backporting critical hotfixes to release branches.

### 3. Interactive Rebase (`git rebase -i HEAD~N`)
* Allows squashing multiple messy "WIP" commits into a single clean commit before merging PR:
  * `pick` — Keep commit.
  * `squash` (s) — Combine commit into previous commit.
  * `reword` (r) — Change commit message.
  * `drop` (d) — Remove commit.

---

## 8. Disaster Recovery with `git reflog`

`git reflog` is the ultimate safety net in Git. It records **every single movement of HEAD**, including deleted branches, hard resets, and rebase actions.

### Recovery Workflow
1. Run `git reflog` to view recent HEAD states:
   ```text
   b4f910a HEAD@{0}: reset: moving to HEAD~1 (Accidental hard reset!)
   8a2e12c HEAD@{1}: commit: feat: complete database schema
   ```
2. Restore your lost commit instantly:
   ```bash
   git reset --hard HEAD@{1}
   ```

---

## 9. Senior DevOps Interview Q&A

### Q1: What is the difference between `git reset --hard` and `git revert`?
* `git reset --hard` moves the branch pointer backward, rewriting history and permanently deleting intermediate commits. It should never be used on shared remote branches.
* `git revert` creates a new forward commit that undoes the changes of a previous commit, preserving historical integrity and safe for public branches.

### Q2: How does `git reflog` allow you to recover a permanently deleted branch?
* Git never immediately deletes commits from disk; it simply removes the reference pointer.
* `git reflog` retains an audit log of all HEAD pointer movements for 30–90 days. Finding the commit hash where the branch tip resided allows running `git checkout -b recovered-branch <commit-hash>`, restoring the branch completely.

### Q3: What is the difference between `git merge` and `git rebase`?
* **`git merge`**: Creates a merge commit that joins two divergent branches. Preserves exact chronological history and the context of feature branch development.
* **`git rebase`**: Takes commits from the current branch and replays them one by one on top of the target branch's latest commit. Rewrites commit hashes to produce a clean, linear, single-stream commit history without merge bubbles.
* **Golden Rule**: Never rebase commits that have been pushed to a public/shared repository.

### Q4: Explain the differences between `git reset --soft`, `--mixed`, and `--hard`.
* **`--soft`**: Moves HEAD pointer back to the specified commit. Leaves the index (Staging Area) and Working Directory untouched. All changes remain staged and ready for a new commit.
* **`--mixed` (Default)**: Moves HEAD pointer back and resets the index (Staging Area). Leaves the Working Directory untouched. Changes remain on disk as modified, unstaged files.
* **`--hard`**: Moves HEAD, clears the index, and overwrites the Working Directory to match the specified commit. All uncommitted changes and unreferenced commits are permanently discarded.

### Q5: What is a detached HEAD state in Git, and how do you fix it?
* **Cause**: Occurs when you checkout an arbitrary commit hash, tag, or remote branch directly (`git checkout a1b2c3d`) instead of a local branch name. HEAD now points directly to a commit rather than a branch reference.
* **Risk**: Any new commits created in this state will become orphaned and eligible for garbage collection (`git gc`) once you switch branches.
* **Fix**: Save work by creating a new branch directly from the current detached HEAD: `git switch -c new-feature-branch`.

### Q6: What is `git cherry-pick`, and what are its production use cases?
* `git cherry-pick <commit-hash>` applies the exact changes from a specific commit on another branch onto your current checked-out branch as a brand new commit.
* **Use Cases**:
  1. Hotfixing production: A bug fix was committed to `develop`, but production (`main`) needs that specific fix immediately without releasing other unapproved features.
  2. Recovering an accidental commit made on the wrong branch.

### Q7: How does Git store data under the hood (`.git/objects`)?
* Git is a content-addressable key-value object store. Every object is compressed with zlib and addressed by the 40-character SHA-1 (or SHA-256) hash of its contents:
  1. **Blob**: Stores raw file contents (no metadata or file names).
  2. **Tree**: Represents a directory. Stores file names, file permissions, and links to blobs or sub-trees.
  3. **Commit**: Points to a top-level Tree object, author/committer metadata, timestamp, commit message, and parent commit hash(es).
  4. **Annotated Tag**: A permanent pointer to a specific commit containing tagger name and PGP signature.

### Q8: What is `git stash` and how do you stash untracked or ignored files?
* `git stash` takes your uncommitted modifications (both staged and unstaged) and saves them on an internal LIFO stack, reverting your working directory to clean `HEAD`.
* By default, `git stash` ignores untracked files and `.gitignore` files.
* To include untracked files: `git stash -u` (or `--include-untracked`).
* To include all files including ignored build artifacts: `git stash -a` (or `--all`).

### Q9: How do you identify which commit introduced a bug using `git bisect`?
* `git bisect` uses binary search to quickly locate the exact commit that introduced a defect:
  1. Start bisect: `git bisect start`.
  2. Mark current broken state: `git bisect bad`.
  3. Mark known good commit from last week: `git bisect good <commit-hash>`.
  4. Git automatically checks out the midpoint commit. Test the application.
  5. If working, type `git bisect good`; if broken, type `git bisect bad`.
  6. Git pinpoints the offending commit in binary search steps. End with `git bisect reset`.

### Q10: How do you clean up and prune stale remote tracking branches locally?
* When teammates delete feature branches on GitHub/GitLab, your local repository still retains references (`origin/feature-xyz`).
* Run `git fetch --prune` (or `git remote prune origin`) to delete local tracking references to branches that no longer exist on the remote repository.
