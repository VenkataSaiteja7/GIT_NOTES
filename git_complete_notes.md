# Comprehensive Git Guide

## 1. Introduction to Git

### What is Git?
Git is a distributed version control system that tracks changes in source code during software development. It was created by Linus Torvalds in 2005 for Linux kernel development.

### Why is Git important?
- **History tracking**: Records all changes to files
- **Collaboration**: Multiple developers can work simultaneously
- **Branching**: Allows parallel development paths
- **Distributed**: Each developer has a complete copy of the repository
- **Backup**: Multiple copies exist across different machines

```
┌────────────────┐     ┌────────────────┐     ┌────────────────┐
│  Developer A   │     │  Developer B   │     │  Developer C   │
│  Repository    │◄───►│  Repository    │◄───►│  Repository    │
└────────────────┘     └────────────────┘     └────────────────┘
         ▲                      ▲                     ▲
         │                      │                     │
         └──────────────┬──────┴─────────────────────┘
                        │
                        ▼
              ┌────────────────────┐
              │  Remote Repository │
              │  (GitHub/GitLab)   │
              └────────────────────┘
```

## 2. Git Basics

### Key Concepts

#### Repository (Repo)
A repository is a storage location for your project, containing all files and the history of changes.

**Example - Initialize a new repository:**
```bash
git init
```

#### Working Directory
The directory on your filesystem where your project files are located.

#### Staging Area (Index)
A space where changes are prepared before committing them to the repository.

**Example - Add files to staging area:**
```bash
git add filename.txt    # Add specific file
git add .               # Add all changes
```

#### Commits
Snapshots of your project at a specific point in time. Each commit has a unique identifier.

**Example - Create a commit:**
```bash
git commit -m "Add login functionality"
```

#### Branches
Separate lines of development that allow you to work on different features simultaneously.

**Example - Create and switch to a new branch:**
```bash
git branch feature-login    # Create branch
git checkout feature-login  # Switch to branch
# OR
git checkout -b feature-login  # Create and switch in one command
```

#### Basic Git Workflow Diagram
```
┌───────────────┐     ┌───────────────┐     ┌───────────────┐
│  Working      │     │  Staging      │     │  Repository   │
│  Directory    │────►│  Area (Index) │────►│  (Commits)    │
└───────────────┘     └───────────────┘     └───────────────┘
       git add             git commit
```

## 3. Git Commands

### Setup and Configuration
```bash
# Set your username and email
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# View configuration settings
git config --list
```

### Starting a Repository
```bash
# Initialize a new repository
git init

# Clone an existing repository
git clone https://github.com/username/repository.git
git clone https://github.com/username/repository.git my-folder  # Clone to specific folder
```

### Basic Workflow Commands
```bash
# Check repository status
git status

# Add files to staging area
git add filename.txt  # Add specific file
git add .             # Add all files
git add *.js          # Add all JavaScript files

# Commit changes
git commit -m "Commit message"
git commit -am "Commit message"  # Add and commit tracked files in one command

# View commit history
git log
git log --oneline     # Compact view
git log --graph       # Graphical representation
```

### Working with Remote Repositories
```bash
# Add a remote repository
git remote add origin https://github.com/username/repository.git

# View remote repositories
git remote -v

# Fetch changes from remote
git fetch origin

# Pull changes (fetch + merge)
git pull origin main

# Push changes to remote
git push origin main
git push -u origin main  # Set upstream and push
```

### Branching and Merging
```bash
# List branches
git branch            # Local branches
git branch -r         # Remote branches
git branch -a         # All branches

# Create branch
git branch branch-name

# Switch branch
git checkout branch-name
git switch branch-name  # Git 2.23+

# Create and switch in one command
git checkout -b branch-name
git switch -c branch-name  # Git 2.23+

# Merge branch into current branch
git merge branch-name

# Delete branch
git branch -d branch-name  # Safe delete
git branch -D branch-name  # Force delete
```

## 4. Branching and Merging

### Branching Strategies
Branches allow you to develop features, fix bugs, or experiment without affecting the main codebase.

#### Branch Types
- **Main/Master**: Stable, production-ready code
- **Development**: Integration branch for features
- **Feature**: Specific functionality development
- **Release**: Preparing for a new release
- **Hotfix**: Urgent fixes for production issues

#### Branching Workflow Diagram
```
            ┌───► feature-1 ───┐
            │                   │
            │                   ▼
main ───────┼───────────────────┬──────► main
            │                   ▲
            │                   │
            └───► feature-2 ───┘
```

