# Linux File Searching, Wildcards, File Types and Links

This directory contains my notes and practical exercises from Day 3 of my Linux learning journey.

## Topics Covered

- Searching for files as the root user
- `find` vs. `locate`
- Updating the locate database
- Wildcards
- Removing files with `rm`
- Using wildcards with commands
- Linux file types
- Inodes
- Hard links and soft links
- Writing to and reading files

## 1. Searching for Files as the Root User

Some files and directories in a Linux system may not be accessible to a normal user because of permissions.

When necessary, I can switch to the root user using:

`su - root`

After entering the root user's password, I can perform operations with root privileges.
To leave the root shell and return to the previous user:

`exit`

**Note**: Being root is not always necessary to use commands such as find. Whether a file can be searched or accessed depends on the permissions of the directories involved.

## 2. find vs. locate

Linux provides several ways to search for files and directories. Two common commands are `find` and `locate`.

### `find`

The `find` command searches the filesystem directly.

It normally requires a path and can be used with different search options.

For example:

```bash
find / -name "filename"
```

The `/` tells find to start searching from the root of the filesystem.

`find` is very flexible and can search based on different conditions.

### `locate`

The `locate` command searches an internal database containing file paths rather than searching the filesystem directly.

For example:

```bash
locate filename
```

Because it searches a database, `locate` is generally much faster than `find`.
However, its results can become outdated if the database has not been updated since a file was created, renamed, or removed.

## 3. Updating the locate Database

The database used by locate can be updated manually with:

```bash
updatedb
```

On some Linux systems, running `updatedb` requires root privileges.

I can switch to the root user first:

```bash
su - root
```

Then update the database:

```bash
updatedb
```

Afterward, I can leave the root shell:

```bash
exit
```

The main difference between the two commands can be summarized as:

| Command | How it searches | Speed | Main characteristic |
| --- | --- | --- | --- |
| `find` | Searches the filesystem | Generally slower | Very flexible |
| `locate` | Searches an indexed database | Generally faster | Results depend on database freshness |


## 4. Wildcards

A wildcard is a special character that can represent one or more characters when matching filenames.

Some commonly used shell wildcards are:

| Wildcard | Meaning |
| --- | --- |
| `*` | Matches zero or more characters |
| `?` | Matches exactly one character |
| `[ ]` | Matches one character from a specified set or range |


## 5. The `*` Wildcard

The `*` wildcard represents zero or more characters.

For example:

```bash
ls -l abc*
```

This can list files whose names begin with `abc`.

Another example:

```bash
rm abcd*
```

This removes files whose names begin with `abcd`.

The `*` can also be used at the beginning:

```bash
rm *xyz
```

This removes files whose names end with `xyz`.

It can also appear in the middle:

```bash
rm *xy*
```

This matches filenames containing `xy`.

**Warning**: Be extremely careful when using `rm` with wildcards. A pattern can match many files, and `rm` can permanently remove them.


## 6. The `?` Wildcard

The `?` wildcard represents exactly one character.

For example:

```bash
ls -l ?bcd*
```

The `?` represents one character before `bcd`.
The `*` then allows zero or more characters after `bcd`.


## 7. The `[ ]` Wildcard

Square brackets can be used to match one character from a specified set.

For example:

```bash
ls -l *[cd]*
```

This matches filenames containing either `c` or `d`.

It does not specifically mean that the filename must contain the sequence `cd`.

For example, a filename containing `c` would match, as would one containing `d`.

A range can also be specified:
`[1-9]`

This matches one character from `1` through `9`.


## 8. Combining Wildcards with more
The output of a command can be passed to another command using a pipe (`|`).

For example:

```bash
ls -l *[cd]* | more
```

The `|` sends the output of `ls -l *[cd]*` to more, allowing the results to be viewed one screen at a time.


## 9. Brace Expansion

I also learned that Bash can use brace expansion to generate multiple filenames.

For example:

```bash
touch abcd{1..9}-xyz
```

This creates nine files:

- abcd1-xyz
- abcd2-xyz
- abcd3-xyz
- abcd4-xyz
- abcd5-xyz
- abcd6-xyz
- abcd7-xyz
- abcd8-xyz
- abcd9-xyz

**Note**: `{1..9}` is technically called brace expansion, not a wildcard. It generates multiple arguments before the command is executed.


## 10. Removing Files with `rm`

The `rm` command is used to remove files.

For example:

```bash
rm filename
```

Wildcards can also be used with `rm`.

For example:

```bash
rm abcd*
```

This can remove every matching file whose name begins with `abcd`.
Because `rm` can permanently delete files, wildcard patterns should be used carefully.


## 11. Other Special Characters

