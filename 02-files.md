# Intro to Bash - Chapter 2. Files

## References
- http://tldp.org/LDP/intro-linux/html/sect_03_01.html

## Table of Contents
- Files and directories
- UNIX directory structure
- Creating and removing files
- Creating and removing directories
- File permissions

### Files and directories
> On a UNIX system, everything is a file; if something is not a file, it is a process.

Use the `ls` command to list the details of the specified directory, which
defaults to the current directory. Directories beginning with `/` are absolute
directories from the root file system. Meanwhile directories beginning with `./`
is a relative directory to the current directory. By default the relative directory
is used. The `~` refers to the current user's home directory.

```sh
# List files in current directory (relative).
ls
ls ../workspace
ls ./workspace
ls workspace

# List files in root directory (absolute).
ls /

# List files in user's home directory (absolute).
ls ~
```

### Unix directory structure
This structure is different between BSD file systems like MacOSX versus inux.

| Directory | Content |
|---|---|
| **/bin** | **Common programs shared by the system and users.** |
| /boot | The startup files, the vmlinuz kernel, and in some recent distributions grub data. Grub is the GRand Unified Boot loader and is an attempt to get rid of the many different boot-loaders we know today. |
| /dev | Contains references to all the CPU peripheral hardware, which are represented as files with special properties. |
| **/etc** | **Most important system configuration files are in /etc, this directory contains data similar to those in the Control Panel in Windows** |
| /home | Home directories of every user. |
| **/lib** | **Library files, includes files for all kinds of programs needed by the system and the users to compile and run code.** |
| /mnt | Standard mount point for external file systems, ex: USB, external hard-drives. |
| /opt | Typically contains extra third party software. |
| /root | The administrative user's home directory. Mind the difference between /, the root directory and /root, the home directory of the root user. |
| /sbin | Programs for use by the system and the system administrator. |
| **/tmp** | **Temporary space for use by the system, cleaned upon reboot, so don't use this for saving any work!** |
| **/usr** | **Programs, libraries, documentation etc. for all user-related programs.** |
| **/var** | **Storage for all variable files and temporary files created by users, such as log files, the mail queue, the print spooler area, space for temporary storage of files downloaded from the Internet, or to keep an image of a CD before burning it.** |


### Creating files
Everytime a file is created, it gets the following information:
- Owner and group owner of the file
- File type
- Permissions
- Date and time of creation, last read, and modified
- Number of symbolic links to this file
- File size
- Address of the file

**Note:** removing files via `rm` will permanantly remove them.

Creating files
```sh
# Create a single file.
touch index.js
touch README.md
```

### Creating and removing directories
- **Note:** removing directories via `rmdir` will permanantly remove them.

```sh
# Make a single folder.
mkdir myfolder

# Remove a single folder.
rmdir myfolder
```

```sh
# Make a parent and child folder.
mkdir -p parent/child

# Remove nested directories.
rm -rf parent
```

```sh
# Make multiple directories. These three are equivalent.
mkdir folder1 folder2 folder3
mkdir {folder1,folder2,folder3}
mkdir folder{1,2,3}

# Remove multiple directories.
rmdir folder{1,2,3}

# Make ranged directories.
mkdir hello{1..100}
rmdir hello{1..100}
```
