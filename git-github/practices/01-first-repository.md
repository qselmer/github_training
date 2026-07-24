# Practice 01 — First repository

## Objective

Create a local repository, register the first version of a file, and publish the project on GitHub.

## Part A. Create the local project

```bash
mkdir my-first-repo
cd my-first-repo
git init
```

## Part B. Create the first file

```bash
echo "# My First Repository" > README.md
git status
```

## Part C. Register the first version

```bash
git add README.md
git commit -m "docs: add initial README"
```

## Part D. Connect with GitHub

Create an empty repository on GitHub and then run:

```bash
git branch -M main
git remote add origin https://github.com/USERNAME/my-first-repo.git
git push -u origin main
```

Replace `USERNAME` with the GitHub username.

## Part E. Make a second change

```bash
echo "This repository contains my Git practice." >> README.md
git diff
git add README.md
git commit -m "docs: describe repository purpose"
git push
```

## Verification

The practice is complete when:

- the repository is visible on GitHub;
- `README.md` contains both lines;
- the history contains at least two commits;
- `git status` reports a clean working tree.
