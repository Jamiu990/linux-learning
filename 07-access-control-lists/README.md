# Linux Access Control Lists (ACL)

This directory contains my notes and practical examples on **Access Control Lists (ACLs)** from Day 7 of my Linux learning journey.

## Topics Covered

- Access Control Lists (ACL)
- Why ACLs are useful
- Assigning permissions to specific users
- Assigning permissions to groups
- Inheriting ACL entries
- Removing specific ACL entries
- Removing all ACL entries
- Viewing ACL permissions
- ACL indicators in file permissions
- ACL write permissions and file deletion


## 1. What Is an Access Control List (ACL)?

An **Access Control List (ACL)** provides an additional and more flexible mechanism for controlling access to files and directories.

Traditional Linux permissions normally assign access to three categories:

```text
User → Group → Others
````

ACLs provide more granular control by allowing permissions to be assigned to **specific users or groups**.

For example, suppose a user needs access to a particular file but is not a member of the group that owns the file.

Instead of changing the user's group membership, an ACL can be used to grant that specific user the required permissions.


## 2. ACL Commands

Two important commands are used when working with ACLs:

| Command   | Purpose                                |
| --------- | -------------------------------------- |
| `setfacl` | Sets, modifies, or removes ACL entries |
| `getfacl` | Displays ACL information               |


## 3. Assigning ACL Permissions to a User

The following command adds an ACL entry for a specific user:

```bash
setfacl -m u:user:rwx /path/to/file
```

Where:

```text
-m      → modify an ACL
u:user  → the specified user
rwx     → read, write, and execute permissions
```

For example:

```bash
setfacl -m u:jamiu:rwx /home/user/file
```

This gives the specified user `rwx` permissions on the file.


## 4. Assigning ACL Permissions to a Group

ACL permissions can also be assigned to a specific group:

```bash
setfacl -m g:group:rw /path/to/file
```

Where:

```text
g:group → the specified group
rw      → read and write permissions
```

For example:

```bash
setfacl -m g:developers:rw /home/user/file
```

This gives the `developers` group read and write permissions on the specified file.


## 5. Applying ACLs Recursively

The `-R` option applies the operation recursively to files and directories under the specified directory.

For example:

```bash
setfacl -Rm "entry" /path/to/dir
```

The operation is applied throughout the directory tree.

**Note:** Recursive modification and ACL inheritance are related but not identical concepts. `-R` applies the command to existing files and directories recursively. Default ACLs are used when you specifically want newly created items within a directory to inherit ACL entries.


## 6. Removing a Specific ACL Entry

A specific ACL entry can be removed using the `-x` option.

For example, to remove a specific user's ACL entry:

```bash
setfacl -x u:user /path/to/file
```

Here:

```text
-x      → remove an ACL entry
u:user  → the user's ACL entry to remove
```

This removes the specified user's additional ACL entry without removing the other ACL entries.


## 7. Removing All Extended ACL Entries

The `-b` option removes all extended ACL entries:

```bash
setfacl -b /path/to/file
```

This removes the file's extended ACL entries and returns it to the standard Linux permission model.


## 8. Viewing ACL Permissions

The `getfacl` command displays the ACL information associated with a file or directory.

For example:

```bash
getfacl /path/to/file
```

This can be used to inspect the users, groups, and permissions associated with the ACL.


## 9. The `+` Symbol in `ls -l`

When a file or directory has an extended ACL, `ls -l` can display a `+` symbol at the end of the traditional permission string.

For example:

```text
-rwxr-xr--+
```

The `+` indicates that additional access-control information exists beyond the standard owner, group, and others permissions.

The ACL details can then be examined with:

```bash
getfacl filename
```


## 10. ACL Write Permission and File Deletion

An important behavior to understand is that giving a user **write permission on a file through an ACL does not automatically give that user permission to delete the file**.

For example:

```bash
setfacl -m u:user:rw /path/to/file
```

allows the specified user to read and modify the file, but deletion is controlled primarily by the permissions of the **parent directory**.

Therefore, whether a user can delete a file depends on the user's permissions on the directory containing that file.

This is an important distinction between:

```text
Permissions on the file
```

and:

```text
Permissions on the parent directory
```


## Key Commands

| Command       | Purpose                               |
| ------------- | ------------------------------------- |
| `setfacl -m`  | Add or modify an ACL entry            |
| `setfacl -Rm` | Recursively add or modify ACL entries |
| `setfacl -x`  | Remove a specific ACL entry           |
| `setfacl -b`  | Remove all extended ACL entries       |
| `getfacl`     | Display ACL information               |



## Quick Reference

### Give a user `rwx` permissions

```bash
setfacl -m u:user:rwx /path/to/file
```

### Give a group `rw` permissions

```bash
setfacl -m g:group:rw /path/to/file
```

### Modify ACLs recursively

```bash
setfacl -Rm "entry" /path/to/dir
```

### Remove a user's ACL entry

```bash
setfacl -x u:user /path/to/file
```

### Remove all extended ACL entries

```bash
setfacl -b /path/to/file
```

### View ACL information

```bash
getfacl /path/to/file
```


## Key Takeaway

Traditional Linux permissions provide access control through:

```text
User → Group → Others
```

ACLs provide a more granular mechanism by allowing additional permissions to be assigned to specific users and groups without necessarily changing their group membership.

The two main commands are:

```text
setfacl → configure ACLs
getfacl → view ACLs
```

ACLs therefore extend the standard Linux permission system when more specific access control is required.