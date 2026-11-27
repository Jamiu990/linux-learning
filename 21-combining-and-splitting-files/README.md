# Day 21 — Combining and Splitting Files in Linux

Linux provides commands for combining multiple files into one and splitting a large file into smaller files.

The two commands covered in this lesson are:

- `cat` — Combines the contents of multiple files.
- `split` — Divides a file into smaller files.

## 1. `cat` — Combining Multiple Files

The `cat` command can display file contents or combine the contents of multiple files.

You can use output redirection (`>`) to save the combined contents into a new file.

**Syntax:**

```bash
cat file1 file2 file3 > file4
```

**Example:**

```bash
cat first.txt second.txt third.txt > combined.txt
```

This command:
1. Reads the contents of `first.txt`.
2. Reads the contents of `second.txt`.
3. Reads the contents of `third.txt`.
4. Combines their contents in that order.
5. Saves the result in `combined.txt`.

**Important:** The `>` operator creates the destination file if it doesn't exist. If it already exists, its previous contents will be overwritten.

To check the combined file:

```bash
cat combined.txt
```

## 2. `split` — Splitting a File

The `split` command divides a file into smaller files.

You can specify how many lines each smaller file should contain.

**Syntax:**

```bash
split -l NUMBER filename prefix
```

**Example:**

```bash
split -l 2 names.txt sep
```

This command splits `names.txt` into smaller files containing two lines each.

The parts are automatically named using the specified prefix.

For example:

```text
sepaa
sepab
sepac
sepad
```

If `names.txt` contains eight lines, Linux creates four smaller files, each containing two lines.

### Understanding the options

| Option | Meaning |
|---|---|
| `-l` | Specifies the number of lines each smaller file should contain. |
| `2` | Sets each output file to contain two lines. |
| `names.txt` | The original file being split. |
| `sep` | The prefix used when naming the smaller files. |

### Checking the split files

```bash
ls sep*
```

Displays files whose names begin with `sep`.

To view the contents of one of the smaller files:

```bash
cat sepaa
```

## Summary

| Command | Purpose |
|---|---|
| `cat file1 file2 > file3` | Combines two files into one. |
| `split -l 2 filename prefix` | Splits a file into smaller files containing two lines each. |
| `ls prefix*` | Lists files created with the specified prefix. |

## Key Takeaway

- Use `cat` with `>` when you want to combine the contents of multiple files.
- Use `split -l` when you want to divide a file based on the number of lines.
- Linux automatically creates the smaller files using the prefix you provide.

These commands are useful when organizing text files or working with large files that need to be processed in smaller sections.