# Day 16: Linux File Display Commands

## Overview

Linux provides several commands for displaying file contents. In this lesson, I learned five useful commands:

- `cat`
- `more`
- `less`
- `head`
- `tail`

## 1. The `cat` Command

The `cat` command displays the contents of a file directly in the terminal.

**Example:**

```bash
cat notes.txt
```

This displays the entire contents of `notes.txt`.

You can also display multiple files:

```bash
cat file1.txt file2.txt
```

This displays the contents of both files sequentially.

**Best used for:** Reading short files quickly.


## 2. The `more` Command

The `more` command displays a file one screen at a time, making long files easier to read.

**Example:**

```bash
more notes.txt
```

**Useful keys:**
- `Space` — move to the next screen.
- `Enter` — move down one line.
- `q` — quit.

**Best used for:** Reading long files page by page.


## 3. The `less` Command

The `less` command allows you to view a file interactively and move both forward and backward through its contents.

**Example:**

```bash
less notes.txt
```

**Useful keys:**
- `Space` — move forward one screen.
- `b` — move backward one screen.
- `↑` / `↓` — move up or down one line.
- `/word` — search forward for `word`.
- `n` — jump to the next search match.
- `q` — quit.

**Best used for:** Navigating and searching large files.


## 4. The `head` Command

The `head` command displays the first 10 lines of a file by default.

**Example:**

```bash
head notes.txt
```

Display the first five lines:

```bash
head -n 5 notes.txt
```

This is useful when you want to inspect the beginning of a file without displaying everything.

**Best used for:** Checking the beginning of files and logs.


## 5. The `tail` Command

The `tail` command displays the last 10 lines of a file by default.

**Example:**

```bash
tail notes.txt
```

Display the last three lines:

```bash
tail -n 3 notes.txt
```

To monitor a file as new lines are added, use:

```bash
tail -f application.log
```

Press `Ctrl + C` to stop monitoring.

**Best used for:** Checking recent entries in log files and monitoring ongoing activity.


## Quick Reference

| Command | Purpose | Example |
|---|---|---|
| `cat` | Displays the entire file | `cat notes.txt` |
| `more` | Displays a file one screen at a time | `more notes.txt` |
| `less` | Navigates forward and backward through a file | `less notes.txt` |
| `head` | Displays the first 10 lines by default | `head notes.txt` |
| `tail` | Displays the last 10 lines by default | `tail notes.txt` |
| `tail -f` | Follows new lines added to a file | `tail -f application.log` |

## Summary

- Use `cat` to display short files quickly.
- Use `more` to read files one screen at a time.
- Use `less` to navigate through large files and search their contents.
- Use `head` to inspect the beginning of a file.
- Use `tail` to inspect the end of a file or monitor new log entries.

These commands are essential for reading files, reviewing logs, and inspecting information from the Linux terminal.