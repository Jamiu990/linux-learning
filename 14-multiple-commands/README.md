# Day 14: Executing Multiple Commands with `;`

## Overview

In Linux, the semicolon (`;`) allows you to execute multiple commands on a single line.

Commands separated by `;` run **sequentially and independently**. Each command runs after the previous command finishes, even if the previous command fails.

### Syntax

```bash
command1 ; command2 ; command3
```

---

## 1. Running Multiple Commands

```bash
ls ; pwd ; whoami
```

**Explanation:**
- `ls` lists files and directories in the current directory.
- `pwd` displays the current working directory.
- `whoami` displays the username of the current user.

The commands run one after another, regardless of whether an earlier command succeeds or fails.

## 2. Printing Multiple Messages

```bash
echo "Hello" ; echo "World"
```

**Output:**

```text
Hello
World
```

The first command prints `Hello`, and the second prints `World`.

## 3. Creating a Directory, Entering It, and Creating a File

```bash
mkdir test_dir ; cd test_dir ; touch test_file.txt
```

**Explanation:**
1. `mkdir test_dir` creates a directory named `test_dir`.
2. `cd test_dir` moves into that directory.
3. `touch test_file.txt` creates an empty file named `test_file.txt`.

This combines three operations into one line. Each command runs after the previous one finishes.

**Important:** If `mkdir test_dir` fails, the remaining commands still run. The `cd` command may also fail, and `touch` could create the file in the original directory. Use `&&` instead when each command should run only if the previous one succeeds.

## 4. Demonstrating Command Independence

```bash
ls ; invalid_command ; echo "Completed"
```

**Explanation:**
- `ls` lists the files and directories.
- `invalid_command` fails because it is not a recognized command.
- `echo "Completed"` still runs and prints `Completed`.

This demonstrates that the semicolon does not stop execution when a command fails.

## 5. Difference Between `;` and `&&`

The semicolon (`;`) runs the next command regardless of whether the previous command succeeds.

The double ampersand (`&&`) runs the next command **only if the previous command succeeds**.

**Using `;`:**

```bash
mkdir test_dir ; cd test_dir
```

The `cd` command runs even if creating the directory fails.

**Using `&&`:**

```bash
mkdir test_dir && cd test_dir
```

The `cd` command runs only if `mkdir test_dir` succeeds.

## Quick Reference

| Operator | Behavior | Example |
|---|---|---|
| `;` | Runs the next command regardless of success or failure | `ls ; pwd` |
| `&&` | Runs the next command only if the previous command succeeds | `mkdir test_dir && cd test_dir` |

## Summary

- The semicolon (`;`) allows multiple commands to be written on one line.
- Commands execute sequentially, regardless of earlier failures.
- The `&&` operator is useful when a command should run only after the previous command succeeds.