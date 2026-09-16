# Linux Help Commands

## Overview

Linux provides several built-in ways to get information about commands. These help commands are useful when you need to understand what a command does, see its available options, or read detailed documentation.

There are **three common types of help commands**:

1. `whatis`
2. `--help`
3. `man`


## 1. `whatis` Command

The `whatis` command provides a **short description** of a Linux command.

### Syntax

```bash
whatis command
```

### Examples

```bash
whatis ls
```

```bash
whatis pwd
```

This is useful when you only need a quick explanation of what a command does.


## 2. `--help`

Many Linux commands support the `--help` option. It displays information about how to use the command, including its available options and arguments.

### Syntax

```bash
command --help
```

### Examples

```bash
ls --help
```

```bash
chmod --help
```

This is useful when you need a quick reference for a command's syntax and options.


## 3. `man` Command

The `man` command opens the **manual page** for a command.

Manual pages provide more detailed documentation, including the command's description, syntax, options, and other relevant information.

### Syntax

```bash
man command
```

### Examples

```bash
man ls
```

```bash
man pwd
```

To exit a manual page, press:

```text
q
```


## Quick Reference

| Help Method | Purpose                             | Example     |
| ----------- | ----------------------------------- | ----------- |
| `whatis`    | Gives a short description           | `whatis ls` |
| `--help`    | Shows usage and available options   | `ls --help` |
| `man`       | Opens detailed manual documentation | `man ls`    |


## Summary

The three help methods covered in this lesson are:

```bash
whatis command
command --help
man command
```

These commands are important for learning Linux because they allow you to **find information directly from the system** instead of having to memorize every command and option.