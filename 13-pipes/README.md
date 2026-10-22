# Day 13: Pipes

## Overview

A **pipe** connects the output of one command directly to the input of another command. This allows you to combine commands to process information without saving intermediate results to a file.

The pipe symbol is:

```bash
|
```

### Syntax

```bash
command1 [arguments] | command2 [arguments]
```

- `command1` produces output.
- `|` passes that output to the next command.
- `command2` processes the received input.

## 1. Using Pipes with `more`

The `more` command displays output one screen at a time.

```bash
ls -ltr | more
```

**Explanation:**
- `ls -ltr` lists files and directories, with the oldest modification times first.
- `| more` sends the listing to `more` so you can view it page by page.

This is useful when a directory listing is too long to fit on one screen.

## 2. Using Pipes with `tail`

The `tail` command displays the last lines of input or a file. By default, it displays the last 10 lines.

```bash
ls -l | tail -1
```

**Explanation:**
- `ls -l` produces a detailed directory listing.
- `|` passes the output to `tail`.
- `tail -1` displays only the final line of that output.

This is useful when you want to inspect the last line of a command's output.

**Note:** The result depends on the output produced by `ls -l`, including whether the directory contains files and how the command formats its listing.

## 3. Additional Examples

### Count Directory Entries

```bash
ls -1 | wc -l
```

This counts the lines produced by `ls -1`, giving the number of visible entries listed in the current directory. Hidden entries are excluded by default.

### Search Command Output

```bash
ls -l | grep ".txt"
```

This passes the detailed directory listing to `grep`, which displays lines containing `.txt`.

**Note:** This searches the displayed text for `.txt`; it is not a precise filename-extension filter.

### Display the First Five Lines

```bash
ls -ltr | head -5
```

This displays the first five lines of the listing.

## Quick Reference

| Command | Purpose |
|---|---|
| `ls -ltr | more` | View a listing one screen at a time |
| `ls -l | tail -1` | Display the last line of the listing |
| `ls -1 | wc -l` | Count listed entries |
| `ls -l | grep ".txt"` | Display lines containing `.txt` |
| `ls -ltr | head -5` | Display the first five lines |

## Summary

- A pipe (`|`) connects the output of one command to the input of another.
- Pipes allow you to combine commands without creating intermediate files.
- Commands such as `more`, `tail`, `head`, `wc`, and `grep` can be combined with pipes to filter or process output.