---
title: "Using the terminal"
teaching: 0
exercises: 0
questions:
- How to navigate in the terminal?
- How to execute commands and start applications?
- What are some of the most important command line tools?
objectives:
- Understanding how the command line interface works.
- Learn the most important command line operations.
keypoints:
- CLI versus GUI
- The command prompt
- Important commands
---
# The Command Line Interface
You probably mostly use your computer via something called a GUI, or Graphical User Interface. Practically any modern operating system comes with a GUI. It is the GUI that, for example, allows you to instruct your computer to run applications by double clicking on an application's icon instead of issuing your commands in writing. However, it is not the only way to use your computer. Before the quick rise in computing capacity and memory, graphical interfaces were impossible to develop. Originally computers are instructed via written commands in something called a CLI, or Command Line Interface. Practically anything that is feasible using a GUI can be done using the CLI, even though it might be much more difficult. Then why bother with using the CLI at all, you might ask. There are two main reasons for familiarizing yourself with the CLI at MicroData:
1. The servers that we use have very limited graphical support, and you will mostly use an Ubuntu terminal when you work on the servers.
2. Most freshly developed tools for data analysis simply do not have a GUI. It takes a lot of resources to develop GUIs, and most open source developers focus their attention to the core performance of the tools instead of a GUI. If you want to use these, you have to familiarize yourself with the CLI of your computer.

## How are commands interpreted?
Every operating system comes with a command line interface. The CLI, just like the GUI is, however, different on each operating system. Most modern Windows operating systems use a CLI called Windows PowerShell, while Unix-like systems like MacOS, Ubuntu and other Linux distributions usually use a CLI called Terminal. It is not only the name of the CLI that differs. The commands that you issue in the CLI have to be interpreted by the computer (translated to a long list of ones and zeros) in order to execute your commands. The way that commands are translated also differs across operating systems. Without going into too much details, it practically depends on something called the command line interpreter, which is a software that does this translation for you. On Windows, this is called cmd.exe, while on most Unix-like systems it's called Bash. The main problem with having mulitple CLIs and command line interpreters is that they understand different commands and translate these commands differently. Something that works on Ubuntu will very likely not work on Windows and vice-versa. However, as mentioned before, the command line interpreter is just a software. Some of these interpreters have versions available for many different operating systems. The most widely used interpreter is probably Bash. If you are using MacOS or Ubuntu, you are good to go, you already have Bash installed on your computer. If you work with Windows, then you have already installed Git-bash, which, as it's name suggests, is a Bash interpreter. You will have to use this instead of the default Windows CLI throughout this episode.

## The Terminal
The CLI that we are going to use is called the Terminal (on Unix-like systems) or Git-bash (on windows). From here on, they both will be referenced as the Terminal. If you open a Terminal window, you are supposed to see a blank screen with something like this written on it:
> kisso@percheron2:~$
It should be followed by a blinking cursor. This is called the command prompt. It tells you some important information about where you are currently working. It is structured the following way:
> username@machine:current_directory$
These are possibly the most important pieces of information, that you need to be aware of when using the CLI. What do they tell you?
1. username: This is your username on your computer. In most cases it will not change. In many systems you can switch to a user called root, that can do anything on the computer that a standard user cannot. You should only see your username there, if it changes you should close the Terminal and start a new session unless you are really sure about what you are doing.
2. machine: This is separated from the username by an '@' sign in most cases. It will change for example if you log in to the server. You will be able to control the MicroData servers using the Terminal as well. It is important to know whether you are controlling your own computer or the server in the Terminal window, always make sure that you are working on the proper machine.
3. current_directory: This is usually separated from the name of the machine by a colon. In many operating systems you have something called your home folder or user folder. It is usually referenced in the Terminal by the `~` sign. If you change the working directory (which will be discussed in a second), it will change accordingly. For example on an other machine and in a different folder it might be something like this:
> kisso@kisso-TravelMate-P236-M:~/Documents/onboarding/_episodes

In order to use your computer via the Terminal, you will have to type commands and press enter. They will be executed one-by-one. The rest of this episode will be about the most important commands in the Terminal.

# The most important Terminal commands


{% include links.md %}

