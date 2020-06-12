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
- The computer can be controlled using a GUI or a CLI.
- Anything that you can do using the GUI can be done using a CLI.
- In the CLI, you have to issue commands with possibly some positional and optional arguments.
---
# The Command Line Interface
You probably mostly use your computer via something called a GUI, or Graphical User Interface. Practically any modern operating system comes with a GUI. It is the GUI that, for example, allows you to instruct your computer to run applications by double clicking on an application's icon instead of issuing your commands in writing. 

However, it is not the only way to use your computer. Before the quick rise in computing capacity and memory, graphical interfaces were impossible to develop. Originally computers are instructed via written commands in something called a CLI, or Command Line Interface. Practically anything that is feasible using a GUI can be done using the CLI, even though it might be much more difficult. Then why bother with using the CLI at all? - you might ask. There are two main reasons for familiarizing yourself with the CLI at MicroData:
1. The servers that we use have very limited graphical support, and you will mostly use an Ubuntu terminal when you work on the servers.
2. Most freshly developed tools for data analysis simply do not have a GUI. It takes a lot of resources to develop GUIs, and most open source developers focus their attention to the core performance of the tools instead of a GUI. If you want to use these, you have to familiarize yourself with the CLI of your computer.

## How are commands interpreted?
Every operating system comes with a command line interface. The CLI, just like the GUI is, however, different on each operating system. Most modern Windows operating systems use a CLI called Windows PowerShell, while Unix-like systems like MacOS, Ubuntu and other Linux distributions usually use a CLI called Terminal. 

It is not only the name of the CLI that differs. The commands that you issue in the CLI have to be interpreted by the computer (translated to a long list of ones and zeros) in order to execute your commands. The way that commands are translated also differs across operating systems. Without going into too much details, it practically depends on something called the command line interpreter, which is a software that does this translation for you. On Windows, this is called cmd.exe, while on most Unix-like systems it's called Bash. The main problem with having mulitple CLIs and command line interpreters is that they understand different commands and translate these commands differently. Something that works on Ubuntu will very likely not work on Windows and vice-versa. 

However, as mentioned before, the command line interpreter is just a software. Some of these interpreters have versions available for many different operating systems. The most widely used interpreter is probably Bash. If you are using MacOS or Ubuntu, you are good to go, you already have Bash installed on your computer. If you work with Windows, then you have already installed Git-bash, which, as it's name suggests, is a Bash interpreter. You will have to use this instead of the default Windows CLI throughout this episode.

## The Terminal
The CLI that we are going to use is called the Terminal (on Unix-like systems) or Git-bash (on Windows). From here on, they both will be referenced as the Terminal. If you open a Terminal window, you are supposed to see an almost-blank window with something like this written on it:
> `kisso@percheron2:~$`

It should be followed by a blinking cursor. This is called the command prompt. It tells you some important information about where you are currently working. It is structured the following way:
> username@machine:current_directory$

These are possibly the most important pieces of information that you need to be aware of when using the CLI. What do they tell you?
1. username: This is your username on your computer. In most cases it will not change. In many systems you can switch to a user called root, that can do anything on the computer that a standard user cannot. You should only see your username there, if it changes you should close the Terminal and start a new session unless you are really sure about what you are doing.
2. machine: This is separated from the username by an `@` sign in most cases. It will change for example if you log in to the server. You will be able to control the MicroData servers using the Terminal as well. It is important to know whether you are controlling your own computer or the server in the Terminal window, always make sure that you are working on the proper machine.
3. current_directory: This is usually separated from the name of the machine by a colon. In many operating systems you have something called your home folder or user folder. It is usually referenced in the Terminal by the `~` sign. If you change the working directory (which will be discussed in a second), it will change accordingly. For example on an other machine and in a different folder it might be something like this:
> `kisso@kisso-TravelMate-P236-M:~/Documents/onboarding/_episodes`

In order to use your computer via the Terminal, you will have to type commands and press enter. They will be executed one-by-one. The rest of this episode will be about the most important commands in the Terminal.

