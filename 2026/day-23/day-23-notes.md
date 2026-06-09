# Day 23 – Git Branching & Working with GitHub

## Task 1: Understanding Branches

### What is a branch in Git?

A branch in Git is an independent line of development. It allows developers to work on new features, bug fixes, or experiments without affecting the main codebase.

### Why do we use branches instead of committing everything to main?

Branches help isolate changes, reduce the risk of breaking stable code, enable parallel development, and make collaboration easier among team members.

### What is HEAD in Git?

HEAD is a pointer that references the currently checked-out branch and its latest commit. It tells Git where you are currently working.

### What happens to your files when you switch branches?

When switching branches, Git updates the working directory to match the files and commit history of the target branch. Files may appear, disappear, or change depending on the branch contents.

---

## Task 2: Branching Commands – Hands-On

### Commands Used

#### List all branches

```bash
git branch
```

#### Create a new branch

```bash
git branch feature-1
```

#### Switch to feature-1

```bash
git checkout feature-1
```

#### Create and switch in a single command

```bash
git switch -c feature-2
```

#### Switch between branches

```bash
git switch feature-1
git switch main
```

### Difference Between git switch and git checkout

| git switch                     | git checkout               |
| ------------------------------ | -------------------------- |
| Used only for branch switching | Used for multiple purposes |
| Easier and safer               | More flexible but complex  |
| Modern Git command             | Legacy command             |

### Commit Created on feature-1

```bash
echo "Feature 1 changes" >> feature1.txt
git add .
git commit -m "Added feature-1 changes"
```

### Verification

After switching back to `main`, the commit made on `feature-1` was not present, demonstrating branch isolation.

### Delete an Unused Branch

```bash
git branch -d feature-2
```

---

## Task 3: Push to GitHub

### Create GitHub Repository

A new GitHub repository was created without initializing a README file.

### Add Remote Repository

```bash
git remote add origin https://github.com/username/devops-git-practice.git
```

### Push Main Branch

```bash
git push -u origin main
```

### Push Feature Branch

```bash
git push -u origin feature-1
```

### Verification

Both `main` and `feature-1` branches were visible on GitHub after pushing.

### Difference Between Origin and Upstream

| Origin                        | Upstream                            |
| ----------------------------- | ----------------------------------- |
| Your remote repository        | Original repository you forked from |
| Default remote name           | Tracks the source repository        |
| Used for pushing your changes | Used for syncing updates            |

---

## Task 4: Pull from GitHub

### Pull Changes from GitHub

```bash
git pull origin main
```

### Difference Between git fetch and git pull

| git fetch                         | git pull                     |
| --------------------------------- | ---------------------------- |
| Downloads changes only            | Downloads and merges changes |
| Does not modify working directory | Updates local branch         |
| Safer for reviewing changes       | Faster for direct updates    |

Example:

```bash
git fetch origin
git pull origin main
```

---

## Task 5: Clone vs Fork

### Clone a Repository

```bash
git clone https://github.com/example/repository.git
```

### Fork and Clone

1. Fork repository on GitHub.
2. Clone your fork.

```bash
git clone https://github.com/yourusername/repository.git
```

### Difference Between Clone and Fork

| Clone                      | Fork                                   |
| -------------------------- | -------------------------------------- |
| Git operation              | GitHub feature                         |
| Creates local copy         | Creates remote copy under your account |
| Used for local development | Used for contributing independently    |

### When Would You Clone vs Fork?

#### Use Clone When:

* You need a local copy.
* You have direct access to the repository.
* Working within your own projects.

#### Use Fork When:

* Contributing to open-source projects.
* You don't have write access.
* You want your own GitHub copy.

### Keeping a Fork in Sync

#### Add Upstream Repository

```bash
git remote add upstream https://github.com/original-owner/repository.git
```

#### Fetch Latest Changes

```bash
git fetch upstream
```

#### Merge Updates

```bash
git checkout main
git merge upstream/main
```

#### Push Updates to Your Fork

```bash
git push origin main
```

---

# Key Learnings

* Git branches allow isolated development.
* HEAD points to the current branch and commit.
* git switch is a modern alternative to git checkout.
* origin refers to your remote repository.
* upstream refers to the original repository.
* git fetch downloads changes without merging.
* git pull downloads and merges changes.
* Clone creates a local copy.
* Fork creates your own GitHub copy.
* Branching is a fundamental workflow in Git and DevOps environments.

#90DaysOfDevOps
#DevOpsLearning
#Git
#GitHub
