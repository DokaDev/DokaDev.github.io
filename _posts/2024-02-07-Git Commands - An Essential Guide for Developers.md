---
title: Git Commands - An Essential Guide for Developers
date: 2024-02-07 00:01:00 +0900
categories: [Git]
tags: [git]     # TAG names should always be lowercase
---

Git is an indispensable tool for managing source code versions in development projects.
This post aims to introduce a wide range of Git commands, from basics to advanced usage, providing usage examples and real-life application scenarios to help you utilize Git more effectively.

## Installing and Configuring Git
The first step is installing Git, which is available for all major operating systems including Windows, macOS, and Linux.

You can get download and install Git through the link below.

[Link Here](https://git-scm.com/)

![image](assets/post/git/0.png){: .w-75 .shadow .rounded-10 }

After installation, it's essential to configure your user name and email address before you start using Git, as this information is used in every commit.

```bash
git config --global user.name "Your Name"
git config --global user.email "youremail@example.com"
```

## Basic Git Commands
### Initializing a Repository: `git init`

Used at the beginning of a new project or when introducing Git to an existing project.
It initializes a new Git repository in the current directory.
```bash
git init
```
### Staging Changes: `git add`

Adds changes in files or directories to the staging area, selecting changes for the next commit.
```bash
git add <file>

git add . # All
```
### Committing Changes: `git commit`

Records the staged changes to the repository.
Each commit has a unique ID, representing a snapshot of changes at a specific point in time.
```bash
git commit -m "Commit message"
```
### Checking Repository Status: `git status`

Shows the current state of the repository, including changes files, stages files, and uncommitted changes.
```bash
git status
```
### Viewing Commit History: `git log`

Displays the commit history of the repository, showing detailed information about each commit, including the author and date.
```bash
git log
```

## Undoing Changes
### Changing the Working Directory: `git checkout`

Changes the state of the working directory to a specific branch or commit.
This can be used to revert to a previous state or switch to another branch.
```bash
git checkout <branch-name or commit-hash>
```

## Branching and Merging
### Listing and Creating Branches: `git branch`

Shows the list of branches in the repository or creates a new branch.
```bash
git branch # List branches
git branch <new-branch-name> # Create a new branch
```
### Merging Branches: `git merge`

Merges changes from another branch into the current branch.
This process may result in conflict that need to be resolved manually.
```bash
git merge <branch-name>
```

## Working with Remote Repositories
### Adding a Remote Repository: `git remote add`

Adds a new remote repository.
This allows for integration with remote hosting services like GitHub.
```bash
git remote add <shortname> <url>
```
### Fetching Changes from a Remote Repository: `git fetch`

Fetches the latest changes from a remote repository to local, without altering the current branch's work.
```bash
get fetch <remote-name>
```

## Advanced Git Commands
### Stashing Changes: `git stash`

Temporarily stores current changes, allowing you to revert the working directory to a clean state.
```bash
git stash
```

