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
- percheron.ceu.hu (function: STATA/Matlab with graphical interface)
- pure.percheron.ceu.hu (function: STATA/Matlab/Python etc with command-line interface only)

The percheron server has 30GB RAM memory and 16 cores, while the pure percheron has 86GB RRAM and 44 cores.
Therefore, pure percheron should be used for running memory intensive processes.

## Connecting to the servers from different local operating systems

First, you have to the CEU network through VPN (e.g. Cisco AnyConnect).
For more information on VPN usage please visit <http://www.it.ceu.edu/vpn> and <http://docs.microdata.io/vpn>.

You can access the shell (command line) on both percheron.ceu.hu and pure.percheron.ceu.hu by using a Secure Shell (ssh) client, such as Putty (http://docs.microdata.io/putty).
This is where you can change your password, or where you can start batch jobs from the shell.

You can connect to the graphical interface (windows-like) on percheron.ceu.hu via VNC.
pure.percheron.ceu.hu does not have a graphical interface.


### Linux

ssh YOURNAME@percheron.ceu.hu -p YOURSSHNUMBER
ssh YOURNAME@pure.percheron.ceu.hu -p YOURSSHNUMBER

### MacOS

ssh YOURNAME@percheron.ceu.hu -p YOURSSHNUMBER
ssh YOURNAME@pure.percheron.ceu.hu -p YOURSSHNUMBER

For the graphical server a useful tool is XQuartz.

### Windows

With Guided User Interface (GUI https://en.wikipedia.org/wiki/Graphical_user_interface) on Windows download https://www.turbovnc.org/

After installation you have to use this: 
VNC server: percheron.ceu.hu:YOURVNCNUMBER
pass: YOURPASS

### Private and public keys for easier connection

## Structure of the server and general workflow

The main Beadbox location is `/srv/dropbox_encrypted/bead-box/`.
Most of the time, however, you work in your sandbox.
You can create an alias to your sandbox

## Useful server tools

### File transfer to the server

To move data between your computer and the server, you need an SFTP or SCP client.
You have access to your home folder, and you may access shared data and project folders.

- Filezilla - <https://filezilla-project.org/>
- On Windows you can use WinScp - <https://winscp.net/eng/index.php>

### Screen

Working in screen allows users to exit the servers without terminating the running processes.

### Virtual environment

When your code requires specific python packages, you should download them to a virtual environment.

### Parallelization

Parallelization refers to the spreading the code processing work across multiple cores (CPUs).
Parallelization is useful to fasten the running time of codes by optimizing the available resources.

### STATA

Pure: /usr/local/stata15/stata-mp
GUI: /usr/local/stata15/xstata-mp

### Python

python2 or python3

## Useful server commands:

| Code             | Short description                            |
|:-------------------|:-------------------------------------------------|
| `htop` |Check servers usage, CPU and memory (see also `top`) |
| `screen` |Create screen running in the background. Ctrl-A-D to close the screen, Ctrl-D to shut down (terminate) the screen. |
| `screen -r "number_of_screen` |Open previously created screen |
| `virtualenv “name_of_virtualenv” -p python3` |Create a Python3 virtual environment |
| `virtualenv “name_of_virtualenv”` |Create a Python2 virtual environment |
| `. [‘name_of_virtualenv’]/bin/activate` |Activate virtual environment |
| `pip3 install -r requirements.txt` |Install requirements for virtual environment in requirements.txt |
| `pip3 install -r requirements_packages.txt -f packages/` |Install every requirement that are contained in a folder (as files) |
| `pip freeze` |Show downloaded python libraries |
| `pip freeze -> requirements.txt` |List the currently downloaded python packages |

## Contacts

- If you have technical difficulties with the server, please contact Daniel Biro (daniel.biro@webgalaxy.hu).
- For VPN-related problems, please contact CEU HelpDesk at helprequest@ceu.hu.
- If you have a problem with a specific application (e.g., Stata, Matlab), Daniel can help you decide whether the problem is with the operating system or with the application. In the latter case, he can put you in touch with Stata or Matlab support.
