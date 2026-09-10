# Linux File Permissions — Numeric Mode

This directory contains my notes and practical examples on assigning Linux file and directory permissions using **numeric mode** with `chmod`.

## Topics Covered

- Numeric permission mode
- `chmod` using numeric values
- Understanding permission values from `0` to `7`
- Converting numeric permissions to symbolic permissions
- Understanding `chmod 764`


## 1. Permission Using Numeric Mode

Linux file and directory permissions can be assigned using either **symbolic mode** or **numeric mode**.

For example, read permission for the user, group, and others can be assigned using symbolic notation:

```bash
chmod ugo+r FILE
```

The same permission can be represented using numeric notation:

```bash
chmod 444 FILE
```

Both commands result in:

```text
-r--r--r--
```

The three numeric digits correspond to:

```text
| User | Group | Others |
| --- | --- | --- |
| 4 | 4 | 4 | 
```

Therefore:

```text
444 = r-- r-- r--
```


## 2. Numeric Permission Values

Linux represents the three basic permissions using numerical values:

| Number | Permissions | Meaning                |
| -----: | :---------: | ---------------------- |
|    `0` |    `---`    | No permissions         |
|    `1` |    `--x`    | Execute                |
|    `2` |    `-w-`    | Write                  |
|    `3` |    `-wx`    | Write + Execute        |
|    `4` |    `r--`    | Read                   |
|    `5` |    `r-x`    | Read + Execute         |
|    `6` |    `rw-`    | Read + Write           |
|    `7` |    `rwx`    | Read + Write + Execute |

These values are based on the following permission numbers:

```text
Read    = 4
Write   = 2
Execute = 1
```

The values can be combined to produce different permission sets.

For example:

```text
4 + 2 + 1 = 7
```

Therefore:

```text
7 = rwx
```

Similarly:

```text
4 + 2 = 6
```

Therefore:

```text
6 = rw-
```

And:

```text
4 = r--
```


## 3. Understanding `chmod 764`

Consider the command:

```bash
chmod 764 FILE
```

The three digits represent permissions for:

```text
| User | Group | Others |
| --- | --- | --- |
| 7 | 6 | 4 |
```

### `7` — User

```text
7 = rwx
```

The user/owner has:

- Read
- Write
- Execute

### `6` — Group

```text
6 = rw-
```

The group has:

- Read
- Write
- No execute permission

### `4` — Others

```text
4 = r--
```

Other users have:

- Read
- No write
- No execute

Therefore:

```text
764 = rwx rw- r--
```

The complete permission representation is:

```text
-rwxrw-r--
```


## 4. Numeric Permission Structure

A numeric permission is normally written using three digits:

```text
   | 7 | 6 | 4 |
   | --- | --- | --- |
   | ↓ | ↓ | ↓ |
   | User | Group | Others |
```

Each digit independently defines the permissions for that user class.

For example:

```text
chmod 764 FILE
```

means:

```text
User   → 7 → rwx
Group  → 6 → rw-
Others → 4 → r--
```


## Quick Reference

```text
0 = ---
1 = --x
2 = -w-
3 = -wx
4 = r--
5 = r-x
6 = rw-
7 = rwx
```

### Example

```bash
chmod 764 FILE
```

Results in:

```text
-rwxrw-r--
```

Where:

```text
User   = rwx
Group  = rw-
Others = r--
```


## Key Takeaway

Numeric permissions provide a compact way to assign Linux file and directory permissions.

The three digits always represent:

```text
User → Group → Others
```

and each digit is a combination of:

```text
Read    = 4
Write   = 2
Execute = 1
```
