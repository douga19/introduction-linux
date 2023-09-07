---
title: Lab 2 - File system and permissions
---

# Lab 2 - File system and permissions

!!! info "Instructions"

    - We recall that in all exercises the `$` at the beginning of the command represents the prompt, it is not to be entered when you write a command line.
    - For each new command, do not hesitate to consult its manual page with the `man` command, or to use the `--help` option (if it is available) to know what it does.


## File system

!!! tip "Linux file system"

    Linux file system is a *tree* or *hierarchy* of files and directories. The root directory is `/` and all other directories are subdirectories of it. Directories are separated by `/` and files are file names.

    When you open a shell (i.e. open a terminal), it is *in* a directory. This directory is called your *current directory* or *working directory*.
    
    A basic Linux system has tens of thousands of system directories and files. Most of these directories and files are hidden and are not visible by default. These hidden files and directories are used by the operating system to store configuration information and other system information.

    Root subdirectories are typically reserved for system files. The `/home` and `/tmp` directories are used to store temporary files and personal files.

    Unless you are a system administrator, you do not need to worry about most system files and directories. However, it is important to understand how directories and files are organized so that you can navigate the file system and find the files you need.

    The following table describes the contents of the main Linux file system directories.

    | Directory | Description |
    ------------ | -------------
    | `/bin` | Contains the programs essential to the operation of the system. |
    | `/boot` | Contains the files needed to boot the system. |
    | `/dev` | Contains the files representing the devices. |
    | `/etc` | Contains the system configuration files. |
    | `/home` | Contains the personal directories of the users. |
    | `/lib` | Contains shared libraries and kernel modules. |
    | `/media` | Contains the mount points of removable devices. |
    | `/mnt` | Contains the mount points of temporary file systems. |
    | `/opt` | Contains additional software. |
    | `/proc` | Contains information about processes and the system. |
    | `/root` | Administrator's home directory. |
    | `/run` | Contains application runtime files. |
    | `/sbin` | Contains the programs essential to the operation of the system. |
    | `/srv` | Contains the data of the services provided by the system. |
    | `/sys` | Contains information about devices. |
    | `/tmp` | Contains temporary files. |
    | `/usr` | Contains programs, libraries and configuration files. |
    | `/var` | Contains variable files such as logs, mails, databases, etc. |
    | `/lost+found` | Contains files recovered during a system crash. |

---

### Exercise 1 : `id` and `/etc/passwd`

1. Type the following commands in a terminal and note the results:
   ```bash
   $ id
   ```
2. Then type the same command, but this time with the argument `root`, note the results.
   ```bash
   $ id root
   ```
3. Then display the contents of the file `/etc/passwd` with the `cat` command.
4. Search for the lines where your username and the username `root` appear. What are the differences?
5. Can you deduce what the `/etc/passwd` file is used for?

## Normal files permissions

!!! tip "File protection"

    A Linux system allows many users to access files and directories. To protect files and directories, Linux uses a system of permissions. Permissions are access rights to files and directories. Permissions are associated with users and groups. Users are *people* who have an account on the system.

    For normal files, permissions are associated with three categories of users: the owner of the file (usually the one who created the file), the owner group of the file and other users.

    The permission categories for a file are as follows:

      - **read** `r`: allows you to read the contents of the file.
      - **write** `w`: allows you to modify the contents of the file.
      - **execute** `x`: allows you to execute the file (if it is a program or a script).

    The `-l` option of the `ls` command displays the meta-data associated with a file, its name, its size, its owner, its group, ... and in particular its permissions, for example:

    ```bash
    $ ls -l fichier
    -rw-r--r-- 1 user group 0 2019-09-09 10:00 fichier
    ```
    The string `-rw-r--r--` represents the permissions associated with the file. The first character designates the type of file, the next three represent the permissions of the owner, the next three represent the permissions of the owner group and the last three represent the permissions of other users. Permissions are represented by the characters `r`, `w` and `x` for read, write and execute permissions respectively. If the permission is not granted, the character `-` is used instead.

    Permissions can be represented by **numbers (octal representation)** or **letters (symbolic representation)**.

    The following table gives the correspondence between the two representations:

    | Numbers | Letters | Description |
    | ------- | ------- | ----------- |
    | 0 | `---` | No permission |
    | 1 | `--x` | Execute |
    | 2 | `-w-` | Write |
    | 3 | `-wx` | Write and execute |
    | 4 | `r--` | Read |
    | 5 | `r-x` | Read and execute |
    | 6 | `rw-` | Read and write |
    | 7 | `rwx` | Read, write and execute |

    In our example, the permissions `-rw-r--r--` can be represented in the following ways:

    | | User | Group | Other |
    |-|----------- | ------ | ------ |
    | symbolic | `rw-` | `r--` | `r--` |
    | binary | 110 | 100 | 100 |
    | octal | 6 | 4 | 4 |
