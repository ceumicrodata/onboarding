---
title: "A quick introduction to Git and Github"
teaching: 0
exercises: 0
questions:
- What are the basic terms used by version control systems?
- Which files are contained within the .git directory?
- How to install git?
- How does the basic collaborative workflow look like?
- What are some of the most important git commands? 
objectives:
- Understand the basic terminology of Git and Github
- Install and setup git
- Understand the collaborative workflow and commit message etiquette
- List some of the most useful commands that can be easily accessed in your everyday work
---

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
It is a 40-character string composed of characters (0–9 and a–f) such as `e2adf8ae3e2e4ed40add75cc44cf9d0a869afeb6`.

#### Branch

A branch is a line of development that diverges from the main line of development.
It further allows you to experiment with the code without modifying the line of development in the master branch.
When the project development in a branch turns out successful, it can be merged back to the master branch.

#### Checkout

Checkout allows you to point your working directory to a different commit.
Therefore, you can jump to a particular SHA or to a different branch.

#### .Git Directory Contents

The .git directory contains:
*   config file - it stores the configuration settings
*   description file - file used by the GitWeb program
*   hooks directory -  client-side or server-side scripts can be placed here to hook into Git's lifecycle events
*   info directory - contains the global excludes file
*   objects directory - stores all the commits
*   refs directory - holds pointers to commits (e.g "branch" and "tag") 

### Install, setup git

*   Supported browsers: current versions of Chrome, Firefox, Safari, Microsoft Edge    
*   Create a [GitHub](https://github.com/) account              
*   Install [git](https://git-scm.com/downloads)   
    * Indented itemIf you are on a Mac, git should already be installed.        
    * Indented itemIf you are using a Windows machine, this will also install a program called *Git Bash*, which provides a text-based interface for executing commands on your computer.
*   Configure installation    
    * `git config --global user.name "your-full-name"`    
    * `git config --global user.email "your-email-address"`     
*   SSH key: for faster usage (no password needed afterwards)    
    * Check if you already have: Is it anything in .ssh? ls .ssh    
        * if no, create a new one and [add to ssh agent](https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)                             
        * if yes, go to next step        
    * [Add new SSH key](https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account) to your github account:           
*   Download [Sublime Merge](https://www.sublimemerge.com/download) (recommended git client) 

### Git workflow - collaborate with others

### Useful commands

| Code             | Short description                            |
|:-------------------|:-------------------------------------------------|
| `git init` |Initialize local git repository |
| `git status` |Check the status of git repository (e.g. the branch, files to commit)|
| `git add` |Add files to staging index|
| `git add .` |Add all modified files to staging index|
| `git commit -m"Text"` |Commit changes with commit message |
| `git log` |Check git commits specifying SHA, author, date and commit message |
| `git log --oneline` |Check git commits specifying short SHA and commit message |
| `git log --stat` |Check git commits with additional information on the files changed and insertions/deletions |
| `git log -p` |Shows detailed information on lines inserted/ deleted in commits |
| `git log -p --stat` |Combines information from previous two commands |
| `git log -p -w` |Shows detailed information on commits ignoring whitespace changes |
| `git show` |Show only last commit|
| `git show <options> <object>` |View expanded details on git objects  |
| `git diff` |See the changes that haven’t been committed yet|
| `git diff <SHA> <SHA>` |Shows changes between commits |
| `git tag` |Show existing tags |
| `git tag -a "tagname"` |Tag current commit |
| `git tag -d "tagname` |Delete tag |
| `git tag -a "tagname" "SHA pattern"` |Tag commit with given SHA pattern |
| `git branch "name_of_branch" "SHA pattern(optional)"` |Create new branch – at SHA pattern |
| `git branch “name_of_branch” master` |Start new branch at the latest commit of master branch |
| `git checkout “name_of_branch”` |Move pointer to the latest commit of the specified branch |
| `git branch -d “name_of_branch` |Delete branch, use -D to force deletion |
| `git checkout -b “name_of_branch”` |Create branch and checkout in one command |
| `git log --oneline --graph --all` |Show branches in a tree |
| `git merge “name_of_branch_to_merge_in”` |Merge in current branch to another |

## Useful resources for mastering git and github:
- Technical foundations of informatics book: <https://info201.github.io/git-basics.html>
- Software carpentry course (Strongly recommended): <https://swcarpentry.github.io/git-novice/>
- Github Learning Lab: <https://lab.github.com/>
- If you are really committed (pun intended): <https://git-scm.com/book/en/v2>
- Getting started with Github: <https://help.github.com/en/github/getting-started-with-github>
- Git cheatsheet: <https://education.github.com/git-cheat-sheet-education.pdf>
- Learn git with bicbucket cloud: <https://www.atlassian.com/git/tutorials/learn-git-with-bitbucket-cloud>


## Useful GUI tools for version control:
- Sublime Merge: <https://www.sublimemerge.com>
- Version Control in VS Code: <https://code.visualstudio.com/docs/editor/versioncontrol>

