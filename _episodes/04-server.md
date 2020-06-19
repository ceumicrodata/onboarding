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
- percheron1: percheron.ceu.hu - function: STATA/Matlab with graphical interface
- percheron2: pure.percheron.ceu.hu - function: STATA/Matlab/Python etc. with command-line interface only

The percheron1 server has 30GB memory and 16 cores, while percheron2 has 86GB RAM and 44 cores.
Therefore, percheron2 should be used for running memory/computation intensive processes.

## Connecting to the servers from different local operating systems

First, you have to be connected tothe CEU network through VPN. You can use the AnyConnect client or the openconnect package depending on your OS.
For more information on VPN usage please visit <http://www.it.ceu.edu/vpn> and <http://docs.microdata.io/vpn>.

You can access the shell (command line) on both percheron.ceu.hu and pure.percheron.ceu.hu by using a Secure Shell (ssh) client, such as Putty (http://docs.microdata.io/putty). On UNIX-like systems the built-in ssh package allows you to connect without any additional software.
This is where you can change your password, or where you can start batch jobs from the shell.

You can connect to the graphical interface (windows-like) on percheron.ceu.hu via a VNC client. On UNIX-like systems using X-server (e.g. Ubuntu) you can simply allow X11 forwarding in an ssh connection by using the `-x` optional argument and don't need a VNC client.
pure.percheron.ceu.hu does not have a graphical interface.


### Linux
You can connect to the servers from a Terminal window using either of the following commands (substitute your username and port number appropriately):
  ~~~
  $ ssh USER@percheron.ceu.hu -p PORT -x
  $ ssh USER@pure.percheron.ceu.hu -p PORT
  ~~~
  {: .language-bash} 

### MacOS
You can connect to the servers from a Terminal window using either of the following commands (substitute your username and port number appropria>
  ~~~
  $ ssh USER@percheron.ceu.hu -p PORT
  $ ssh USER@pure.percheron.ceu.hu -p PORT
  ~~~
  {: .language-bash} 

For the graphical server a useful tool is XQuartz. Using XQuartz you can enable X11 forwarding from the graphical server. In an XQuartz terminal you can connect to the graphical server by issuing the following command:
You can connect to the servers from a Terminal window using either of the following commands (substitute your username and port number appropria>
  ~~~
  $ ssh USER@percheron.ceu.hu -p PORT -y
  ~~~
  {: .language-bash} 

### Windows

PuTTy provides a CLI for both servers. For GUI on Windows download [TurboVNC](https://www.turbovnc.org/). After installation you have to use the following server address along with your server username and password: 
`percheron.ceu.hu:VNCPORT`

### Private and public keys for easier connection

## Structure of the server and general workflow

The main Beadbox location is `/srv/dropbox_encrypted/bead-box/`.
Most of the time, however, you work in your sandbox.
You can create an alias to your sandbox

## Useful server tools

### File transfer to the server

To move data between your computer and the server, you need an SFTP or SCP client.
You have access to your home folder, and you may access shared data and project folders.
You can choose from a wide variety of SFTP clients. A few of these are the following:

- Filezilla - <https://filezilla-project.org/>
- On Windows you can use WinScp - <https://winscp.net/eng/index.php>

To access the files on the server, provide the following sftp address to your client along with your username, password, and appropriate port number:

`sftp://percheron.ceu.hu`

It is worth noting that on Ubuntu systems you don't need any additional client for file transfer. Just open a file navigator, go to Other locations, and connect to the server by issuing it's sftp address. You will automatically be prompted for your username and password, and you can navigate on the server just like on your own computer.
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

- If you have technical difficulties with the server, please contact a Project Manager.
- For VPN-related problems, please contact CEU HelpDesk at helprequest@ceu.hu.
- If you have a problem with a specific application (e.g., Stata, Matlab), a Project Manager can help you decide whether the problem is with the operating system or with the application. In the latter case, he can put you in touch with Stata or Matlab support.