---

### Exercise 2 : File permissions

1. Create an empty directory and an empty file (these two must be at the same level). Use the `ls` command and the `-l` and `-d` options on each of these two new files to determine the permissions you (respectively your group and others) have on these files. How do you recognize a directory?
2. The following lines give the answer of the `ls -ld` command on a certain directory (for the needs of the Exercise we have reported only the first and the last field of the result of `ls -ld`).
    ```bash
    drwxr-xr-x a
    dr-xr--r-- b
    -rw-r--r-- c.txt
    --w--w-r-- d.c
    -rwxr-xr-x op
    ```
    Among these files, which are the directories?
3. For each of the files above, give the permissions associated with each of the users (owner, owner group and other users) using the symbolic representation and the octal representation.
4. Give the symbolic representation and the octal representation of the permissions associated with the file `/etc/passwd`, the command `ls` and your home directory.

### Exercise 3 : Modify permissions `chmod`

1. Test the following commands in a terminal and try to understand how the `chmod` command works (with the symbolic representation).
    ```bash
    $ touch f; ls -l f
    $ chmod a= f; ls -l f
    $ chmod o+rw f; ls -l f
    $ chmod u=o f; ls -l f
    $ chmod o-wx f; ls -l f
    $ chmod g+u f; ls -l f
    $ chmod a+x,g-w f; ls -l f
    ```
2. Test the command `chmod 644 f; ls -l f`. What does this command do?
3. With the two modes of use of `chmod` (octal and symbolic), modify the permissions of the file `f` as follows:
    - execution for all, read and write only for the owner.
    - read and execute for all, no one can write.
    - all permissions for all, no writing for others.
    - read and write for the owner, execution for the group and none for others.
  
## Directories permissions

!!! tip "What is a directory ?"

    A directory is a table of file names associated with an index number called *inode number* which allows to know the information (contained in the inode) concerning this file (size, permissions, timestamp, where to find the content of the file, ...).

    In a directory, permissions are not associated with files but with the directory itself. The permissions associated with a directory are:

      - **read** `r`: allows you to list the contents of the directory.
      - **write** `w`: allows you to modify the contents of the directory (create or delete files).
      - **execute** `x`: allows you to open the directory (with the `cd` command for example).
---

### Exercise 4 : Directories permissions

1. Create a directory `rep` and two normal files `a` and `b` inside this directory.
2. Remove all permissions on the directory `rep` and try the following commands:
    ```bash
    $ cd rep
    $ ls rep
    $ cat rep/a
    $ touch rep/c
    $ rm rep/a
    ```
3. Give only the *read* permission on the directory `rep` and try all the commands of question 2. Note the differences.
4. Same question but with only the *write* permission on `rep`. Note the differences.
5. This time with only the *execute* permission on `rep`. Test the following commands:
    ```bash
    $ cd rep
    $ ls rep
    $ echo "toto" >> rep/a
    $ cat rep/c
    $ ls -l rep/a
    $ touch rep/c
    $ rm rep/a
    ```
6. With the set of permissions `-wx` on `rep` for all users, try to:
   - create a file d in `rep`
   - rename the file b
   - remove all permissions associated with the file d
   - delete the file d

## Default permissions

!!! tip "What us `umask` ?"

    `umask` is a built-in command that allows you to define the default permissions of files and directories that you create. The value of the umask is an octal value that is *subtracted* from the default permissions. For example, if the umask is 022, the default permissions are 755 for directories and 644 for files.

---

### Exercise 5 : `umask` (optional)

1. In a terminal, type the command `umask` and note the result.
2. Create a directory `rep` and a file `f` at the same level as `rep`. Display the permissions associated with `rep` and `f` with the command `ls -ld rep f`. Convert these permissions to octal representation and note them. Finally, delete `rep` and `f`.
3. Change the value of the mask with the command
    ```bash
    $ umask 240
    ```
4. Change the value of the mask with the command
    ```bash
    $ umask 121
    ```
    then redo question 2.
5. Change the value of the mask with the command
    ```bash
    $ umask 666
    ```
    then redo question 2.
6. From all the previous questions, can you deduce how the value of the umask affects the permissions associated with the directories and files you create?
7. Give back the umask its initial value.