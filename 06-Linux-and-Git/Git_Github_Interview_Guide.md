# 📖 Git Github Interview Guide
> *Converted from `Git Github Interview Guide.pdf` for high-readability on GitHub.*

---
## Page 1

Git & GitHub Interview Questions, Answers, and Commands
Git & GitHub Interview Questions & Answers
Basic Questions
What is Git?  Git is a distributed version control system that tracks changes in source code during
software development.
What  is  GitHub? GitHub  is  a  cloud-based  platform  that  hosts  Git  repositories  and  provides
collaboration features like pull requests, issues, and project management.
Difference between Git and GitHub  | Feature | Git | GitHub | |---------|-----|--------| | Type | VCS
(tool) | Hosting service | | Usage | Local repo | Remote repo | | Features | Branching, commits |
Pull requests, issues |
What is a repository (repo)?  A repository is a directory containing project files, history of commits,
and versioning data.
What is a commit in Git?  A commit is a snapshot of changes in the repository with a message and
author info.
What is a branch?  A branch is a separate line of development in Git. Master/main is the default
branch.
Difference between git pull and git fetch  | Command | Description | |---------|-------------| | git
fetch | Retrieves updates from remote repo without merging | | git pull | Fetches and merges
updates with local branch |
What is a merge conflict? Occurs when Git cannot automatically reconcile differences between two
branches.
Fork vs Clone  | Term | Description | |------|-------------| | Fork | Copy of someone else’s repo on
GitHub | | Clone | Local copy of a repo (remote or forked) |
What is a pull request?  Request to merge your branch into another branch on GitHub. Supports
code review and approval.
Intermediate Questions
Git merge vs Git rebase
Merge: Combines branches preserving history.
1. 
2. 
3. 
4. 
5. 
6. 
7. 
8. 
9. 
10. 
1. 
2. 
1

## Page 2

Rebase: Moves branch commits onto another branch creating linear history.
Undo a commit
git reset --soft HEAD~1 → undo commit, keep staged changes
git reset --hard HEAD~1 → undo commit, discard changes
Check repo status
git status
View commit history
git log
Discard changes in a file
git checkout -- filename
Git tag Reference to a specific commit, used for marking releases.
git clone vs git init  | Command | Description | |---------|-------------| | git clone | Copies an existing
repo from remote | | git init | Initializes a new local repo |
git pull vs git merge | git pull | git merge | |-----------|-----------| | Fetch + merge | Only merges local
branches |
Revert a commit
git revert <commit-id>
.gitignore Specifies files/folders Git should ignore (e.g., logs, temp files).
3. 
4. 
5. 
6. 
7. 
8. 
9. 
10. 
11. 
12. 
13. 
14. 
2

## Page 3

Git Commands
Local Repository Commands
Command Description
git init Initialize a new local repository
git clone <repo_url> Clone a remote repository
git add <file> Stage changes for commit
git add . Stage all changes in directory
git commit -m "message" Commit staged changes
git status Check working directory status
git log View commit history
git log --oneline Compact commit history
git diff Show unstaged changes
git diff --staged Show staged changes
git branch List branches
git branch <branch_name> Create a branch
git checkout <branch_name> Switch branch
git checkout -b <branch_name> Create and switch branch
git merge <branch> Merge branch into current branch
git reset --soft HEAD~1 Undo last commit, keep staged
git reset --hard HEAD~1 Undo last commit, discard changes
git revert <commit_id> Revert changes of a commit
git stash Save uncommitted changes temporarily
git stash pop Apply stashed changes
git rm <file> Remove file from repo and staging
git mv <old> <new> Rename/move a file
git tag <tag_name> Create a tag
git log --graph --oneline --all Visualize branches & merges
3

## Page 4

Remote Repository Commands
Command Description
git remote -v Show remote repositories
git remote add <name> <url> Add a new remote
git remote remove <name> Remove remote repository
git remote rename <old> <new> Rename remote repository
git push <remote> <branch> Push commits to remote branch
git push -u <remote> <branch> Push branch and set upstream
git push --all <remote> Push all branches to remote
git push --tags Push all tags to remote
git fetch <remote> Fetch changes without merging
git pull <remote> <branch> Fetch and merge changes from remote
git pull --rebase <remote> <branch> Rebase local changes on remote branch
git branch -r List remote branches
git branch -a List all branches (local + remote)
git checkout <remote>/<branch> Checkout remote branch locally
Other Useful Commands
Command Description
git show <commit_id> Show commit details
git log -p Show commit diffs
git clean -f Remove untracked files
git reflog Show history of HEAD movements
git shortlog Summarize commits by author
git blame <file> Show who modified each line
git config --global user .name "Name" Set Git username
git config --global user .email "Email" Set Git email
git config --list Show all Git configurations
4

