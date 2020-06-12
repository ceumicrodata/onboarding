---
title: "How to use the percheron1 and percheron2 servers"
teaching: 0
exercises: 0
questions:
- How to connect to percheron1 and percheron2?
- What is the structure of the server?
- What is the general workflow on the servers?
objectives:
- Learn how to set up connection with the servers
- Understand the basic specifications of our servers
- Study commands that are useful when working on the servers
---

{% include links.md %}

## The servers and some basic information

Microdata currently uses two servers.
The first one is percheron (percheron1) which is a graphical server (GUI).
The second one is pure percheron (percheron2) which is command line input only (CLI).

The percheron server has 30GB RAM memory and 16 cores, while the pure percheron has 86GB RRAM and 44 cores.
Therefore, pure percheron should be used for running memory intensive processes.

## Connecting to the servers from different local operating systems

### Linux

### MacOS

For the graphical server a useful tool is XQuartz.

### Windows

### Private and public keys for easier connection


## Structure of the server

## Workflow on the server

## Useful server tools

### Screen

Working in screen allows users to exit the servers without terminating the running processes.

### Virtual environment

### Parallelization

Parallelization refers to the spreading the code processing work across multiple cores (CPUs).
Parallelization is useful to fasten the running time of codes by optimizing the available resources.

## Useful server commands:

| Code             | Short description                            |
|:-------------------|:-------------------------------------------------|
| `htop` |Check running processes on the server (check also `top`) |
| `screen` |Create screen running in the background. Ctrl-A-D to close the screen, Ctrl-D to shut down (terminate) the screen. |
| `screen -r "number_of_screen` |Open previously created screen |
| `virtualenv “name_of_virtualenv” -p python3` |Create a Python3 virtual environment |
| `virtualenv “name_of_virtualenv”` |Create a Python2 virtual environment |
| `. [‘name_of_virtualenv’]/bin/activate` |Activate virtual environment |
| `pip3 install -r requirements.txt` |Install requirements for virtual environment in requirements.txt |
| `pip3 install -r requirements_packages.txt -f packages/` |Install every requirement that are contained in a folder (as files) |
| `pip freeze` |Show downloaded python libraries |
| `pip freeze -> requirements.txt` |List the currently downloaded python packages |

