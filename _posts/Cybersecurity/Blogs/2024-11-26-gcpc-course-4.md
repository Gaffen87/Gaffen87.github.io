---
layout: post
title: GCPC Course 4 - Linux and SQL
date: 2024-11-26 10:01 +0000
categories: [IT-sikkerhed, IT-sikkerhed/blog]
image: https://media.licdn.com/dms/image/v2/D5610AQGV6ogDvsWHmw/image-shrink_1280/image-shrink_1280/0/1696018945798?e=2147483647&v=beta&t=XPa5lWELqm72qw-BwtrNHWTCoGmsUIgOlJoAVFbLuQY
---

## Modul 2

### Linux
An open-source operating system

### Components of Linux
- User
- Applications
- Shell
- Filesystem Hierarchy Standard
- Kernel
- Hardware

### Shell
The command-line interpreter

### Filesystem Hierarchy Standard (FHS)
The component of the Linux OS that organizes data

### Kernel
The component of the Linux OS that manages processes and memory

### Distributions
The different versions of Linux

### Parent distributions
- Red Hat Enterprise Linux (CentOS)
- Slackware (SUSE)
- Debian (Ubuntu and KALI LINUX)

### Pentest tools in KALI LINUX
- Metasploit
- Burp Suite
- John the Ripper

### Digital forensics
The practice of collecting and analyzing data to determine what has happened after an attack

### Digital forensic tools in KALI LINUX
- tcpdump
- Wireshark
- Autopsy

### Package managers
- Red Hat Package Manager (RPM)
	- .rpm
- dpkg for Debian
	- .deb

### Package management tools
- Advanced Package tool (APT)
	- APT is a tool used with Debian-derived distributions. It is run from the command-line interface to manage, search, and install packages.
- Yellowdog Updater Modified (YUM)
	- YUM is a tool used with Red Hat-derived distributions. It is run from the command-line interface to manage, search, and install packages. YUM works with .rpm files.

### Types of shells
- Bourne-Again Shell (bash)
- C Shell (csh)
- Korn Shell (ksh)
- Enhanced C shell (tcsh)
- Z Shell (zsh)

### Standard input
Information received by the OS via the command line

### Standard output
Information returned by the OS through the shell

### Standard error
Error messages returned by the OS through the shell

### echo
A Linux command that outputs a specified string of text

## Modul 3

### Security analysts
- Work with server logs
- Navigate, manage and analyze files remotely
- Verify and configure users and group access
- Give authorization and set file permissions

### Bash
The default shell in most Linux distros

### Root directory
The highest-level directory in Linux

### pwd
Prints the working directory onto the screen

### ls
Displays the names of files and directories in the current working directory

### cd
Navigates between directories

### cat 
Displays the content of a file

### head
Displays just the beginning of a file, by default 10 lines

### Standard FHS directories

Directly below the root directory, you’ll find standard FHS directories. In the diagram, home, bin, and etc are standard FHS directories. Here are a few examples of what standard directories contain:

- **/home:** 
	- Each user in the system gets their own home directory.
    
- **/bin:** 
	- This directory stands for “binary” and contains binary files and other executables. Executables are files that contain a series of commands a computer needs to follow to run programs and perform other functions.
    
- **/etc:** 
	- This directory stores the system’s configuration files.
    
- **/tmp:** 
	- This directory stores many temporary files. The /tmp directory is commonly used by attackers because anyone in the system can modify data in these files.
    
- **/mnt:** 
	- This directory stands for “mount” and stores media, such as USB drives and hard drives.


### grep
Searches a specified file and returns all lines in the file containing a specified string

### | (piping)
Sends the standard output of one command as standard input to another command for further processing

### mkdir
Creates a new directory

### rmdir
Removes or deletes a directory

### touch
Creates a new file

### rm
Removes or deletes a file

### mv
Moves a file or directory to new location

### cp
Copies a file or directory into a new location

### Permissions
The type of access granted for a file or directory
- Read
- Write
- Execute

### Types of owners
- User
- Group
- Other

### Options
Modify the behaviour of the command

### ls -l
Displays permissions to files and directories

### ls -a
Displays hidden files

### ls -la
Previous 2 options combined

### chmod
Changes permissions on files and directories

### Root user (superuser)
A user with elevated privileges to modify the system

### Problems with logging in as root
- security risks
- Irreversible mistakes
- Accountability

### sudo
Temporarily grants elevated permissions to specific users

### useradd
Adds a user to the system
- -g: sets default group
- -G: set additional groups

### userdel
Deletes a user from the system

### usermod
Modifies existing users

- -a: used to append new groups
- .d: changes users home directory
- -l: changes users login name
- -L: Locks account

### chown
Changes ownership of a file or directory

### man
Displays information on other commands and how they work

### whatis
Displays a description of a command on a single line

### apropos
Searches the manual page descriptions for a specified string
