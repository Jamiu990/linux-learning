# File Operations and Searching

This directory contains my notes and exercises on basic Linux file and directory operations.

## Topics Covered

- Creating files
- Creating directories
- Copying files
- Copying directories
- Finding files and directories
- `find`
- `locate`

## 1. Creating Files

The ### `touch` command can be used to create an empty file.

```bash
touch example.txt
```

## 2. Creating Directories

The ### `mkdir` command creates a directory.

```bash
mkdir projects
```

## 3. Copying Files

The ### `cp` command can copy a file.

```bash
cp sourceFile destinationFile
```

## 4. Copying Directories

Directories can be copied recursively using ### `cp -r`.

```bash
cp -r sourceDirectory destinationDirectory
```

## 5. Finding Files

The ### `find` command can search for files and directories based on different criteria.

```bash
find /path -name "filename"
```

## 6. Locate

The ### `locate` command can also be used to search for files.

`find` is more flexible because it can perform searches using different conditions, while `locate` searches its database of file paths.