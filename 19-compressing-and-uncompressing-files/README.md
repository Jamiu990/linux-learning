# Day 19 — Compressing and Uncompressing Files in Linux

Linux provides commands for combining multiple files into one archive and reducing their storage size through compression.

The main commands covered in this lesson are:

- `tar` — Combines files and directories into a single archive.
- `gzip` — Compresses files to reduce their size.
- `gunzip` — Decompresses `.gz` files.
- `gzip -d` — Another way to decompress `.gz` files.

## 1. `tar` — Creating an Archive

The `tar` command combines multiple files and directories into one archive file.

**Important:** Creating a `.tar` archive does not compress the files or reduce their size. It simply groups them together.

### Creating a TAR archive

**Syntax:**

```bash
tar -cvf archiveName.tar file1 file2 directory
```

**Example:**

```bash
tar -cvf backup.tar Documents/
```

Creates an archive named `backup.tar` containing everything inside the `Documents` directory.

**Understanding the options:**

| Option | Meaning |
|---|---|
| `-c` | Creates a new archive. |
| `-v` | Displays the files being added. |
| `-f` | Specifies the archive filename. |

### Extracting a TAR archive

**Syntax:**

```bash
tar -xvf archiveName.tar
```

**Example:**

```bash
mkdir newContainer
tar -xvf backup.tar -C newContainer/
```

- `mkdir newContainer` creates a new directory.
- `-x` extracts the archive.
- `-C` specifies the directory where the contents should be extracted.

The files from `backup.tar` will be extracted into `newContainer`.

## 2. `gzip` — Compressing Files

The `gzip` command compresses files to reduce their size.

It is commonly used to compress TAR archives.

**Example:**

```bash
gzip backup.tar
```

Compresses `backup.tar` and creates:

```text
backup.tar.gz
```

**Note:** By default, `gzip` replaces the original `.tar` file with the compressed `.tar.gz` file.

## 3. `gunzip` and `gzip -d` — Decompressing Files

These commands decompress files that have been compressed using `gzip`.

Both commands perform the same basic operation.

**Using `gunzip`:**

```bash
gunzip backup.tar.gz
```

Decompresses the file and restores:

```text
backup.tar
```

**Using `gzip -d`:**

```bash
gzip -d backup.tar.gz
```

Also decompresses the file and restores `backup.tar`.

## 4. Combining `tar` and `gzip`

You can archive and compress files in one command instead of running `tar` and `gzip` separately.

**Example:**

```bash
tar -czvf backup.tar.gz Documents/
```

This command:
1. Creates a TAR archive.
2. Compresses the archive using gzip.
3. Produces `backup.tar.gz`.

**Understanding the options:**

| Option | Meaning |
|---|---|
| `-c` | Creates an archive. |
| `-z` | Compresses the archive using gzip. |
| `-v` | Displays the files being processed. |
| `-f` | Specifies the archive filename. |

### Extracting a compressed TAR archive

```bash
tar -xzvf backup.tar.gz
```

Extracts and decompresses the archive.

To extract it into a particular directory:

```bash
mkdir restoredFiles
tar -xzvf backup.tar.gz -C restoredFiles/
```

Here, `-x` extracts the archive, while `-z` handles gzip decompression.

## Summary

| Command | Purpose |
|---|---|
| `tar -cvf` | Creates a TAR archive. |
| `tar -xvf` | Extracts a TAR archive. |
| `gzip` | Compresses a file. |
| `gunzip` | Decompresses a `.gz` file. |
| `gzip -d` | Decompresses a `.gz` file. |
| `tar -czvf` | Creates and compresses a TAR archive. |
| `tar -xzvf` | Extracts and decompresses a TAR archive. |

## Key Takeaway

Remember the difference:

- **Archiving (`tar`):** Combines multiple files and directories into one file.
- **Compression (`gzip`):** Reduces the size of a file.
- **Decompression (`gunzip` or `gzip -d`):** Restores a compressed file.
- **Extraction (`tar -x`):** Retrieves the contents of an archive.

The `.tar.gz` extension indicates a TAR archive that has also been compressed using gzip.