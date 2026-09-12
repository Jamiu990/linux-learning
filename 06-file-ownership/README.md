# File Ownership

This directory contains my notes and practical examples from Day 6 of my Linux learning journey.

## Topics Covered

- Linux file ownership
- User ownership
- Group ownership
- `chown`
- `chgrp`
- Recursive ownership changes
- Viewing ownership with `ls -l`
- Ownership and file deletion
- Directory permissions and file creation
- Root-owned directories
- The `/etc` directory


## 1. File Ownership

Linux associates files and directories with **two ownership identities**:

* **User (owner)**
* **Group**

The **user owner** is typically the user who created the file or directory.

The **group owner** is the group associated with the file or directory.

For example, when running:

```bash
ls -l
```

you may see output similar to:

```text
-rw-r--r-- 1 jamiu jamiu 1234 anime
```

The ownership information is shown after the number of links:

```text
-rw-r--r-- 1 jamiu jamiu 1234 anime
             │     │
             │     └── Group owner
             └──────── User owner
```


## 2. The `chown` Command

`chown` is used to change the **user ownership** of a file or directory.

The general syntax is:

```bash
chown USER FILE
```

For example:

```bash
chown root anime
```

This changes the user owner of the file `anime` to `root`.

In this command:

```text
chown → command
root  → new owner
anime → file
```


## 3. Changing File Ownership as Root

Changing ownership generally requires appropriate privileges.

To switch to the root user:

```bash
su -
```

After entering the root password, navigate to the directory containing the file.

For example:

```bash
cd /home/username
```

Then change the ownership:

```bash
chown root anime
```

To verify the change:

```bash
ls -l anime
```

The **user-owner column** should now show:

```text
root
```

When finished with the root shell:

```bash
exit
```


## 4. The `chgrp` Command

`chgrp` is used to change the **group ownership** of a file or directory.

The general syntax is:

```bash
chgrp GROUP FILE
```

For example:

```bash
chgrp root anime
```

This changes the group owner of `anime` to `root`.

To verify:

```bash
ls -l anime
```

The **group-owner column** should now show:

```text
root
```

Then leave the root shell:

```bash
exit
```


## 5. `chown` vs. `chgrp`

| Command | Purpose                 |
| ------- | ----------------------- |
| `chown` | Changes user ownership  |
| `chgrp` | Changes group ownership |

For example:

```bash
chown root anime
```

changes the **user owner**.

```bash
chgrp root anime
```

changes the **group owner**.



## 6. Recursive Ownership Changes

The `-R` option can be used with `chown` and `chgrp` to apply ownership changes **recursively**.

For example:

```bash
chown -R root directory
```

This changes the ownership of the specified directory and the files and subdirectories inside it.

Similarly:

```bash
chgrp -R root directory
```

changes the group ownership recursively.

**Important:** `-R` applies the operation to the specified directory and everything underneath it. It does **not** mean that the parent directory above the specified directory is changed.



## 7. Ownership and Deleting Files

Changing the ownership of a file does not necessarily determine whether another user can delete it.

For example, suppose the file is:

```text
/home/username/anime
```

Even if `anime` is owned by `root`, another user may still be able to delete it if they have the necessary **write and execute permissions on the parent directory** (`/home/username`).

This demonstrates an important Linux concept:

**The ability to delete a file is primarily controlled by the permissions of the directory containing the file, rather than the permissions of the file itself.**

For example:

```text
/home/username/
        │
        └── anime
```

The permissions on `/home/username/` determine whether a user can create, delete, or rename entries inside that directory.



## 8. Creating a File in `/etc`

The `/etc` directory contains system-wide configuration files and is normally owned by `root`.

As a normal user, attempting to create a file directly inside `/etc` will normally result in a permission error.

For example:

```bash
cd /etc
touch testfile
```

This can result in:

```text
Permission denied
```



## 9. Checking `/etc` Permissions

The permissions and ownership of the root filesystem can be viewed with:

```bash
ls -l /
```

This displays information about directories such as:

```text
/etc
```

The `/etc` directory is normally owned by:

```text
root root
```

A typical permission set is:

```text
drwxr-xr-x
```

The permission portion:

```text
rwxr-xr-x
```

means:

```text
User   → rwx
Group  → r-x
Others → r-x
```

The owner (`root`) has write permission, while the group and others do not.

Therefore, a normal user generally cannot create a new file directly inside `/etc`.



## 10. Creating a File as Root

A user with appropriate privileges can switch to root:

```bash
su -
```

Then navigate to `/etc`:

```bash
cd /etc
```

A file can then be created:

```bash
touch testfile
```

Because the file was created by root, it will normally be owned by:

```text
root root
```

Afterward, exit the root shell:

```bash
exit
```



## 11. Attempting to Delete a Root-Owned File

After creating `testfile` as root, a normal user can attempt to remove it:

```bash
rm /etc/testfile
```

The operation can be denied.

The important point is that **the ownership of `testfile` is not the main reason for the denial**.

The parent directory `/etc` controls whether the user can remove directory entries.

Since a normal user does not have write permission on `/etc`, they generally cannot delete files from it.

This reinforces the distinction between:

```text
File permissions
        vs.
Directory permissions
```



## Key Commands Learned

| Command    | Purpose                                                   |
| ---------- | --------------------------------------------------------- |
| `ls -l`    | Displays file details including ownership and permissions |
| `su -`     | Switches to a root login shell                            |
| `chown`    | Changes user ownership                                    |
| `chgrp`    | Changes group ownership                                   |
| `chown -R` | Recursively changes user ownership                        |
| `chgrp -R` | Recursively changes group ownership                       |
| `touch`    | Creates an empty file                                     |
| `rm`       | Removes a file                                            |
| `exit`     | Exits the current shell                                   |



## Key Takeaways

### Ownership

Every file and directory has a:

```text
User owner
Group owner
```

### Changing ownership

```bash
chown root anime
```

changes the user owner.

```bash
chgrp root anime
```

changes the group owner.

### Recursive changes

```bash
chown -R root directory
```

applies the ownership change to the directory and everything inside it.

### Directory permissions matter

A user's ability to create, delete, or rename files inside a directory depends heavily on the **permissions of the directory itself**.

For example:

```text
/etc
```

is normally writable only by privileged users, which prevents ordinary users from creating or deleting entries there.
