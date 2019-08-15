# Chapter 2. Files and Permissions

## Table of Contents
- Files and directories
- UNIX directory structure
- Creating and removing files
- Creating and removing directories
- Moving files and directories
- File permissions

### Files and directories
http://tldp.org/LDP/intro-linux/html/sect_03_01.html

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
This structure is different between BSD file systems like MacOSX versus Linux.

| Directory | Content |
|---|---|
| /bin | Common programs shared by the system and users. |
| /boot | The startup files, the vmlinuz kernel, and in some recent distributions grub data. Grub is the GRand Unified Boot loader and is an attempt to get rid of the many different boot-loaders we know today. |
| /dev | Contains references to all the CPU peripheral hardware, which are represented as files with special properties. |
| /etc | Most important system configuration files are in /etc, this directory contains data similar to those in the Control Panel in Windows |
| /home | Home directories of every user. |
| /lib | Library files, includes files for all kinds of programs needed by the system and the users to compile and run code. |
| /mnt | Standard mount point for external file systems, ex: USB, external hard-drives. |
| /opt | Typically contains extra third party software. |
| /root | The administrative user's home directory. Mind the difference between /, the root directory and /root, the home directory of the root user. |
| /sbin | Programs for use by the system and the system administrator. |
| /tmp | Temporary space for use by the system, cleaned upon reboot, so don't use this for saving any work! |
| /usr | Programs, libraries, documentation etc. for all user-related programs. |
| /var | Storage for all variable files and temporary files created by users, such as log files, the mail queue, the print spooler area, space for temporary storage of files downloaded from the Internet, or to keep an image of a CD before burning it. |


### Creating files
Everytime a file is created, it gets the following information:
- Owner and group owner of the file
- File type
- Permissions
- Date and time of creation, last read, and modified
- Number of symbolic links to this file
- File size
- Address of the file


### Creating and removing files
Note: removing files via `rm` will permanantly remove them.

```sh
# Create a single file.
touch index.js
touch README.md

# Remove single file.
rm index.js
```

```sh
# Create multiple files.
touch index.html index.css index.js
touch index.{html,css,js}

# Remove multiple files.
rm index.html index.css index.js
rm index.{html,css,js}
```

Sidenote: You can use `touch` to change the modify/access date of a file.
```sh
touch -t YYYYMMDDHHMM.SS filename
touch -t 201212211111 index.{html,css,js}
```

### Creating and removing directories
Note: removing directories via `rmdir` will permanantly remove them.

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

### Moving files and directories
The `mv` command is used to move and rename files and directoies. If a file
already exists you will be prompted to overrwrite the existing file.

```sh
# Renaming index.html to hello.html
mv index.html hello.html

# Moving index.html to the tmp directory
mv index.html /tmp/index.html
```

The `rename` command is useful for renaming files using pattern matching. It
uses sed-like syntax with perl regular expressions.

```sh
# Replace all spaces with dashes (using sed substitute).
rename 's/ /\-/g' *

# Use -n to perform a dry run (using sed substitute).
rename -n 's/ /-/g' *

# Rename all uppercase letters to lowercase (using sed transform).
rename -f 'y/A-Z/a-z/' *

# Rename all lowercase letters to uppercase (using sed transform).
rename -f 'y/a-z/A-Z/' *
```


### File permissions
Linux permissioning is based on the **principle of least privilege**.

Use `ls` to list files and permissions.
```sh
$ ls -lah

total 0
drwxr-xr-x   5 jorgeyaulee  wheel   160B Aug 14 15:31 .
drwxrwxrwt  28 root         wheel   896B Aug 14 14:27 ..
-rw-r--r--   1 jorgeyaulee  wheel     0B Aug 14 15:31 index.css
-rw-r--r--   1 jorgeyaulee  wheel     0B Aug 14 15:31 index.html
-rw-r--r--   1 jorgeyaulee  wheel     0B Aug 14 15:31 index.js
```

Breakdown
```sh
# Permissions.
d (directory)
rwx (user read, write, execute)
rwx (group read, write, execute)
rwx (other read, write, execute)
t (root)

# Owner.
jorgeyaulee

# Group.
wheel
```

Granting and revoking permissions (standard format).
```sh
# Revoke (user) (executable) permissions.
chmod u+x index.html

# Revoke (user) (executable) permissions.
chmod u-x index.html

# Grant (user, guest, other) (executable) permissions.
chmod ugo+x index.html

# Revoke (user, guest, other) (executable) permissions.
chmod ugo-x index.html

# Granting all users all permissions.
chmod ugo+rwx index.html

# Revoking all users all permissions.
chmod ugo-rwx index.html
```

Granting and revoking permissions (octal format).
```sh
# Granting all users all permissions.
chmod 777 index.html

# Grant only user all permissions.
chmod 700 index.html

# Revoking all users all permissions.
chmod 000 index.html
```

Changing owners.
```sh
chown <user> <file>
chown root index.html
```

#### Sudo
As a last resort, use `sudo` (superuser do) to grant the current user
superuser access to a command, which bypasses all permissions.
```sh
sudo chmod 700 index.html
```

Sudo also leaves an audit trail of all elevated commands and attempts.
```sh
```

As a **break-glass last resort**, switch to the root user.
You will be able to read, modify, delete any file as well
as start and kill any
```sh
sudo su -
whoami
```