The backslash (`\`) can be used as an escape character in the shell. It can prevent a character from being interpreted specially.

For example:

```bash
echo "hello\ world"
```

The exact behavior depends on how the character is used and where it appears.

I also encountered:

- `^`
- `$`

These are commonly used as anchors in regular expressions:

- `^` represents the beginning of a line.
- `$` represents the end of a line.

They are not ordinary shell wildcards like `*`, `?`, and `[ ]`.


## 12. Linux File Types

Linux supports several different types of filesystem objects.

When using:

```bash
ls -l
```

the first character of each entry indicates its type.

### Regular File

A regular file has `-` as its first character.

Examples include:
- Text files
- Executable files
- Images
- Videos
- Documents

Example:

```bash
-rw-r--r-- 1 user user 1234 file.txt
```

The first character is:
`-`

### Directory

A directory starts with:

`d`

For example:

```bash
drwxr-xr-x
```

Directories are used to organize files and other directories.


### Symbolic Link

A symbolic link starts with:

`l`

For example:

```bash
lrwxrwxrwx
```

A symbolic link is similar to a shortcut in Windows because it points to another file or directory.


### Character Device

A character device file starts with:
`c`
Character devices provide access to devices that handle data as a stream of characters.

### Block Device
A block device file starts with:
`b`
Examples include storage devices such as hard drives and USB storage devices.

### Socket
A socket file starts with:
`s`
Sockets are used for communication between processes.

### Named Pipe
A named pipe, also called a FIFO (First In, First Out), starts with:
`p`
Named pipes can be used for communication between processes.


## 13. Inodes

An inode is a data structure used by Linux filesystems to store information about a filesystem object.

An inode can contain information such as:
- File type
- File permissions
- Owner
- Group
- File size
- Timestamps
- References to the data blocks containing the file's contents

Each file has an inode number within its filesystem.

The inode is important when understanding how Linux handles links.


## 14. Hard Links and Soft Links

Linux allows multiple names to refer to filesystem objects.

There are two important types of links:
- Hard links
- Soft (symbolic) links

Links are somewhat similar to shortcuts in Windows, although hard links work differently from Windows shortcuts.

## 15. Hard Links

A hard link is another directory entry that refers to the same underlying inode as the original file.

The command for creating a hard link is:

```bash
ln original_file hard_link
```

Because both names refer to the same inode, a hard link continues to work even if the original filename is removed.

For example:

```bash
echo "animes are amazing!" > anime
```

Then:

```bash
ln anime anime-hard
```

Both `anime` and `anime-hard` refer to the same underlying file data.


## 16. Soft Links

A soft link, also called a symbolic link, contains a reference to another path.

The command for creating a symbolic link is:

```bash
ln -s original_file soft_link
```

For example:

```bash
ln -s anime anime-soft
```

A symbolic link can point to a file or directory.

If the target of a symbolic link is removed or renamed, the symbolic link can become a broken link because its target path no longer exists.


## 17. Hard Links vs. Soft Links

| Feature | Hard Link | Soft Link |
| --- | --- | --- |
| Command| ln | ln -s |
| Refers to | Same inode | Target path |
| Can become broken if target is renamed/deleted? | No, if another hard link remains | Yes |
| Can normally cross filesystems? | No | Yes |
| Can point to a directory? | Generally no | Yes |
| Similar to a Windows shortcut? | Not exactly | More similar |

Hard links and symbolic links cannot normally be created with the same name in the same directory because each directory entry must have a unique name.


## 18. Writing to and Reading Files

I also learned how to write text into a file using the `>` redirection operator.

For example:

```bash
echo "animes are amazing!" > anime
```

This creates the file anime if it doesn't already exist and writes the text into it.

If the file already exists, `>` overwrites its existing contents.

The `cat` command can then be used to display the contents:

```bash
cat anime
```

The output will be:

```bash
animes are amazing!
```

**Important**: If I want to add text to an existing file without overwriting its contents, I can use `>>` instead of `>`.

For example:

```bash
echo "another line" >> anime
```

## Key Commands Learned

| Command | Purpose |
| --- | --- |
| `su - root` | Switch to the root user |
| `exit` | Leave the current shell/session |
| `find` | Search the filesystem |
| `locate` | Search the file-location database |
| `updatedb` | Update the database used by `locate` |
| `rm` | Remove files |
| `ls` | List files and directories |
| `more` | View output one screen at a time |
| `ln` | Create a hard link |
| `ln -s` | Create a symbolic link |
| `echo` | Display or write text |
| `cat` | Display file contents |


## Practical Examples

Create multiple files

```bash
touch abcd{1..9}-xyz
```

List files beginning with `abc`

```bash
ls -l abc*
```

List files ending with `xyz`

```bash
ls -l *xyz
```

Find filenames containing `xy`

```bash
ls -l *xy*
```

Find filenames containing either `c` or `d`

```bash
ls -l *[cd]*
```

Remove files beginning with `abcd`

```bash
rm abcd*
```

Create a file and write text to it

```bash
echo "animes are amazing!" > anime
```

Display the contents

```bash
cat anime
``

Create a hard link

```bash
ln anime anime-hard
```

Create a symbolic link

```bash
ln -s anime anime-soft
```