### Merging
Combining changes from one branch into another.

**Fast-forward Merge**: When there are no new changes in the target branch.
```
Before:          After:
    main             main
      │                │
      │                ▼
      └─► feature      feature
```

**Three-way Merge**: When both branches have unique commits.
```
Before:                 After:
     main                 main
      │                    │
      ├─────                ▼
      │    │          ┌────┴───┐
      │    │          │ Merge  │
      │    │          │ Commit │
      ▼    │          └────┬───┘
      │    │               │
      │    ▼               │
      └─► feature ─────────┘
```

**Example - Merge a feature branch:**
```bash
git checkout main      # Switch to target branch
git merge feature      # Merge feature into main
```

### Merge Conflicts
Conflicts occur when Git can't automatically merge changes.

**Example - Resolving a merge conflict:**
```bash
# After a merge conflict occurs:
git status                  # See conflicted files
# Edit files to resolve conflicts
git add resolved-file.txt   # Mark as resolved
git commit                  # Complete the merge
```

**Conflict Markers Example:**
```
<<<<<<< HEAD
This is the current branch content
=======
This is the incoming branch content
>>>>>>> feature-branch
```

## 5. Remote Repositories

### Working with Remote Repositories

#### Setting Up Remote Repositories
```bash
# Add a remote repository
git remote add origin https://github.com/username/repo.git

# View remote repositories
git remote -v

# Change remote URL
git remote set-url origin https://github.com/username/new-repo.git
```

#### Synchronizing with Remotes
```bash
# Fetch remote changes (without merging)
git fetch origin

# Pull changes (fetch + merge)
git pull origin main

# Push local changes to remote
git push origin main

# Push all local branches
git push --all origin

# Set upstream branch and push
git push -u origin feature-branch
```

#### Remote Repository Workflow
```
┌─────────────────┐                    ┌─────────────────┐
│  Local          │                    │  Remote         │
│  Repository     │◄───── push ───────►│  Repository     │
└─────────────────┘                    └─────────────────┘
        ▲                                      │
        │                                      │
        └─────────── pull/fetch ───────────────┘
```

## 6. Git Workflows

### Feature Branch Workflow
Each feature is developed in its own branch and merged back to the main branch when complete.

```
┌─── feature-1 ────┐
│                  │
main ──┼───────────┬─── main
       │           │
       └─── bug-fix ┘
```

**Example:**
```bash
git checkout -b feature-login
# Make changes
git add .
git commit -m "Implement login functionality"
git push -u origin feature-login
# Create pull request
git checkout main
git pull
git merge feature-login
git push
```

### Gitflow Workflow
A branching model with specific branches for features, releases, and hotfixes.

```
        ┌─── feature-1 ─┐
        │               │
develop ┼───────────────┼─── develop
        │               │     │
        └─── feature-2 ─┘     │
                              │
                              ▼
                         release-1.0 ─┐
                              │       │
                              │       │
main ─────────────────────────┴───────┴─── main
                                      ▲
                                      │
                                  hotfix-1.0.1
```

**Example commands:**
```bash
# Start a feature
git checkout develop
git checkout -b feature-x
# Complete feature
git checkout develop
git merge feature-x

# Start a release
git checkout develop
git checkout -b release-1.0
# Finalize release
git checkout main
git merge release-1.0
git checkout develop
git merge release-1.0
git tag -a v1.0 -m "Version 1.0"

# Create hotfix
git checkout main
git checkout -b hotfix-1.0.1
# Complete hotfix
git checkout main
git merge hotfix-1.0.1
git checkout develop
git merge hotfix-1.0.1
git tag -a v1.0.1 -m "Version 1.0.1"
```

### Forking Workflow
Common in open-source projects, where developers fork the main repository and submit pull requests.

```
┌────────────────┐     ┌────────────────┐
│  Main Repo     │     │  Forked Repo   │
│  (Original)    │◄────│  (Your Copy)   │
└────────────────┘     └────────────────┘
        ▲                     │
        │                     │
        │                     ▼
        │              ┌────────────────┐
        └──────────────│  Local Clone   │
                       └────────────────┘
```

**Example:**
```bash
# Fork the repository on GitHub/GitLab

# Clone your fork
git clone https://github.com/your-username/repo.git

# Add original repository as upstream
git remote add upstream https://github.com/original-owner/repo.git

# Keep fork updated
git fetch upstream
git merge upstream/main

# Create and push changes
git checkout -b feature-x
# Make changes
git push origin feature-x
# Create pull request from GitHub/GitLab interface
```

