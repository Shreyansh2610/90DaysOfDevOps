# Day 25 – Git Reset vs Revert & Branching Strategies

## Task 1: Git Reset — Hands-On

### Setup

Created three commits:

```bash
echo "Commit A" > reset-demo.txt
git add .
git commit -m "Commit A"

echo "Commit B" >> reset-demo.txt
git add .
git commit -m "Commit B"

echo "Commit C" >> reset-demo.txt
git add .
git commit -m "Commit C"
```

---

### 1. git reset --soft HEAD~1

```bash
git reset --soft HEAD~1
```

#### Observation

* Commit C was removed from history.
* Changes from Commit C remained staged.
* `git status` showed changes ready to commit.

#### Use Case

Useful when you want to modify the previous commit message or combine commits.

---

### 2. git reset --mixed HEAD~1

Re-created Commit C and executed:

```bash
git reset --mixed HEAD~1
```

#### Observation

* Commit C was removed from history.
* Changes remained in the working directory.
* Changes were unstaged.

#### Use Case

Useful when you want to rework files before committing again.

---

### 3. git reset --hard HEAD~1

Re-created Commit C and executed:

```bash
git reset --hard HEAD~1
```

#### Observation

* Commit C was removed from history.
* Changes were deleted from both staging area and working directory.
* Repository returned exactly to the previous commit state.

#### Use Case

Useful when unwanted changes should be discarded completely.

---

### Answers

#### What is the difference between --soft, --mixed, and --hard?

| Mode    | Commit History | Staging Area | Working Directory |
| ------- | -------------- | ------------ | ----------------- |
| --soft  | Reset          | Preserved    | Preserved         |
| --mixed | Reset          | Cleared      | Preserved         |
| --hard  | Reset          | Cleared      | Deleted           |

#### Which one is destructive and why?

`git reset --hard`

Because it permanently removes uncommitted changes from the working directory.

#### When would you use each one?

* **Soft** → Rewrite recent commits.
* **Mixed** → Unstage changes while keeping files.
* **Hard** → Completely discard changes.

#### Should you ever use git reset on commits that are already pushed?

Generally **No**.

Rewriting public history can break collaborators' repositories and create merge conflicts.

---

## Task 2: Git Revert — Hands-On

### Setup

Created commits:

```bash
git commit -m "Commit X"
git commit -m "Commit Y"
git commit -m "Commit Z"
```

### Revert Commit Y

```bash
git revert <commit-hash-of-Y>
```

### Observation

* Git created a new commit that reversed the changes introduced by Commit Y.
* Commit Y remained in history.
* A new "Revert" commit appeared in git log.

### Answers

#### How is git revert different from git reset?

* Reset moves branch pointers and can remove commits from visible history.
* Revert creates a new commit that undoes previous changes.

#### Why is revert considered safer than reset for shared branches?

Because it preserves history and does not rewrite commits already shared with others.

#### When would you use revert vs reset?

**Revert**

* Shared branches
* Production fixes
* Public repositories

**Reset**

* Local branches
* Cleaning up commit history before pushing

---

## Task 3: Reset vs Revert Comparison

| Feature                      | git reset                     | git revert             |
| ---------------------------- | ----------------------------- | ---------------------- |
| What it does                 | Moves branch pointer backward | Creates inverse commit |
| Removes commit from history? | Yes                           | No                     |
| Safe for shared branches?    | No                            | Yes                    |
| Rewrites history?            | Yes                           | No                     |
| Typical use                  | Local cleanup                 | Undo public changes    |

---

# Task 4: Branching Strategies

## 1. GitFlow

### How It Works

Uses multiple long-lived branches:

* main
* develop
* feature/*
* release/*
* hotfix/*

### Flow

```text
main
 │
 ├── develop
      ├── feature/login
      ├── feature/payment
      └── feature/profile

release/v1.0
      │
      ▼
     main

hotfix/security-fix
      │
      ▼
     main
```

### Used In

* Enterprise software
* Products with scheduled releases

### Pros

* Structured workflow
* Clear release management
* Stable production branch

### Cons

* Complex
* Many merges
* Slower delivery

---

## 2. GitHub Flow

### How It Works

Single production branch:

```text
main
 │
 ├── feature-a
 ├── feature-b
 └── feature-c
```

Changes are merged through Pull Requests.

### Used In

* SaaS products
* Continuous deployment teams

### Pros

* Simple
* Easy to learn
* Fast delivery

### Cons

* Less control over release cycles
* Requires strong CI/CD

---

## 3. Trunk-Based Development

### How It Works

Developers commit directly to trunk/main or use very short-lived branches.

```text
main
 ├── small feature
 ├── bug fix
 ├── refactor
 └── deploy
```

### Used In

* Google
* High-performance engineering teams

### Pros

* Fast integration
* Fewer merge conflicts
* Supports continuous delivery

### Cons

* Requires excellent automated testing
* Demands disciplined developers

---

## Answers

### Which strategy would you use for a startup shipping fast?

**GitHub Flow**

Reason:

* Simple workflow
* Fast releases
* Works well with CI/CD

### Which strategy would you use for a large team with scheduled releases?

**GitFlow**

Reason:

* Better release planning
* Supports multiple environments
* Strong control over production releases

### Which one does your favorite open-source project use?

Example: React

* Uses a variation of Trunk-Based Development.
* Most work happens through short-lived branches and pull requests into the main branch.

---

# Task 5: Git Commands Reference Update

## Setup & Config

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
git init
```

## Basic Workflow

```bash
git status
git add .
git commit -m "message"
git log
git diff
```

## Branching

```bash
git branch
git branch feature-x
git switch feature-x
git checkout feature-x
git merge feature-x
```

## Remote

```bash
git remote -v
git clone <url>
git fetch
git pull
git push origin main
```

## Merge & Rebase

```bash
git merge branch-name
git rebase main
```

## Stash & Cherry Pick

```bash
git stash
git stash pop
git cherry-pick <commit>
```

## Reset & Revert

```bash
git reset --soft HEAD~1
git reset --mixed HEAD~1
git reset --hard HEAD~1
git revert <commit>
git reflog
```

---

## Key Learnings

* Reset rewrites history.
* Revert preserves history.
* Hard reset is destructive.
* Reflog can recover seemingly lost commits.
* GitHub Flow is ideal for fast-moving teams.
* GitFlow suits structured release cycles.
* Trunk-Based Development maximizes integration speed.
