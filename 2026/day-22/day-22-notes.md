# Day 22 – Introduction to Git: Your First Repository

## Objective

Today marks the beginning of my Git journey. Git is the foundation of modern software development and DevOps practices. The goal was to understand Git basics, create my first repository, build a Git command reference, and learn the Git workflow.

---

# Task 1: Install and Configure Git

## Verify Git Installation

```bash
git --version
```

Example Output:

```bash
git version 2.49.0
```

## Configure Git Identity

```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Verify Configuration

```bash
git config --list --global
```

---

# Task 2: Create Your Git Project

## Create Project Directory

```bash
mkdir devops-git-practice
cd devops-git-practice
```

## Initialize Git Repository

```bash
git init
```

## Check Repository Status

```bash
git status
```

### Output

Git shows:

* Current branch
* Tracked files
* Untracked files
* Changes ready to commit

## Explore the .git Directory

```bash
ls -la .git
```

Important folders and files:

| Item     | Purpose                  |
| -------- | ------------------------ |
| objects/ | Stores Git objects       |
| refs/    | Stores branch references |
| HEAD     | Current branch pointer   |
| config   | Repository configuration |
| hooks/   | Git automation scripts   |

---

# Task 3: Git Commands Reference

## Setup & Configuration

| Command                                  | Description            |
| ---------------------------------------- | ---------------------- |
| `git --version`                          | Check Git version      |
| `git config --global user.name "Name"`   | Set username           |
| `git config --global user.email "email"` | Set email              |
| `git config --list --global`             | View Git configuration |

### Examples

```bash
git --version
git config --global user.name "John Doe"
git config --global user.email "john@example.com"
git config --list --global
```

---

## Basic Workflow

| Command                   | Description            |
| ------------------------- | ---------------------- |
| `git init`                | Initialize repository  |
| `git add <file>`          | Stage file             |
| `git add .`               | Stage all files        |
| `git commit -m "message"` | Commit changes         |
| `git status`              | View repository status |
| `git log --oneline`       | Compact commit history |

### Examples

```bash
git init
git add git-commands.md
git commit -m "Initial commit"
git status
git log --oneline
```

---

## Viewing Changes

| Command             | Description           |
| ------------------- | --------------------- |
| `git diff`          | Show unstaged changes |
| `git diff --staged` | Show staged changes   |
| `git show <commit>` | Show commit details   |

### Examples

```bash
git diff
git diff --staged
git show a1b2c3d
```

---

# Task 4: Stage and Commit

## Stage Files

```bash
git add git-commands.md
```

## Verify Staging

```bash
git status
```

## Commit Changes

```bash
git commit -m "Add Git commands reference"
```

## View Commit History

```bash
git log
```

---

# Task 5: Build Commit History

### Commit 1

```bash
git commit -m "Add setup and configuration commands"
```

### Commit 2

```bash
git commit -m "Add basic workflow commands"
```

### Commit 3

```bash
git commit -m "Add viewing changes commands"
```

### Commit 4

```bash
git commit -m "Add day 22 notes and Git workflow explanation"
```

## Compact History

```bash
git log --oneline
```

Example:

```bash
a7c9d12 Add day 22 notes
5d3b8f7 Add viewing changes commands
c4e6a91 Add basic workflow commands
b2f1d33 Add setup commands
e1a2b3c Initial commit
```

---

# Task 6: Understanding the Git Workflow

## 1. What is the difference between git add and git commit?

`git add` moves changes from the working directory to the staging area.

`git commit` permanently saves staged changes into the repository history.

---

## 2. What does the staging area do? Why doesn't Git commit directly?

The staging area acts as a preparation zone where changes can be reviewed and organized before creating a commit.

Git does not commit directly because developers often want to include only selected changes in a commit instead of everything modified.

---

## 3. What information does git log show?

`git log` displays:

* Commit ID (SHA)
* Author name
* Author email
* Commit date
* Commit message

---

## 4. What is the .git folder and what happens if you delete it?

The `.git` folder contains all repository metadata, commit history, branches, configuration, and objects.

If it is deleted:

* Git history is lost
* Branch information is lost
* The folder is no longer a Git repository

---

## 5. What is the difference between a working directory, staging area, and repository?

### Working Directory

The place where files are actively edited.

### Staging Area

The area where selected changes are prepared for the next commit.

### Repository

The permanent Git database where commits and project history are stored.

Workflow:

```text
Working Directory
       ↓
    git add
       ↓
  Staging Area
       ↓
   git commit
       ↓
   Repository
```

---

# Key Learnings

* Git is a distributed version control system.
* Every project should be tracked using version control.
* The staging area provides control over commits.
* Commit messages should be meaningful and descriptive.
* Git history helps track project evolution.
* The `.git` directory is the heart of a repository.

---

# Commands Used Today

```bash
git --version
git config --global user.name
git config --global user.email
git config --list --global
mkdir devops-git-practice
cd devops-git-practice
git init
git status
ls -la .git
git add .
git commit -m "message"
git log
git log --oneline
git diff
git diff --staged
git show <commit>
```

---

# Conclusion

Today I created my first Git repository, learned the fundamentals of version control, explored the Git workflow, and built a personal Git command reference. This foundation will help me understand branching, merging, collaboration, and CI/CD workflows in the upcoming days of the #90DaysOfDevOps journey.