## 7. Git Rebase vs. Git Merge

### Git Merge
- Creates a new "merge commit" that combines changes from both branches
- Preserves complete history and chronological order
- Non-destructive operation (doesn't change existing commits)

```
Before:              After merge:
A---B---C (main)     A---B---C---M (main)
     \                     \     /
      D---E (feature)       D---E (feature)
```

**Example:**
```bash
git checkout main
git merge feature
```

### Git Rebase
- Moves the entire feature branch to begin on the tip of the main branch
- Creates new commits for each commit in the original branch
- Results in a linear project history
- Rewrites project history (potentially problematic for shared branches)

```
Before:              After rebase:
A---B---C (main)     A---B---C (main)
     \                     \
      D---E (feature)       D'---E' (feature)
```

**Example:**
```bash
git checkout feature
git rebase main
```

### When to Use Each
- **Use Merge When:**
  - You want to preserve the complete history
  - The branch is shared with other developers
  - You want to maintain context of a feature branch

- **Use Rebase When:**
  - You want a clean, linear history
  - The branch is private to you
  - You want to integrate upstream changes before pushing

## 8. Undoing Changes

### Unstaging Files
Undo adding files to the staging area:
```bash
git reset HEAD filename.txt
git restore --staged filename.txt  # Git 2.23+
```

### Discarding Changes in Working Directory
Discard changes in your working directory:
```bash
git checkout -- filename.txt  # Pre Git 2.23
git restore filename.txt      # Git 2.23+
```

### Modifying the Last Commit
Modify the last commit message or add changes to it:
```bash
git commit --amend -m "New commit message"
git commit --amend --no-edit  # Keep same message
```

### Reset Commits
Move the branch pointer backward to undo commits:

**Soft Reset** - Keep changes in staging area:
```bash
git reset --soft HEAD~1  # Undo last commit
```

**Mixed Reset** - Keep changes in working directory:
```bash
git reset HEAD~1         # Undo last commit
git reset --mixed HEAD~1 # Same as above
```

**Hard Reset** - Discard all changes:
```bash
git reset --hard HEAD~1  # Warning: Destructive!
```

```
                  HEAD~2    HEAD~1     HEAD
                    ▼         ▼         ▼
Commit History:  ... C ──────► D ──────► E
                              ▲
                 git reset HEAD~1
```

### Reverting Commits
Create a new commit that undoes changes in a previous commit:
```bash
git revert HEAD        # Revert the last commit
git revert abc123      # Revert a specific commit
```

### Recovering Deleted Commits
Find and restore commits that are no longer referenced:
```bash
# Find dangling commits
git reflog

# Restore a commit
git checkout abc123
git checkout -b recovered-branch
```

## 9. Git Tags

### What are Git Tags?
Tags are references to specific points in Git history, used to mark release points (v1.0, v2.0, etc.).

### Types of Tags
- **Lightweight tags**: Simple pointers to commits
- **Annotated tags**: Full objects containing tagger name, email, date, and a message

### Working with Tags
```bash
# Create a lightweight tag
git tag v1.0

# Create an annotated tag
git tag -a v1.0 -m "Version 1.0 release"

# List tags
git tag
git tag -l "v1.*"  # List with pattern

# View tag information
git show v1.0

# Tag a specific commit
git tag -a v0.9 abc123 -m "Version 0.9 release"

# Push tags to remote
git push origin v1.0
git push origin --tags  # Push all tags

# Delete a tag
git tag -d v1.0

# Delete remote tag
git push origin --delete v1.0
```

## 10. Best Practices

### Commit Messages
Write clear, descriptive commit messages:

```
feat: Add login authentication system

- Implement OAuth2 authentication
- Add user login form
- Create login API endpoints
- Store user sessions
```

**Guidelines:**
- Use the imperative mood ("Add feature" not "Added feature")
- First line: concise summary (50 chars or less)
- Leave a blank line after the summary
- Body: detailed explanation (wrap at 72 chars)
- Explain what and why, not how

### Branching Strategy
- Keep the main branch stable and deployable
- Use feature branches for development
- Delete branches after merging
- Use descriptive branch names (e.g., `feature/user-authentication`, `bugfix/login-error`)

### Pull Requests
- Keep PRs small and focused on a single issue
- Include a clear description of changes
- Reference related issues
- Add screenshots or GIFs for UI changes
- Request reviews from appropriate team members

### .gitignore
Create a proper `.gitignore` file to exclude:
- Build artifacts and compiled code
- Dependencies and package directories
- Environment and configuration files with secrets
- System files and editor-specific files
- Log files and databases

**Example `.gitignore` for a Node.js project:**
```
# Dependencies
node_modules/
npm-debug.log
yarn-error.log

# Build
dist/
build/
.next/

# Environment variables
.env
.env.local
.env.*.local

# OS files
.DS_Store
Thumbs.db

# IDE files
.idea/
.vscode/
*.sublime-project
*.sublime-workspace
```

## 11. Troubleshooting

### Common Issues and Solutions

#### "Cannot pull with rebase: You have unstaged changes."
```bash
# Option 1: Stash changes
git stash
git pull --rebase
git stash pop

# Option 2: Commit changes
git commit -m "WIP: Saving changes before pull"
git pull --rebase
```

#### Detached HEAD state
```bash
# Check which commit you're on
git log -n 1

# Create a branch to save your work
git checkout -b recovery-branch

# Return to a branch
git checkout main
```

#### Accidentally committed to wrong branch
```bash
# Undo the last commit, but keep changes
git reset HEAD~1

# Stash the changes
git stash

# Switch to correct branch
git checkout correct-branch

# Apply stashed changes
git stash pop

# Commit to correct branch
git commit -m "Your message"
```

#### Accidentally pushed sensitive information
```bash
# Remove the file from Git but keep it locally
git rm --cached sensitive_file.txt

# Commit the removal
git commit -m "Remove sensitive file"

# Push the change
git push

# Update .gitignore to prevent future accidents
echo "sensitive_file.txt" >> .gitignore
git add .gitignore
git commit -m "Update .gitignore to exclude sensitive files"
git push
```

#### Merge conflict resolution
```bash
# During a merge with conflicts:
git status  # See which files have conflicts

# Open files and look for conflict markers:
# <<<<<<< HEAD
# Current branch content
# =======
# Incoming branch content
# >>>>>>> feature-branch

# After resolving:
git add resolved-file.txt
git commit  # Or git merge --continue
```

#### Large files rejected by remote
```bash
# For current commit
git filter-branch --tree-filter 'rm -f large-file.zip' HEAD

# For entire history
git filter-branch --tree-filter 'rm -f large-file.zip' --all

# Consider using Git LFS for large files
git lfs install
git lfs track "*.zip"
git add .gitattributes
```

### Git Command Cheat Sheet
```
┌──────────────────────────────────────────────────────────┐
│                   GIT COMMAND REFERENCE                   │
├────────────────────┬─────────────────────────────────────┤
│ SETUP              │ WORKING WITH CHANGES                │
├────────────────────┼─────────────────────────────────────┤
│ git init           │ git status                          │
│ git clone URL      │ git add file                        │
│ git config         │ git add .                           │
├────────────────────┼─────────────────────────────────────┤
│ BRANCHES           │ HISTORY                             │
├────────────────────┼─────────────────────────────────────┤
│ git branch         │ git log                             │
│ git checkout       │ git log --graph                     │
│ git switch         │ git blame file                      │
│ git merge branch   │ git diff                            │
│ git rebase branch  │                                     │
├────────────────────┼─────────────────────────────────────┤
│ REMOTE             │ UNDOING                             │
├────────────────────┼─────────────────────────────────────┤
│ git remote -v      │ git restore file                    │
│ git fetch origin   │ git reset HEAD~1                    │
│ git pull origin    │ git revert commit                   │
│ git push origin    │ git commit --amend                  │
├────────────────────┼─────────────────────────────────────┤
│ COLLABORATION      │ TEMPORARY                           │
├────────────────────┼─────────────────────────────────────┤
│ git tag v1.0       │ git stash                           │
│ git fetch          │ git stash list                      │
│ git fork           │ git stash pop                       │
│ git request-pull   │ git stash apply                     │
└────────────────────┴─────────────────────────────────────┘
```

---

## Additional Resources
- [Official Git Documentation](https://git-scm.com/doc)
- [Git Book](https://git-scm.com/book)
- [GitHub Learning Lab](https://lab.github.com/)
- [Atlassian Git Tutorials](https://www.atlassian.com/git/tutorials)
- [Interactive Git Visualization Tool](https://git-school.github.io/visualizing-git/) 