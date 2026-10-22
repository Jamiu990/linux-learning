# Day 11: Input and Output Redirection

## Overview

In Linux, commands receive input and produce output. By default, input usually comes from the keyboard, while output and error messages are displayed in the terminal.

Linux provides **three standard streams** that allow us to control how commands receive input and where their output goes.

The three standard streams are:

1. **Standard Input (`stdin`)** — file descriptor `0`
2. **Standard Output (`stdout`)** — file descriptor `1`
3. **Standard Error (`stderr`)** — file descriptor `2`

Redirection allows us to send these streams to files or other destinations instead of using their default locations.


## 1. Standard Output (`stdout`) — File Descriptor 1

Standard output is the stream a command uses to produce its normal results.

By default, standard output is displayed in the terminal. However, we can redirect it to a file using the `>` operator.

### A. Redirecting Output to a File

**Example 1:**

```bash
ls -l > listings
```

This command displays a detailed listing of the current directory and redirects the output into a file named `listings`.

If the file does not exist, Linux creates it. If it already exists, its contents are overwritten.

**Example 2:**

```bash
pwd > findpath
```

The `pwd` command prints the current working directory. The `>` operator saves that path in a file named `findpath`.

To view the saved output, use:

```bash
cat findpath
```

### B. Appending Output to a File

The `>>` operator appends output to the end of a file without removing its existing contents.

**Example 1:**

```bash
ls -la >> listings
```

This appends the output of `ls -la` to the existing `listings` file.

**Example 2:**

```bash
echo "Hello world" >> findpath
```

This adds the text `Hello world` to the end of `findpath`.

To inspect the updated file, run:

```bash
cat findpath
```

### Difference Between `>` and `>>`

| Operator | Function | Effect on Existing Contents |
|---|---|---|
| `>` | Redirects output to a file | Overwrites existing contents |
| `>>` | Appends output to a file | Preserves existing contents and adds new output |


## 2. Standard Input (`stdin`) — File Descriptor 0

Standard input is the stream a command uses to receive data.

By default, standard input comes from the keyboard. However, we can use the `<` operator to redirect input from a file.

### A. Reading Input from a File

**Example:**

```bash
cat < listings
```

This command redirects the contents of `listings` to the standard input of `cat`.

The `cat` command reads the input and displays it in the terminal.

For this simple example, the command below produces essentially the same result:

```bash
cat listings
```

The `<` operator becomes more useful when a command expects to receive input through standard input.

### B. Redirecting a File into an Email Command

Consider the following example:

```bash
mail -s "Office memo" tosomeone@earth.org < memoletter
```

This command uses the contents of `memoletter` as the standard input for the `mail` command.

The options and arguments mean:

- `mail` — invokes the mail command-line utility.
- `-s "Office memo"` — sets the email subject to `Office memo`.
- `tosomeone@earth.org` — specifies the recipient.
- `< memoletter` — supplies the contents of `memoletter` as the email message body.

**Note:** Sending the email requires a working mail utility and a properly configured mail system. The example address is illustrative.

### Key Point

The `<` operator redirects input from a file into a command.

```bash
command < inputfile
```


## 3. Standard Error (`stderr`) — File Descriptor 2

Standard error is the stream used by commands to display error messages.

For example, if a command tries to access a file or directory that does not exist or that the current user cannot access, it may produce an error message.

By default, error messages are usually displayed in the terminal, just like normal output. However, standard output and standard error are separate streams, so they can be redirected independently.

### A. Redirecting Error Messages to a File

Consider this command:

```bash
ls -l /root 2> errorfile
```

The command attempts to list the contents of `/root` in long format.

The components are:

- `ls -l /root` — attempts to display a detailed listing of `/root`.
- `2>` — redirects standard error, identified by file descriptor `2`.
- `errorfile` — the file where error messages are saved.

If the command produces an error, that error message is written to `errorfile` instead of being displayed in the terminal.

If `errorfile` does not exist, Linux creates it. If it already exists, its previous contents are overwritten.

To inspect the file, run:

```bash
cat errorfile
```