# The most important Terminal commands
Terminal commands can be executed by pressing enter after typing them. The general structure of a command is the following:
`command <positional arguments> <optional arguments>`. Some commands work by themselves, while others require arguments (for example if you want to change the working directory, you have to specify the new working directory). Positional arguments always have to be specified, while optional arguments are, as their name suggests, optional. You can almost always get a detailed explanation on the positional and optional arguments by opening up the manual of the command by executing `man <command>` or by calling the command with it's help optional argument by `<command> --help` or `help <command>`

You can find the most commonly used commands with a short description below by categories

## Navigation
- `pwd` returns the path to the current working directory. In most cases this is part of the command prompt, however, if you are deep down in the folder structure, the command prompt will only display a few parent directories.

  ~~~
  $ pwd
  ~~~
  {: .language-bash}

  ~~~
  ~/Documents/GitRepos/CEU_MD_Onboard/onboarding/
  ~~~
  {: .output}

  Now, we are at the *~/Documents/GitRepos/CEU_MD_Onboard/onboarding/* after typing the `pwd`. (Don't worry about the tilde ("~") sign. You are going to learn about it in a minute. 

- `cd` changes the working directory. It has a positional argument, which is the target directory. The target directory can be either given as an absolute path or a relative path. 
  ~~~
  #absolute path
  $ cd /srv/dropbox_encrypted/   

  #relative path
  $ cd ../../srv/dropbox_encrypted/ 
  ~~~
  {: .language-bash}

  In relative paths you can reference the parent directory by two dots `..`, thus if you want to go to the parent directory, you should issue `cd ..`.  Some more commonly used `cd` commands:
  ~~~
  #Going to your home directory
  $ cd  

  #going to the root folder
  $ cd /

  #going up to the parent directory 
  $ cd ..

  #going to the Desktop directory in the home directory
  $ cd ~/Dekstop
  ~~~
  {: .language-bash}

  The tilde ("~") character in the last command is a shortcut for indicating the home directory.

- `start` will open a file in the default application associated with it on **Windows** (aka your default application on Windows).

- `open` will open a file in the default application associated with it on **MacOS** (aka your default application on MacOS). 

- `xdg-open` will open a file in the default application associated with it on Ubuntu and many other **Linux** distributions (aka your default application on any Linux distros). 

  The example is opening a picture in the default picture viewer.
  ~~~
  #On Windows
  $ start my-picture.png

  #On MacOS
  $ open my-picture.png

  #On (most) Linux distros 
  $ xdg-open my-picture.png
  ~~~
  {: .language-bash}

## File System Exploaration
- `ls` lists the content of the current working directory. It has a wide set of optional arguments that you can combine to get a listing you prefer. A few of these are:
  - `-l` will give you the list of files with one file in one line, and it will include additional information on file permissions, file owners, file size and modification date.
  - `-a` will list all files and folders including hidden ones.
  - `-S` will sort the files by size in descending order before listing them.
  - `-t` will sort the files by modification time (newest first) before listing them.
  - `-r` will revert the order of files before listing them.
  - `-h` will display the file sizes in a human-readable format.
  - You can combine these options, so for example `ls -ltrha` will list all files, including hidden ones, in a list where one file will be one line, and the oldest file will be the first (notice the revert option, that is why it's not the newest) and file sizes will be human-readable.

  ~~~
  $ ls -ltrha  
  ~~~
  {: .language-bash} 

- `less` will show you the content of a text file. It has one positional argument, the text file. It's worth noting that it can be any text file, for example `.py` python codes can be viewed as well as `.csv` data files.
  ~~~
  $ less trial.py 
  ~~~
  {: .language-bash} 

  You can scroll up and down using the arrows on your keyboard and exit by pressing `q`.

  FIXME: Adding a table of useful `less` associated keyboard combos


- `file` will determine file type. In fact, one of the common ideas in Unix-like operating systems such as Linux is that “everything is a file.”

  ~~~
  $ file picture.jpg 
  ~~~
  {: .language-bash}

  ~~~
  picture.jpg: JPEG image data, JFIF standard 1.01  
  ~~~
  {: .output} 


## Files and Directories Manipulation
- `cp` copies a file. It has two positional arguments, the source file and the target file. 
  ~~~
  #Copy a file to the parent folder
  $ cp my-file.txt ../my-file.txt

  #Copy a folder to the parent folder by using -R recursive option 
  $ cp -R my-folder/ ../
  ~~~
  {: .language-bash}


- `mv` moves a file or folder. It has two positional arguments, the source and the target path. 
  ~~~
  #Move the directory "my-folder" and its content to the parent directory
  $ mv my-file.txt ../
  ~~~
  {: .language-bash}

  It is also the way to rename files.
  ~~~
  #"old-filename.txt" will be renamed to "new-filename.txt"
  $ mv old-filename.txt new-filename.txt
  ~~~
  {: .language-bash}


- `mkdir` creates a new folder in the current working directory. It has a single positional argument, which is the name of the new folder.
  ~~~
  $ mkdir my-new-folder
  ~~~
  {: .language-bash}

  It can also have multiple optional arguments if you wish to create multiple folders.
  ~~~
  $ mkdir dir1 dir2 dir3
  ~~~
  {: .language-bash}
  
  It is even possible to create nested folder structures by providing the `-p` argument. 
  ~~~
  $ mkdir -p dir4/dir5/dir6
  ~~~
  {: .language-bash}
  
- `rmdir` removes an empty directory. It's only positional argument is the folder to be removed. It only removes empty folders, you need to delete it's content first.

- `rm` removes a file. It has a positional argument, which is a list of files to be removed. You can give multiple files separated by spaces to remove. 
  ~~~
  #Remove a single file
  $ rm my-text.txt

  #Remove multiple files
  $ rm my-text.txt my-data.dta
  ~~~
  {: .language-bash}

  **IMPORTANT**: If you remove a file by `rm` it will be **permanently** deleted, be careful with it!

- Recursive `rm` removes a directory with all of its subdirectories and files. It can be accessed with the `-r` optional argument. 
  ~~~
  $ rm my_folder/ -r
  ~~~
  {: .language-bash}

  **IMPORTANT**: Recursive `rm` will remove the directory with all of it's content **permanently**.

- Recursive forced `rm` removes a directory with all of its subfolders and files even if the files are read-only. It can be executed using the `rf` optional argument.
  ~~~
  $ rm my_folder/ -rf
  ~~~
  {: .language-bash}

  **IMPORTANT**: deletion is **permanent**. You should not use it in general, it is only a last resort. The presence of read-only files strongly suggests that they should not be deleted using `rm`, but in some other ways (e.g. `bead nuke` in case of beads). There are some cases when this is useful, but use it with care and only if it is unavoidable.

- Some useful shortcuts, which could be used with the some of the above-mentioned commands: 
  - `?` , a question mark can be used to indicate "any single character". 
  - `* `, an asterisk can be used to indicate "zero or more characters".
    ~~~
    #Instead of using 
    $ cat test_1.txt test_2.txt test_3.txt

    #Better usage is
    $ cat test_?.txt

    #An even better shorter solution is
    $ cat test_*
    ~~~
    {: .language-bash}
      
## Working with Commands
- `type` will indicate how a command name is interpreted.

- `which` will display which executable program will be executed.

- `apropros` will display a list of appropriate commands.

- `info` will display a command's info entry.

- `whatis` will display one-line manual page descriptions.

- `alias` will create an alias for a command 

- `whoami` will remind you of your username. (Hope it will not forget your identity like Jackie Chan in the "Who am I?" movie)


## Redirection
- `cat`  will print the content of files on your terminal screen. It's positional argument is a file list separated by spaces. E.g. `cat my-code.py` prints the code in `my-code.py` to your screen. If you specify multiple files, they will be printed after each other.

- `sort` will sort lines of text.

- `uniq` will report or omit repeated lines.

- `grep` will print lines matching a pattern. 

- `wc` will print newline, word, and byte counts for each file.

- `head` and `tail` shows you the first and last few lines of a text file, respectively. It has one positional argument, the text file. E.g. `tail my-data.csv`.

- `echo` will print the value of it's argument on your terminal screen. E.g. `echo hello world!` will pring `hello world!` in your terminal window.

# Useful resources for learning Terminal: 
- Intro to the Command Line for Economics: <https://datacarpentry.org/shell-economics/>
- Official Ubuntu tutorial: <https://ubuntu.com/tutorials/command-line-for-beginners#1-overview>
- The Linux Command Line by William Shotts: <http://linuxcommand.org/tlcl.php>