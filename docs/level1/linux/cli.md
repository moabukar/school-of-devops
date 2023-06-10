# Command Line Basics

## What is a Command

A command is a program that tells the operating system to perform specific work. Programs are stored as files in Linux. Therefore, a command is also a file that is stored somewhere on the disk.

Commands may also take additional arguments as input from the user. These arguments are called command line arguments. Knowing how to use the commands is important, and there are many ways to get help in Linux, especially for commands. Almost every command will have some form of documentation. Most commands will have a command-line argument `-h` or `--help` that will display a reasonable amount of documentation. But the most popular documentation system in Linux is called man pages, short for manual pages.

To show the documentation for the `cat` command using the `--help` option:

```bash
cat --help
```

## File system hierarchy

The Linux file system follows a hierarchical structure, forming a tree-like directory structure with the highest level directory called the root (denoted by `/`). The directories within the root directory store various types of files related to the system, applications, and users.

Here are some of the key directories and their purposes:

- `/bin`: This directory contains executable programs for commonly used commands.
- `/dev`: Files related to devices on the system are stored in this directory.
- `/etc`: System configuration files are stored in this directory.
- `/home`: User-related files and directories are stored in this directory.
- `/lib`: Library files are stored in this directory.
- `/mnt`: Files related to mounted devices on the system can be found in this directory.
- `/proc`: This directory contains files related to running processes on the system.
- `/root`: User-related files and directories for the root user are stored here.
- `/sbin`: Programs used for system administration purposes are stored in this directory.
- `/tmp`: This directory is used to store temporary files on the system.
- `/usr`: Application programs are stored in this directory.

Please note that this is just a brief overview of the file system organization in Linux. Each directory serves a specific purpose and contains various files and subdirectories relevant to that purpose.

Understanding the file system structure is essential for navigating and managing files and directories in Linux. It provides a foundation for effective file system management and organization.

## Commands for Navigating the File System

The 3 basic commands which are used frequently to navigate the file system:

- `ls`

- `cd`

- `pwd`

Let's now try these commands.

### `ls` (print working directory)

The ls command is used to list the contents of a directory. It will list down all the files and folders present in the given directory.

```
ls
```

### `cd` (change directory)

The cd command can be used to change the working directory. Using the
command, you can move from one directory to another.

```
cd /etc
```

The above command will go to the /etc directory.


### `pwd` (list files and directories)


## Commands for Manipulating Files

The 5 basic commands which are used frequently to manipulate files:

- `touch`

- `mkdir`

- `mv`

- `rm`

- `cp`

Let's now try these commands.

### `touch` (create new file)

The touch command can be used to create an empty new file.

```
touch file.txt
```

### `mkdir` (create new directories)

The mkdir command is used to create directories.You can use ls command to verify that the new directory is created.

```
mkdir directory_name
```

### `mv` (move files and directories)

The mv command can either be used to move files or directories from one location to another or it can be used to rename files or directories. Do note that moving files and copying them are very different. When you move the files or directories, the original copy is lost.

General usage of the mv command:

```
mv source_path destination_path
```


### `rm` (delete files and directories)

The rm command can be used to delete files and directories. It is very important to note that this command permanently deletes the files and directories. It's nearly impossible and rare to recover these files and directories once you have executed the rm command. Run this command carefully.

General usage of the rm command:

```
rm file_name
```

### `cp` (copy files and directories)

The cp command is used to copy files and directories from one location to another.

General usage of the cp command:

```
cp <source_path> <destination_path>
```

## Commands for Viewing Files

The 5 basic commands that are used frequently to view files:

- `cat`

- `head`

- `tail`

- `more`

- `less`

### `cat` (view content of a file)

The most frequenet use of cat command is to print the contents of the file on your output screen. 

```
cat file.txt
```

### `head`

The head command displays the first 10 lines of the file by default. You can include additional flags to display as many lines as we want from the top.

```
head file.txt
```

Other usage:

```
head -n 10 file.txt
```

`
### `tail`

The tail command displays the last 10 lines of the file by default. You can include additional flags to display as many lines as we want from the end of the file.

```
tail file.txt
```

Other usage:

```
tail -n 10 file.txt
```

### `more`

The more command displays the contents of a file or a command output, displaying one screen at a time in case the file is large (Eg: log files). It also allows forward navigation and limited backward navigation in the file.

```
more file.txt
```

### `less` 

The `less` command is an improved version of `more`. It allows you to view the contents of a file or the output of a command, one page at a time. `less` provides various navigation options and features, making it a versatile tool for reading and exploring large files.

To use `less` with a file, simply type:

```
less filename
```

## The echo Command in Linux

The echo command is one of the simplest commands that is used in the
shell. This command is equivalent to what we have <print> in other
programming languages.

The echo command prints the given input string on the screen.