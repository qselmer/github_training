# Basic Git commands

## Configuration

```bash
git --version
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
git config --global --list
```

## Repository creation

```bash
git init
git clone REPOSITORY_URL
```

## Daily workflow

```bash
git status
git diff
git add FILE
git add .
git commit -m "type: concise description"
git log --oneline
```

## Remote repositories

```bash
git remote -v
git remote add origin REPOSITORY_URL
git push -u origin main
git pull origin main
git fetch origin
```

## Branches

```bash
git branch
git switch -c new-branch
git switch main
git merge new-branch
git branch -d new-branch
```

## Safe corrections

```bash
git restore FILE
git restore --staged FILE
git commit --amend
```

Before running a command that discards changes, inspect the repository with `git status` and `git diff`.
