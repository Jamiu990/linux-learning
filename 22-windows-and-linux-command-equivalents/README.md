# Day 22 — Windows and Linux Command Equivalents

Windows and Linux use different commands to perform similar tasks. Understanding their equivalents makes it easier to work across both operating systems.

This lesson compares common Windows commands with their Linux equivalents.

## 1. Windows and Linux Command Comparison

| Windows Command | Linux Equivalent | Purpose |
|---|---|---|
| `dir` | `ls -l` | Lists files and directories with details. |
| `ren` | `mv` | Renames files or directories. |
| `copy` | `cp` | Copies files. |
| `move` | `mv` | Moves files or directories. |
| `cls` | `clear` | Clears the terminal screen. |
| `del` | `rm` | Deletes files. |
| `fc` | `diff` | Compares two files and displays differences. |
| `find` | `grep` | Searches for text inside files. |
| `command /?` | `man command` | Displays a command's manual. |
| `chdir` | `pwd` | Displays the current working directory. |
| `time` | `date` | Displays the current date and time. |

## 2. Understanding the Linux Commands

### `ls -l` — Listing Files and Directories

```bash
ls -l
```

Displays files and directories in the current directory with additional information, including permissions, ownership, size and modification date.

### `mv` — Renaming and Moving Files

**Renaming a file:**

```bash
mv oldname.txt newname.txt
```

Changes the filename from `oldname.txt` to `newname.txt`.

**Moving a file:**

```bash
mv file.txt /home/user/Documents/
```

Moves `file.txt` into the Documents directory.

The `mv` command performs both renaming and moving operations.

### `cp` — Copying Files

```bash
cp file.txt backup.txt
```

Creates a copy of `file.txt` named `backup.txt`.

The original file remains unchanged.

### `clear` — Clearing the Terminal

```bash
clear
```

Clears the visible terminal screen without deleting files or affecting running programs.

### `rm` — Removing Files

```bash
rm file.txt
```

Deletes `file.txt`.

To remove multiple files:

```bash
rm file1.txt file2.txt
```

**Note:** Linux does not normally send files deleted with `rm` to a recycle bin. Be careful when using this command.

### `diff` — Comparing Files

```bash
diff file1.txt file2.txt
```

Compares two files line by line and displays their differences.

### `grep` — Searching for Text

```bash
grep "Linux" filename.txt
```

Searches for the word `Linux` inside `filename.txt` and displays matching lines.

### `man` — Reading Command Manuals

```bash
man ls
```

Displays the manual page for the `ls` command.

To leave the manual page, press `q`.

You can replace `ls` with another command to view its manual.

### `pwd` — Displaying the Current Directory

```bash
pwd
```

Displays the full path of the directory you are currently working in.

For example:

```text
/home/user/Documents
```

### `date` — Displaying the Date and Time

```bash
date
```

Displays the current system date and time.

---

## 3. Important Differences to Remember

- `mv` can rename and move files, while `cp` creates copies.
- `rm` permanently removes files under normal Linux usage.
- `diff` compares file contents, while `grep` searches for specific text.
- `pwd` displays your current directory; it does not change directories. Use `cd` to move between directories.
- `date` displays the date and time, while `time` in Linux is commonly used to measure how long a command takes to execute.

## Key Takeaway

Learning Windows and Linux command equivalents makes switching between operating systems easier.
