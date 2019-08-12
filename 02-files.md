# Intro to Bash - Chapter 1. Sessions and Jobs

## Table of Contents
- Files and directories
- Creating and removing files
- Creating and removing directories


### Creating files
Note: removing files via `rm` will permanantly remove them.

Creating files
```

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
