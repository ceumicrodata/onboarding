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

You can connect to the graphical interface (windows-like) on percheron.ceu.hu via a VNC client. On UNIX-like systems using X-server (e.g. Ubuntu) you can simply allow X11 forwarding in an ssh connection by using the `-X` optional argument and don't need a VNC client.
pure.percheron.ceu.hu does not have a graphical interface.


### Linux
You can connect to the servers from a Terminal window using either of the following commands (substitute your username and port number appropriately):
  ~~~
  $ ssh USER@percheron.ceu.hu -p PORT -X
  $ ssh USER@pure.percheron.ceu.hu -p PORT
  ~~~
  {: .language-bash} 

### MacOS
You can connect to the servers from a Terminal window using either of the following commands (substitute your username and port number appropriately)
  ~~~
  $ ssh USER@percheron.ceu.hu -p PORT
  $ ssh USER@pure.percheron.ceu.hu -p PORT
  ~~~
  {: .language-bash} 

For the graphical server a useful tool is XQuartz.
Using XQuartz you can enable X11 forwarding from the graphical server.
In an XQuartz terminal you can connect to the graphical server by issuing the following command:
(substitute your username and port number appropriately)
  ~~~
  $ ssh USER@percheron.ceu.hu -p PORT -y
  ~~~
  {: .language-bash} 

### Windows

PuTTy provides a CLI for both servers. For GUI on Windows download [TurboVNC](https://www.turbovnc.org/). After installation you have to use the following server address along with your server password: 
`percheron.ceu.hu:VNCPORT`

### Private and public keys for easier connection

For easier server access you can create private/public key pairs as follows:

1. Start the key generation program by typing `ssh-keygen` on your local computer

2. Enter the path to the file where it is going to be located.
Make sure you locate it in your `.ssh` folder and name it as `microdata_kulcs` (or any alternative filename).

3. Enter a Passphrase or just simply press Enter.
The public and private keys are created automatically. The public key ends with the string `.pub`.

4. Copy the public key to the `$HOME/USER/.ssh` folder on the server. 
(substitute your username appropriately)

4b. An alternative solution for point 4 is using the following code: ssh-copy-id -i ~/.ssh/id_rsa USER@pure.percheron.ceu.hu -p PORT
(a useful [source](https://www.ssh.com/ssh/keygen/) for the whole process)

Finally, you can alias the command that connects you to server:

#### MacOS

Copy the following text into the `config` file which is located in your .ssh folder:
(substitute your usernames and port number appropriately)

```
Host pure
        HostName pure.percheron.ceu.hu
        User USER
        Port PORT
        IdentityFile /Users/LOCAL_USER/.ssh/microdata_kulcs

Host percheron
        HostName percheron.ceu.hu
        User USER
        Port PORT
        IdentityFile /Users/LOCAL_USER/.ssh/microdata_kulcs
```

This allows you to connect to the percheron1 and percheron2 servers by typing the `ssh pure` and `ssh percheron` commands respectively.

#### Linux

Add the following lines to your `.bashrc` file located in your home folder (by typing `nano .bashrc`):

```
alias pure='ssh USER@pure.percheron.ceu.hu -p PORT'
alias percheron='ssh -X USER@percheron.ceu.hu -p PORT'
```

This allows you to connect to the percheron1 and percheron2 servers by typing the `pure` and the `percheron` commands respectively.
#### Windows

## Structure of the server and general workflow

When connecting to the server, you are directed to your home folder `/home/USER_NAME'.
Only you have access to your home folder and you can use it for developing your own projects.

For Microdata project work, however, you should be working in your sandbox located at `/srv/dropbox_encrypted/USER_NAME_sandbox`.
Working in your sandbox allows others to check your work and develop projects collaboratively.

When saving your bead, a copy of your work is created in .zip format in the beadbox.
The beadbox is located at `/srv/dropbox_encrypted/bead-box/`.
For more information on the use of bead, please visit the corresponding episode on this website.

Finally, you may want to access files that were created before the bead system was developed.
These folders and files can be found at `/srv/dropbox`.
We no longer use this path for project development.

### Creating alias to your sandbox

You can create aliases that simplifies your access to you sandbox.
For that, you need to add the following commands to your `.bashrc` file: (substitute your username appropriately)

```
alias sandbox='cd /srv/dropbox_encrypted/USER_sandbox'
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

`sftp://percheron.ceu.hu`

It is worth noting that on Ubuntu systems you don't need any additional client for file transfer. Just open a file navigator, go to Other locations, and connect to the server by issuing it's sftp address - e.g. `sftp://USER@percheron.ceu.hu:PORT`. You will automatically be prompted for your username and password, and you can navigate on the server just like on your own computer.
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

You can access the STATA program on both servers, however, only the Percheron server has graphical user interface.
The stata is located in the folders:

Pure: /usr/local/stata15/stata-mp

Percheron (GUI): /usr/local/stata15/xstata-mp

### Python

The servers run both python2 or python3.
You can access them by typing `python` for python2 (current version 2.7.15) and `python3` for python3 (current version 3.6.5).
To leave the python shell and return to the system shell, type the python command `exit()`.

## Useful server commands:

| Code             | Short description                            |
|:-------------------|:-------------------------------------------------|
| `htop` |Check servers usage, CPU and memory (see also `top`) |
| `screen` |Create screen running in the background. Ctrl-A-D to close the screen, Ctrl-D to shut down (terminate) the screen. |
| `screen -r "number_of_screen` |Open previously created screen |
| `virtualenv “name_of_virtualenv” -p python3` |Create a Python3 virtual environment |
| `virtualenv “name_of_virtualenv”` |Create a Python2 virtual environment |
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
