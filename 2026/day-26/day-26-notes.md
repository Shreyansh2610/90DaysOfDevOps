# Day 26 – GitHub CLI: Manage GitHub from Your Terminal

## What I Learned

GitHub CLI (`gh`) allows developers and DevOps engineers to interact with GitHub directly from the terminal. It reduces context switching between the browser and terminal, making repository management, pull requests, issues, and workflow automation faster and more efficient.

---

# Task 1: Install and Authenticate

## Commands Used

### Check Version

```bash
gh --version
```

### Login to GitHub

```bash
gh auth login
```

### Verify Authentication

```bash
gh auth status
```

### Logout

```bash
gh auth logout
```

## What Authentication Methods Does gh Support?

GitHub CLI supports multiple authentication methods:

1. Browser-based OAuth authentication
2. Personal Access Token (PAT)
3. SSH authentication
4. GitHub Enterprise authentication

The recommended method is browser-based authentication or fine-grained Personal Access Tokens.

---

# Task 2: Working with Repositories

## Create a New Public Repository

```bash
gh repo create gh-cli-demo \
  --public \
  --clone \
  --add-readme
```

## Clone a Repository

```bash
gh repo clone owner/repository-name
```

## View Repository Details

```bash
gh repo view owner/repository-name
```

## List All Repositories

```bash
gh repo list
```

## Open Repository in Browser

```bash
gh repo view --web
```

## Delete Repository

```bash
gh repo delete gh-cli-demo --yes
```

### Observation

Using `gh repo` commands eliminates the need to navigate GitHub's web interface for common repository operations.

---

# Task 3: Issues

## Create an Issue

```bash
gh issue create \
  --title "Sample Bug Report" \
  --body "Description of the issue" \
  --label bug
```

## List Open Issues

```bash
gh issue list
```

## View a Specific Issue

```bash
gh issue view 1
```

## Close an Issue

```bash
gh issue close 1
```

## How Could You Use gh issue in Scripts or Automation?

The `gh issue` command can be integrated into automation workflows to:

* Create issues when CI/CD pipelines fail
* Automatically report deployment errors
* Generate maintenance tickets
* Close issues after successful fixes
* Send issue reports to Slack or Teams
* Create incident tickets from monitoring systems

Using `--json` output allows issue data to be consumed by scripts and automation tools.

---

# Task 4: Pull Requests

## Create a Branch

```bash
git checkout -b feature/update-readme
```

## Make Changes and Commit

```bash
git add .
git commit -m "Update README"
```

## Push Branch

```bash
git push origin feature/update-readme
```

## Create Pull Request

```bash
gh pr create --fill
```

## List Pull Requests

```bash
gh pr list
```

## View Pull Request

```bash
gh pr view 1
```

## Check PR Status

```bash
gh pr checks 1
```

## Merge Pull Request

```bash
gh pr merge 1 --merge
```

## What Merge Methods Does gh pr merge Support?

### Merge Commit

```bash
gh pr merge --merge
```

Creates a merge commit.

### Squash Merge

```bash
gh pr merge --squash
```

Combines all commits into a single commit.

### Rebase Merge

```bash
gh pr merge --rebase
```

Rebases commits onto the target branch.

### Delete Branch After Merge

```bash
gh pr merge --delete-branch
```

Deletes the source branch after merging.

## How Would You Review Someone Else's PR Using gh?

### Checkout PR Locally

```bash
gh pr checkout 15
```

### View PR Details

```bash
gh pr view 15
```

### View Changes

```bash
gh pr diff 15
```

### Approve PR

```bash
gh pr review 15 --approve
```

### Request Changes

```bash
gh pr review 15 --request-changes --body "Please fix issues."
```

### Leave Comment

```bash
gh pr review 15 --comment --body "Looks good overall."
```

---

# Task 5: GitHub Actions & Workflows (Preview)

## List Workflow Runs

```bash
gh run list
```

## View Workflow Run Details

```bash
gh run view RUN_ID
```

## Watch Workflow Progress

```bash
gh run watch RUN_ID
```

## List Available Workflows

```bash
gh workflow list
```

## View Workflow Information

```bash
gh workflow view WORKFLOW_NAME
```

## How Could gh run and gh workflow Be Useful in CI/CD?

These commands allow engineers to:

* Monitor pipeline execution
* Check deployment status
* Debug failed workflows
* Trigger workflows manually
* Automate release processes
* Integrate workflow status into monitoring systems
* Build deployment dashboards

This is particularly useful for DevOps teams managing multiple repositories and pipelines.

---

# Task 6: Useful gh Tricks

## GitHub API Calls

```bash
gh api user
```

```bash
gh api repos/OWNER/REPO/issues
```

---

## GitHub Gists

### Create Gist

```bash
gh gist create notes.txt
```

### List Gists

```bash
gh gist list
```

---

## GitHub Releases

### Create Release

```bash
gh release create v1.0.0
```

### List Releases

```bash
gh release list
```

---

## Create Aliases

### Create Alias

```bash
gh alias set co pr checkout
```

### Use Alias

```bash
gh co 15
```

---

## Search Repositories

```bash
gh search repos "laravel"
```

```bash
gh search repos "language:go stars:>5000"
```

---

# Key Takeaways

* GitHub CLI enables full GitHub management from the terminal.
* Repository, issue, and pull request workflows can be completed without a browser.
* GitHub CLI is automation-friendly through JSON outputs and API integration.
* GitHub Actions can be monitored directly from the terminal.
* Aliases and scripting make repetitive GitHub tasks significantly faster.
* GitHub CLI is a valuable tool for DevOps engineers working with CI/CD pipelines and automation.

## Commands Added to git-commands.md

```bash
# Authentication
gh auth login
gh auth status
gh auth logout

# Repository Management
gh repo create
gh repo clone
gh repo view
gh repo list
gh repo delete

# Issues
gh issue create
gh issue list
gh issue view
gh issue close

# Pull Requests
gh pr create
gh pr list
gh pr view
gh pr checkout
gh pr review
gh pr checks
gh pr merge

# Workflows
gh run list
gh run view
gh run watch
gh workflow list
gh workflow view

# Advanced
gh api
gh gist create
gh release create
gh alias set
gh search repos
```
