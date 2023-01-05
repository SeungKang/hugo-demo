---
title: "Process Treasure Hunt"
date: 2023-01-03T21:53:14-05:00
draft: false
tags: [shell]
---

**POSIX (Portable Operating System Interfaces)** is a standard that attempted to standardize a bunch of stuff about computers such as manual pages for software.

[Site for Manual Standard](https://pubs.opengroup.org/onlinepubs/9699919799.2008edition/)
> Base Definitions > 12. Untility Conventions\
> Shell & Utilities > 1. Introduction > 1.4 Utility Description Defaults

    [name of the program] -[options]
Details about a program and be found in the manual by using `man COMMAND NAME`

## Shell Commands

**cat:** is generally used to concatenate the files and gives the output on the standard output

**more:** is a filter for paging through text one screenful at a time

**less:** used for viewing files, similar to more but it allows forward and backward movement

**tail:** used to print the last lines of a file\
**tail -f nohup.out:** -f outputs the appended data as the file grows

**doas:** execute commands as another user, run as root\
**doas su -:** su allows user to run a shell with the user and group ID of another user

**procstat:** get detailed process information\
**procstat -e PID#:** view environment variables for the process\
**procstat -f PID#:** to view file descriptors for the process

**ps:** shows the status of processes\
**ps -aux -www:** -a writes to standard output information about all processes, -w additional w's help the output from getting cropped by the window

**cd DIRECTORY:** change the current working directory\
**cd ..:** moves the user up one directory\
**cd .:** will leave the user in the same directory\
**cd:** will put the user in their home directory

**pwd:** show the present working directory

**mkdir:** create a directory

**cp:** copy the files and directories from the source path to the destination path

**mv:** used to move files or directories

**rm:** used to remove files or directions

**chmod:** used to modify the access/permissions of a user

**grep:** used to search for the specified text in a file

**ls:** lists the files and directores in the current working directory\
**ls -la:** -l lists files in the long format -a lists all the entries including hidden files

