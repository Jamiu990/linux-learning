# Day 12: Standard Output to a File (`tee`)

## Overview

The Linux `tee` command allows you to **display command output in the terminal and save it to a file simultaneously**.

Unlike `>` which redirects output directly to a file, `tee` lets you view the output while saving it.

## 1. Writing Output with `>`

Use `echo` to write text to Day 11: Standard Output to a File (tee)

Overview

The Linux tee command allows you to display command output in the terminal and save it to a file simultaneously.

Unlike > which redirects output directly to a file, tee lets you view the output while saving it.

1. Writing Output with >

Use echo to write text to a file:

```bash
echo "Welcome to reality" > Naruto
```

Display the file contents:

```bash
cat Naruto
```

Output:
```text
Welcome to reality
```

2. Using tee

Replace > with | tee to display the text and save it to the file simultaneously.

```bash
echo "Golang is quite an interesting language" | tee go
```

The text appears in the terminal and is saved to go.

Verify the contents:

```bash
cat go
```

Note: By default, tee overwrites the file if it already exists.

3. Appending with tee -a

Use the -a option to append text without overwriting existing contents.

```bash
echo "Golang is fast as well and have beautiful syntax" | tee -a go
```

View the updated file:

```bash
cat go
```

Output:

```text
Golang is fast as well and have beautiful syntax
```

4. Counting Characters in a File

Use wc -c to count the bytes in a file:

```bash
wc -c go
```

The output includes the byte count and filename. For this file, the byte count includes the newline characters at the ends of the lines.

Important: wc -c counts bytes, not necessarily characters, because some characters occupy multiple bytes in UTF-8.


Summary

```tee``` displays output and writes it to a file simultaneously.

```tee -a``` appends output instead of overwriting the file.

```cat``` displays the contents of a file.

```wc -c``` counts the bytes in a file.a file:

``` bash
echo "Golang is quite an interesting language" > go
```

Display the file contents:

``` bash
cat go
```

**Output:**

``` text
Golang is quite an interesting language
```

## 2. Using `tee`

Replace `>` with `| tee` to display the text and save it to the file simultaneously.

``` bash
echo "Golang is quite an interesting language" | tee go
```

The text appears in the terminal and is saved to `go`.

Verify the contents:

``` bash
cat go
```

**Note:** By default, `tee` overwrites the file if it already exists.

## 3. Appending with `tee -a`

Use the `-a` option to append text without overwriting existing contents.

``` bash
echo "Golang is fast as well and has beautiful syntax" | tee -a go
```

View the updated file:

``` bash
cat go
```

**Output:**

``` text
Golang is quite an interesting language
Golang is fast as well and has beautiful syntax
```

## 4. Counting Characters in a File

Use `wc -c` to count the bytes in a file:

``` bash
wc -c go
```

The output includes the byte count and filename. For this file, the byte count includes the newline characters at the ends of the lines.

**Important:** `wc -c` counts bytes, not necessarily characters, because some characters occupy multiple bytes in UTF-8.

## Quick Reference

| Command | Purpose |
| --- | --- |
| `echo "text" > go` | Write text to a file |
| `echo "text" | tee go` | Display output and overwrite the file |
| `echo "text" | tee -a go` | Display output and append to the file |
| `cat go` | Display file contents |
| `wc -c go` | Count bytes in the file |

## Summary

- `tee` displays output and writes it to a file simultaneously.
- `tee -a` appends output instead of overwriting the file.
- `cat` displays the contents of a file.
- `wc -c` counts the bytes in a file.