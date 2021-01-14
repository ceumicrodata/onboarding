---
title: "How to use the haflinger server"
teaching: 0
exercises: 0
questions:
- How to connect to haflinger server?
- What is the structure of the server?
- What is the general workflow on the server?
objectives:
- Learn how to set up connection with the server
- Understand the basic specifications of our server
- Study commands that are useful when working on the server
---

{% include links.md %}

## The server and some basic information

Microdata currently uses one server.

- haflinger: haflinger.ceu.hu - function: STATA/Matlab/Python with graphical interface

The haflinger server has 504GB memory and 112 cores.

## Connecting to the server from different local operating systems

First, you have to be connected to the CEU network through VPN. You can use the AnyConnect client or the openconnect package depending on your OS.
For more information on VPN usage please visit <http://www.it.ceu.edu/vpn> and <http://docs.microdata.io/vpn>.

You can access the shell (command line) on haflinger.ceu.hu by using a Secure Shell (ssh) client, such as Putty (http://docs.microdata.io/putty). On UNIX-like systems the built-in ssh package allows you to connect without any additional software.
This is where you can change your password, or where you can start batch jobs from the shell.

You can connect to the graphical interface (windows-like) on haflinger.ceu.hu via a VNC client. On UNIX-like systems using X-server (e.g. Ubuntu) you can simply allow X11 forwarding in an ssh connection by using the `-X` optional argument and don't need a VNC client.

### Linux
You can connect to the servers from a Terminal window using either of the following commands (substitute your username and port number appropriately):
  ~~~
  $ ssh USER@haflinger.ceu.hu -p PORT -X
  ~~~
  {: .language-bash} 

### MacOS
You can connect to the servers from a Terminal window using either of the following commands (substitute your username and port number appropriately)
  ~~~
  $ ssh USER@haflinger.ceu.hu -p PORT
  ~~~
  {: .language-bash} 

For a graphical server connection a useful tool is XQuartz.
Using XQuartz you can enable X11 forwarding.
In an XQuartz terminal you can connect to the graphical server by issuing the following command:
(substitute your username and port number appropriately)
  ~~~
  $ ssh USER@haflinger.ceu.hu -p PORT -y
  ~~~
  {: .language-bash} 

### Windows

PuTTy provides a CLI for the server. 
On Windows you can download a simple REAL VNC viewer from: [vncviewer](https://cp.webgalaxy.hu/haflinger/vncviewer.exe)
After installation you have to use the following server address along with your server password: 
`haflinger.ceu.hu:VNCPORT`

A good example how you can start the viewer from the cmd. You have to change the "%vnc_port%" part to your own port number. 
  ~~~
  $ vncviewer.exe -SecurityNotificationTimeout=0 -WarnUnencrypted=0 -Quality=High -Scaling=100%x100% haflinger.ceu.hu:%vnc_port%
  ~~~
  {: .language-bash} 

### Private and public keys for easier connection

For easier server access you can create private/public key pairs as follows:

1. Start the key generation program by typing `ssh-keygen` on your local computer

2. Enter the path to the file where it is going to be located.
Make sure you locate it in your `.ssh` folder and name it as `microdata_kulcs` (or any alternative filename).

3. Enter a Passphrase or just simply press Enter.
The public and private keys are created automatically. The public key ends with the string `.pub`.

4. Copy the public key to the `$HOME/USER/.ssh` folder on the server. 
(substitute your username appropriately)

5. An alternative solution for point 4 is using the following code: `ssh-copy-id -i ~/.ssh/id_rsa USER@haflinger.ceu.hu -p PORT`.
(a useful [source](https://www.ssh.com/ssh/keygen/) for the whole process)

Finally, you can alias the command that connects you to server:

#### MacOS

Copy the following text into the `config` file which is located in your .ssh folder:
(substitute your usernames and port number appropriately)

```
Host haflinger
        HostName haflinger.ceu.hu
        User USER
        Port PORT
        IdentityFile /Users/LOCAL_USER/.ssh/microdata_kulcs

```

This allows you to connect to the haflinger server by typing the `ssh haflinger` command.

#### Linux

Add the following lines to your `.bashrc` file located in your home folder (by typing `nano .bashrc`):

```
alias haflinger='ssh USER@haflinger.ceu.hu -p PORT'
```

This allows you to connect to the haflinger server by typing the `ssh haflinger` command.

#### Windows

## Structure of the server and general workflow

When connecting to the server, you are directed to your home folder `/home/USER_NAME'.
Only you have access to your home folder and you can use it for developing your own projects.

For Microdata project work, however, you should be working in your sandbox located at `/srv/sandbox/USER_NAME`.
Working in your sandbox allows others to check your work and develop projects collaboratively.

When saving your bead, a copy of your work is created in .zip format in one of the beadboxes.
The beadboxes are located at `/srv/bead-box/`.
For more information on the use of bead, please visit the corresponding episode on this website.

### Creating alias to your sandbox

You can create aliases that simplifies your access to you sandbox.
For that, you need to add the following commands to your `.bashrc` file: (substitute your username appropriately)

```
alias sandbox='cd /srv/sandbox/USER_NAME'
```

The `.bashrc` is located in your home folder (`home/USER`).

Then, you can access your sandbox by typing `sandbox` to the command line.

## Useful server tools

### File transfer to the server

To move data between your computer and the server, you need an SFTP or SCP client.
You have access to your home folder, and you may access shared data and project folders.
You can choose from a wide variety of SFTP clients. A few of these are the following:

- Filezilla - <https://filezilla-project.org/>
- On Windows you can use WinScp - <https://winscp.net/eng/index.php>

To access the files on the server, provide the following sftp address to your client along with your username, password, and appropriate port number:

`sftp://haflinger.ceu.hu`

It is worth noting that on Ubuntu systems you don't need any additional client for file transfer. Just open a file navigator, go to Other locations, and connect to the server by issuing it's sftp address - e.g. `sftp://USER@haflinger.ceu.hu:PORT`. You will automatically be prompted for your username and password, and you can navigate on the server just like on your own computer.
### Screen

Working in screen allows users to exit the servers without terminating the running processes.
Therefore, you should always work in screen when running complex programs that run for longer time.
For instructions on how to open and close a screen window, see the 'Useful server commands' section below.

### Virtual environment

When your code requires specific python packages, you should download them to a virtual environment.
The Python environment on the server incorporates only the most basic Python packages so it is always recommended to work in a virtual environment.
For instructions on how to create and activate a virtual environment, see the 'Useful server commands' section below.

If your program runs from a `main.sh` file, you can easily automate the creation of the virtual environment by inserting the following script to your code.
Substitute the name of the virtual environment and local package folder (if applicable) appropriately.

```
virtualenv 'NAME_OF_THE_ENV'
. 'NAME_OF_THE_ENV'/bin/activate
pip install -r requirements.txt
pip install -f 'LOCAL_PACKAGE_FOLDER'/ -r requirements-local.txt

YOUR_CODE

deactivate
```

To create a virtualenv and use it permanently, one can use [mkvirtualenv](https://virtualenvwrapper.readthedocs.io/en/latest/):

```
$ mkvirtualenv pandas
(pandas) $ pip install pandas
(pandas) $ python
(pandas) $ deactivate
$ echo "I am no longer in a virtualenv."
$ workon pandas
(pandas) $ pip install jupyter
```

### Parallelization

Parallelization refers to the spreading the code processing work across multiple cores (CPUs).
Parallelization is useful to fasten the running time of codes by optimizing the available resources.

For a short introduction on parallelization in Python, please visit the following website:
https://sebastianraschka.com/Articles/2014_multiprocessing.html

### STATA

You can access the STATA program with graphical user interface on the haflinger.
The stata is located in the folders:

 /usr/local/stata16/xstata-mp

### Python

The servers run both python2 or python3.
You can access them by typing `python2` for python2 (current version 2.7.18) and `python` for python3 (current version 3.8.5).
To leave the python shell and return to the system shell, type the python command `exit()`.

## Useful server commands:

| Code             | Short description                            |
|:-------------------|:-------------------------------------------------|
| `htop` |Check servers usage, CPU and memory (see also `top`) |
| `screen` |Create screen running in the background. Ctrl-A-D to close the screen, Ctrl-D to shut down (terminate) the screen. |
| `screen -r "number_of_screen` |Open previously created screen |
| `virtualenv “name_of_virtualenv” -p python` |Create a Python3 virtual environment |
| `virtualenv “name_of_virtualenv” -p python2` |Create a Python2 virtual environment |
| `. [‘name_of_virtualenv’]/bin/activate` |Activate virtual environment |
| `pip3 install -r requirements.txt` |Install requirements for virtual environment listed in requirements.txt |
| `pip3 install -r requirements_packages.txt -f packages/` |Install every requirement that are contained in a folder (as files) |
| `pip freeze` |Show downloaded python libraries |
| `pip freeze -> requirements.txt` |List the currently downloaded python packages |
| `exit` |Terminate connection with the server |

## Contacts

- If you have technical difficulties with the server, please contact a Project Manager.
- For VPN-related problems, please contact CEU HelpDesk at helprequest@ceu.hu.
- If you have a problem with a specific application (e.g., Stata, Matlab), a Project Manager can help you decide whether the problem is with the operating system or with the application. In the latter case, he can put you in touch with Stata or Matlab support.
