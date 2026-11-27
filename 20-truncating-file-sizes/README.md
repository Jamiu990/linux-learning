# Day 20 — Truncating File Sizes in Linux

The `truncate` command is used to reduce or increase the size of an existing file to a specified size.

It can:
- Shrink a file by removing content from the end.
- Extend a file by adding null bytes (`\0`) to the end.

## 1. Shrinking a File

**Syntax:**

```bash
truncate -s SIZE filename
```

**Example:**

```bash
truncate -s 5K sample.txt
```

Reduces or sets the size of `sample.txt` to exactly 5 kilobytes.

If the file was originally larger, the content beyond the specified size will be removed.

## 2. Extending a File

You can also use `truncate` to increase a file's size.

**Example:**

```bash
truncate -s 10K sample.txt
```

Sets the file size to exactly 10 kilobytes.

If the file was originally smaller, the additional space is filled with null bytes (`\0`).

**Important:** Extending a file with `truncate` does not add readable text. It increases the file size using null bytes.

## 3. Checking File Size

You can use `ls -lh` to check the file size.

```bash
ls -lh sample.txt
```

Displays the file size in a human-readable format, such as KB or MB.

You can also use:

```bash
du -h sample.txt
```

Displays the disk space occupied by the file. Note that this may differ from the file's actual size, especially for sparse files.

## Summary

| Command | Purpose |
|---|---|
| `truncate -s 5K sample.txt` | Sets the file size to 5 KB. |
| `truncate -s 10K sample.txt` | Sets the file size to 10 KB. |
| `ls -lh sample.txt` | Displays the file's size. |
| `du -h sample.txt` | Displays the disk space used by the file. |

## Key Takeaway

The `truncate` command sets a file to an exact size.

- If the specified size is smaller, content at the end is removed.
- If the specified size is larger, null bytes are added.
- Be careful when shrinking files because removed content cannot normally be recovered.