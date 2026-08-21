\# Linux Access and Filesystem



This directory contains my notes and practical exercises from my Linux learning journey.



\## Topics Covered



\- Accessing a Linux system

\- SSH

\- Linux users

\- The root user

\- Changing passwords

\- Linux filesystem

\- Filesystem structure

\- Filesystem types

\- Directory properties

\- Absolute and relative paths

\- Basic filesystem navigation

## 1. Accessing a Linux System



I learned how to access a Linux machine remotely using SSH.



From Windows Command Prompt, I can connect to a Linux machine using (I already had SSH configured on my laptop, so I did not need to install PuTTY):



```bash

ssh -l username ip\_address
```

## 2. The Root User



The root user is the superuser in Linux.



The root account has extensive privileges over the system.


## 3. Changing a Password



The `passwd` command can be used to change a user's password.



```bash

passwd
```

## 4. Linux Filesystem



I learned about the structure of the Linux filesystem and how files and directories are organized.



Some important directories include:



\- `/`

\- `/home`

\- `/etc`

\- `/var`

\- `/tmp`

\- `/usr`


## 5. Basic Navigation Commands



\### `pwd`



Displays the current working directory.



```bash

pwd
```


### `ls`


Lists files and directories.


```bash
ls

```



\### `cd`



```bash

cd /home

```



\## 6. Absolute and Relative Paths



An absolute path starts from the root directory.



Example:



```bash

/home/user/Documents

```



A relative path is based on the current working directory.



Example:



```bash

Documents

```



