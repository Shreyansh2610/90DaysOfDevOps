# Day 24 – Advanced Git: Merge, Rebase, Stash & Cherry Pick

## Overview

Today I explored advanced Git workflows used in real-world software development. I practiced merging branches, rebasing commits, stashing work-in-progress changes, squash merges, and cherry-picking specific commits.

---

# Task 1: Git Merge

## Fast-Forward Merge

Created branch:

```bash
git checkout -b feature-login
```

Added multiple commits and merged into main:

```bash
git checkout main
git merge feature-login
```

### Observation

Git performed a Fast-Forward merge because no new commits existed on `main` after the branch was created.

### What is a Fast-Forward Merge?

A fast-forward merge occurs when the target branch has not moved ahead. Git simply moves the branch pointer forward without creating a merge commit.

Example:

```text
A---B---C (main)
         \
          D---E (feature)
```

After merge:

```text
A---B---C---D---E (main)
```

---

## Merge Commit

Created branch:

```bash
git checkout -b feature-signup
```

Added commits.

Meanwhile, added a separate commit to `main`.

Merged branch:

```bash
git checkout main
git merge feature-signup
```

### Observation

Git created a merge commit because both branches had diverged.

### When does Git create a merge commit?

When both branches contain unique commits and Git needs to preserve both histories.

Example:

```text
      D---E
     /
A---B---C
     \
      F
```

After merge:

```text
      D---E
     /     \
A---B---C---M
     \
      F
```

---

## Merge Conflict

Modified the same line in the same file on two branches.

During merge Git displayed:

```text
CONFLICT (content): Merge conflict in file.txt
```

### What is a Merge Conflict?

A merge conflict occurs when Git cannot automatically determine which change should be kept because the same section of code was modified differently in multiple branches.

Conflict markers:

```text
<<<<<<< HEAD
Main branch change
=======
Feature branch change
>>>>>>> feature-branch
```

---

# Task 2: Git Rebase

Created branch:

```bash
git checkout -b feature-dashboard
```

Added multiple commits.

Added another commit to main.

Rebased:

```bash
git checkout feature-dashboard
git rebase main
```

---

## What does rebase do?

Rebase takes commits from the current branch and replays them on top of another branch.

Instead of creating a merge commit, Git rewrites commit history.

### Before Rebase

```text
A---B---C (main)
     \
      D---E (feature)
```

### After Rebase

```text
A---B---C---D'---E'
```

---

## How is history different from merge?

### Merge

Preserves complete branch history.

```text
      D---E
     /     \
A---B---C---M
```

### Rebase

Creates a cleaner linear history.

```text
A---B---C---D'---E'
```

---

## Why should you never rebase shared commits?

Rebase changes commit hashes.

If others have already pulled those commits, rebasing causes history divergence and collaboration problems.

---

## When to use Rebase vs Merge?

### Use Rebase

* Before creating a pull request
* To maintain clean history
* For local feature branches

### Use Merge

* For shared branches
* When preserving historical context is important
* Team collaboration workflows

---

# Task 3: Squash Merge vs Regular Merge

Created branch:

```bash
git checkout -b feature-profile
```

Added 5 small commits.

Merged using:

```bash
git merge --squash feature-profile
git commit
```

---

## Observation

Only one commit was added to main.

---

## What does squash merge do?

Combines all branch commits into a single commit before merging.

### Example

Before:

```text
A---B---C---D---E
```

After squash:

```text
A---S
```

Where `S` contains all changes.

---

## Regular Merge

Created another branch:

```bash
git checkout -b feature-settings
```

Added multiple commits.

Merged normally:

```bash
git merge feature-settings
```

All commits remained visible in history.

---

## Squash Merge vs Regular Merge

### Squash Merge

Advantages:

* Cleaner history
* Easier review
* One commit per feature

### Regular Merge

Advantages:

* Preserves detailed development history
* Easier debugging of individual commits

### Trade-off

Squashing loses commit-by-commit history.

---

# Task 4: Git Stash

Modified files without committing.

Attempted branch switch.

Used:

```bash
git stash
```

Switched branches successfully.

Returned and restored changes:

```bash
git stash pop
```

---

## Multiple Stashes

Create stash with message:

```bash
git stash push -m "UI changes"
git stash push -m "API work"
```

List stashes:

```bash
git stash list
```

Apply specific stash:

```bash
git stash apply stash@{1}
```

---

## Difference Between Pop and Apply

### git stash pop

* Applies stash
* Removes stash from list

### git stash apply

* Applies stash
* Keeps stash in list

---

## Real-World Use Cases

* Urgent bug fixes
* Context switching
* Temporary experiments
* Pulling latest changes before finishing work

---

# Task 5: Cherry Pick

Created branch:

```bash
git checkout -b feature-hotfix
```

Added 3 commits.

Selected second commit hash:

```bash
git log --oneline
```

Applied only that commit:

```bash
git checkout main
git cherry-pick <commit-hash>
```

---

## What does Cherry-Pick do?

Copies a specific commit from one branch and applies it to another branch.

---

## Real-World Use Cases

* Applying hotfixes to production
* Backporting bug fixes
* Selecting only required changes from a feature branch

---

## What can go wrong?

* Merge conflicts
* Duplicate commits
* Loss of context
* Difficult history tracking

---

# Useful Commands Learned

```bash
git merge branch-name

git merge --squash branch-name

git rebase main

git log --oneline --graph --all

git stash

git stash push -m "message"

git stash list

git stash apply

git stash pop

git cherry-pick <commit-hash>
```

---

# Key Takeaways

* Merge combines histories.
* Rebase rewrites history into a linear sequence.
* Squash merge creates a clean single commit.
* Stash temporarily stores uncommitted work.
* Cherry-pick copies specific commits between branches.
* Understanding these workflows is essential for professional Git usage and team collaboration.
