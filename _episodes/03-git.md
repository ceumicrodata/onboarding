---
title: "A quick introduction to Git and Github"
teaching: 0
exercises: 0
questions:
- "Key question (FIXME)"
objectives:
- "First learning objective. (FIXME)"
keypoints:
- "First key point. Brief Answer to questions. (FIXME)"
---
FIXME

{% include links.md %}

## Version Control Basics

There are various Version Control Systems such as:
*   [Git](https://git-scm.com/)
*   [Subversion](https://subversion.apache.org/)
*   [Mercurial](https://www.mercurial-scm.org/)

A version control system can be either:
*   centralized - all users connect to a central, master repository
*   distributed - each user has the entire repository on their computer

### Terminology

#### Version Control System / Source Code Manager

A version control system (or source code manager) is a tool that manages different versions of source code.
It helps to create snapshots ("commits") of project files, thereby, supporting the tractability of a project. 

#### Repository / repo

A repository is a directory which the version control system tracks and should contain all the files of your project.
Besides your project files, a repository contains (hidden) files that git uses for configuration purposes.
Git, by default, tracks all your files in a repository.
If there are files you do not wish to track, you can include them in the manually created .gitignore file.

Repositories can be located either on a local computer or on the servers of an online version control platform (such as Github).

#### Staging Area / Staging Index / Index

Before committing changes to your project code, the files you want to snapshot need to be added to the Staging Index.
Changes to these files can be captured in a commit. 

#### Commit

A commit is a snapshot of the files that are added to the Staging Index.
Creating a commit can help you to save a particular version of your project.
When committing changes, you should also include a commit message that explains the changes of the project files since the previous commit.
Therefore, commits track the evolution of your project and allows you to see the changes from one commit to another.
It is also useful when experimenting with new code, as git makes it possible to jump back to a previous commit in case your code changes do not work out as planned. 

#### SHA

A SHA("Secure Hash Algorithm") is an identification number for each commit.
It contains 40-character string composed of characters (0–9 and a–f) such as `e2adf8ae3e2e4ed40add75cc44cf9d0a869afeb6`.

#### Branch

A branch is a line of development that diverges from the main line of development.
It further allows you to experiment with the code without modified the line of development in the master branch.
When the project development in a branch turns out successful, it can be merged back to the master branch.

#### Checkout

Checkout allows you to switch your working directory to a different commit.
Therefore, you can jump to a particular SHA or to a different branch.

#### .Git Directory Contents

The .git directory contains:
*   config file - it stores the configuration settings
*   description file - file used by the GitWeb program
*   hooks directory -  client-side or server-side scripts can be placed here to hook into Git's lifecycle events
*   info directory - contains the global excludes file
*   objects directory - stores all the commits
*   refs directory - holds pointers to commits (e.g "branch" and "tag") 

### Useful commands

| Code             | Short description                            |
|:-------------------|:-------------------------------------------------|
| `git init` |Initialize local git repository |
| `git status` |Check the status of git repository |
| `git add` |Add files to staging index|
| `git add .` |Add all modified files to staging index|
| `git commit -m"Text"` |Commit changes with commit message |
| `git log` | |
| `git log --oneline` | |
| `git log --stat` | |
| `git log -p` |Patch |
| `git log -p --stat` | |
| `git log -p -w` |It ignores whitespace changes |
| `git shoq` | |
| `git diff` | |
| `git tag` | |
| `git tag -a "tagname"` | |
| `git tag -d "tagname` | |
| `git tag -a "tagname" "SHA pattern"` | |
| `git branch` | |
| `git branch "name_of_branch" "SHA pattern(optional"` | |



