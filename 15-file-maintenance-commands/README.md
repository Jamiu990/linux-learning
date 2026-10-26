# Day 15: Linux File Maintenance Commands

## Overview

Linux provides several commands for managing files and directories. In this lesson, I learned how to copy, remove, move, and create files and directories, as well as manage ownership.

### Commands Covered

| Command | Purpose |
|---|---|
| `cp` | Copies files and directories |
| `rm` | Removes files and directories |
| `mv` | Moves or renames files and directories |
| `mkdir` | Creates directories |
| `rmdir` | Removes empty directories |
| `chgrp` | Changes group ownership |
| `chown` | Changes user ownership and, optionally, group ownership |


## 1. The `cp` Command

The `cp` command copies files or directories from one location to another.

**Syntax:**

```bash
cp source destination
```

### Example 1: Copy a File

```bash
cp anime japanese
```

This creates a copy of the file `anime` named `japanese` in the current directory.

### Example 2: Copy a File into a Directory

```bash
cp anime /tmp
```

This copies `anime` into the `/tmp` directory.

Verify the copy:

```bash
cd /tmp
ls -ltr
```

**Note:** To copy a directory and its contents, use the recursive option `-r`:

```bash
cp -r source_dir destination_dir
```


## 2. The `rm` Command

The `rm` command removes files.

### Example: Create and Remove a File

Create a file:

```bash
touch gitignore
```

Add some text:

```bash
echo "Here is the list of items I want Git to ignore..." > gitignore
```

Remove the file:

```bash
rm gitignore
```

The file is deleted.

**Warning:** The `rm` command normally removes files without moving them to a recycle bin. Check the filename before executing it.


## 3. The `mv` Command

The `mv` command is used to **move or rename** files and directories.

### Example 1: Rename a File

Create a file:

```bash
touch noName
```

Rename it:

```bash
mv noName yesName
```

The file is now named `yesName`.

### Example 2: Move a File into a Directory

Create a file:

```bash
touch noName
```

Move it to `/tmp`:

```bash
mv noName /tmp
```

Verify the result:

```bash
cd /tmp
ls -ltr
```

The file `noName` should appear in the `/tmp` directory.


## 4. The `mkdir` Command

The `mkdir` command creates directories.

### Example

```bash
mkdir gameOfThrones
```

This creates a directory named `gameOfThrones` in the current working directory.

Verify it:

```bash
ls -ltr
```


## 5. The `rmdir` and `rm -r` Commands

Both commands can remove directories, but they behave differently.

### A. Using `rmdir`

The `rmdir` command removes an **empty directory**.

```bash
rmdir gameOfThrones
```

This removes `gameOfThrones` if it is empty.

### B. Using `rm -r`

The `rm -r` command removes a directory and its contents recursively.

```bash
rm -r gameOfThrones
```

Unlike `rmdir`, this can remove a directory containing files and subdirectories.

**Warning:** Use `rm -r` carefully because it can permanently delete an entire directory tree.


## 6. The `chgrp` and `chown` Commands

These commands manage file and directory ownership.

### A. `chgrp` — Change Group Ownership

```bash
chgrp developers anime
```

This changes the group ownership of `anime` to `developers`, provided the group exists and you have the necessary permissions.

### B. `chown` — Change User Ownership

```bash
chown user1 anime
```

This changes the owner of `anime` to `user1`, subject to system permissions.

You can also change both the user and group:

```bash
chown user1:developers anime
```

**Note:** Changing ownership often requires root privileges or `sudo`.


## Quick Reference

| Command | Example | Purpose |
|---|---|---|
| `cp` | `cp anime japanese` | Copy a file |
| `rm` | `rm gitignore` | Remove a file |
| `mv` | `mv noName yesName` | Rename a file |
| `mv` | `mv noName /tmp` | Move a file |
| `mkdir` | `mkdir gameOfThrones` | Create a directory |
| `rmdir` | `rmdir gameOfThrones` | Remove an empty directory |
| `rm -r` | `rm -r gameOfThrones` | Remove a directory and its contents |
| `chgrp` | `chgrp developers anime` | Change group ownership |
| `chown` | `chown user1 anime` | Change user ownership |


## Summary

In this lesson, I learned the basic Linux file maintenance commands:

- `cp` copies files and directories.
- `rm` removes files.
- `mv` moves or renames files and directories.
- `mkdir` creates directories.
- `rmdir` removes empty directories.
- `rm -r` removes directories and their contents.
- `chgrp` changes group ownership.
- `chown` changes user ownership and can also change group ownership.

These commands are essential for everyday Linux file management and system administration.