**Important:** The `/root` directory is normally restricted to the root user. If your account does not have permission to access it, you may receive a permission-denied error. If the command succeeds without producing an error, `errorfile` will contain no error message.

### B. Appending Error Messages

You can append error messages instead of overwriting an existing error log.

Use `2>>`:

```bash
ls -l /root 2>> errorfile
```

This appends any new error messages to the end of `errorfile`.


## 4. Understanding the Three Standard Streams

When you execute a command in Linux, the following streams are involved:

### Standard Input — `stdin` (0)

This is where a command receives input. By default, input usually comes from the keyboard.

Example:

```bash
cat < listings
```

### Standard Output — `stdout` (1)

This is where a command sends its normal output. By default, it is displayed in the terminal.

Example:

```bash
ls -l > listings
```

### Standard Error — `stderr` (2)

This is where a command sends error messages. By default, these messages are displayed in the terminal.

Example:

```bash
ls -l /root 2> errorfile
```

### Summary Table

| Stream | Name | File Descriptor | Default Destination or Source | Example |
|---|---|---|---|---|
| Standard Input | `stdin` | `0` | Keyboard or terminal input | `cat < listings` |
| Standard Output | `stdout` | `1` | Terminal | `ls -l > listings` |
| Standard Error | `stderr` | `2` | Terminal | `ls -l /root 2> errorfile` |


## 5. Additional Practical Examples

### Example 1: Save Normal Output

```bash
date > currentdate
```

This saves the current date and time in a file named `currentdate`.

Read the file:

```bash
cat currentdate
```

### Example 2: Append Normal Output

```bash
pwd >> currentdate
```

This appends the current working directory to the same file.

### Example 3: Save Error Messages

```bash
ls /directory_that_does_not_exist 2> errors.txt
```

If the directory does not exist, the error message is saved in `errors.txt`.

Read the file:

```bash
cat errors.txt
```

### Example 4: Redirect Normal Output and Errors Separately

```bash
ls -l /root > output.txt 2> errors.txt
```

This sends normal output to `output.txt` and error messages to `errors.txt`.

If the command produces no normal output because access is denied, `output.txt` may be empty while `errors.txt` contains the error message.

### Example 5: Redirect Both Output and Errors to the Same File

In Bash, you can redirect both standard output and standard error to one file:

```bash
ls -l /root > results.txt 2>&1
```

Here:

- `> results.txt` redirects standard output to `results.txt`.
- `2>&1` redirects standard error to the same destination as standard output.

This is useful when you want to capture both normal results and error messages in one file.

**Note:** The order matters. `> results.txt 2>&1` sends both streams to the file. Reversing the order can produce a different result.


## 6. Quick Reference

| Command | Purpose |
|---|---|
| `ls -l > listings` | Save normal output to a file |
| `pwd > findpath` | Save the current directory path |
| `ls -la >> listings` | Append normal output to a file |
| `echo "Hello world" >> findpath` | Append text to a file |
| `cat < listings` | Redirect file contents to standard input |
| `ls -l /root 2> errorfile` | Save error messages to a file |
| `ls -l /root 2>> errorfile` | Append error messages to a file |
| `ls -l /root > output.txt 2> errors.txt` | Save normal output and errors separately |
| `ls -l /root > results.txt 2>&1` | Save normal output and errors in the same file |


## Summary

In this lesson, I learned about the three standard streams in Linux:

- **Standard Input (`stdin`, descriptor `0`)** receives data.
- **Standard Output (`stdout`, descriptor `1`)** carries normal command output.
- **Standard Error (`stderr`, descriptor `2`)** carries error messages.

I also learned how to use redirection operators to control these streams:

- `<` redirects input from a file.
- `>` redirects output to a file, replacing its existing contents.
- `>>` appends output to a file.
- `2>` redirects error messages to a file.
- `2>>` appends error messages to a file.
- `2>&1` redirects standard error to the current destination of standard output.

Understanding input and output redirection is an important Linux skill because it allows you to save command results, capture errors, and manage information more effectively from the command line.