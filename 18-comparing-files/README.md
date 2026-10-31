# Day 18 — Comparing Files in Linux

Linux provides commands for comparing two files to identify differences between them. Two commonly used commands are `diff` and `cmp`.

## 1. `diff` — Comparing Files Line by Line

The `diff` command compares two files line by line and displays the differences between them.

**Syntax:**

```bash
diff filename1 filename2
```

**Example:**

```bash
diff file1.txt file2.txt
```

Compares `file1.txt` and `file2.txt` and displays the lines that are different.

**Common option:**

```bash
diff -u file1.txt file2.txt
```

Displays the differences in a unified format, making them easier to read.

## 2. `cmp` — Comparing Files Byte by Byte

The `cmp` command compares two files byte by byte. It reports the first position where the files differ.

**Syntax:**

```bash
cmp filename1 filename2
```

**Example:**

```bash
cmp file1.txt file2.txt
```

Compares both files and reports the first difference, if one exists.

**Common option:**

```bash
cmp -s file1.txt file2.txt
```

Compares the files silently without displaying differences. It returns an exit status that indicates whether the files are identical.

## Difference Between `diff` and `cmp`

| Command | How It Compares | What It Shows |
|---|---|---|
| `diff` | Line by line | The lines that differ between files. |
| `cmp` | Byte by byte | The first byte position where files differ. |

## Key Takeaway

- Use `diff` when you want to see which lines have changed between two text files.
- Use `cmp` when you want to check whether two files are identical at the byte level.

Both commands are useful when checking file changes, verifying copies, and identifying differences between files.