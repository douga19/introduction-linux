---
title: Lab 5 - Processes, and other commands
---

# Lab 5 - Processes, and other commands

!!! info "Instructions"

    - We recall that in all exercises the `$` at the beginning of the command represents the prompt, it is not to be entered when you write a command line.
    - For each new command, do not hesitate to consult its manual page with the `man` command, or to use the `--help` option (if it is available) to know what it does.
    - Do not hesitate to review the previous Lab if needed.
    - Exercises 1, 2, 3 and 4 are **mandatory**. The rest is optional, but to be finished if you have time.


!!! warning "Last lab session"

    Since it is the last session of the module, take the time to answer the course evaluation questionnaire :) Do not hesitate to tell us what you found good and not that good. Your answers are anonymous and will allow us to improve the course for the next years. Thank you in advance !

## Processes and tasks (or jobs)

!!! tip "Processes and tasks (or jobs)"

    A *processs* is a unit of work on an operating system. It can be a program, a script, or a service. Each program you run represents one or more processes. Each process is identified by a unique number called *PID* (Process IDentifier).
    
    Linux offers us several commands to view the running processes.

    - `ps` allows to display the running processes. By default, `ps` only displays the processes launched by the current user. To display all processes, use the `-e` (or `-A`) option.
    - `top` allows to display the running processes. It can be used interactively, in particular to sort them by CPU usage. You can exit `top` with the `q` key.

    A *task* on the other hand is a unit of work of the shell. A task can be a process, or a group of processes but it must have been launched by the shell. The shell has a task control system: it is the ability to execute several commands at the same time. You can run a command in the background and in the foreground.

    The `jobs` command displays the tasks currently running.


    !!! warning "What is the difference between a process and a task?"
        A task is a processes but a process is not necessarily a task.

---

### Exercise 1 - Processes visualization
1. Try out the following commands and observe their results. Use `man ps` to understand the options used.
    ```bash
    $ ps
    $ ps -f
    $ ps -u
    $ ps -T
    $ ps -e
    $ ps -U root
    ```

2. The `ps` command returns the list of running processes. This list contains four columns by default.
    
    !!! info "Information from the `ps` command"
        - The first column corresponds to the *PID* (Process IDentifier) of the process.
        - The second column corresponds to the *TTY* (TeleTYpewriter) on which the process is launched. This is the type of terminal used to launch the process. Here `pts/0` (pseudo-terminal slave) means that the process was launched in a pseudo-terminal. The number indicated corresponds to the number of the terminal (for example if you have several instances of the terminal open).
        - The third column corresponds to the *TIME* (time) of execution of the process.
        - The fourth column corresponds to the *CMD* (CoMmanD) that launched the process.
 
3. The standard output of the `ps` command can be redirected. Using the `grep` and/or `wc` command:

    - Display the number of processes launched by the current user.
    - Display the number of processes launched by the `root` user.
    - Display the number of processes launched by the current user and whose command is `bash`.

4. (Optional) The `top` command displays the running processes. Once launched, it runs continuously and displays the processes in real time. The `h` key displays the help and allows you to view the available features, the `q` key allows you to exit `top`. Test the `top` command, display the help then:
    - Filter the running processes to display only those launched by the current user.
    - Filter the running processes to display only those launched by the `root` user.
    - Filter the running processes to display only those whose command is `bash`.


### Exercise 2 - Processes and tasks
1. In this exercise we will simulate the execution of a long process. For this, we will use the `sleep` command which allows to pause the execution of a script for a certain time. Type the command `sleep 10` and observe what happens.
2. Then test the following commands and comment on the results:
    ```bash
    $ ps
    $ sleep 240
    $ C-z # Control + z
    $ ps
    $ fg %1 # fg %<task number>
    $ C-c # Control + c
    $ ps
    ``` 
      
      - In your opinion what does the keyboard shortcut `C-z` do? and the keyboard shortcut `C-c`?
      - Redo the commands by typing commands (or anything else in the terminal) between the `sleep 240` and the `C-z`. What do you notice?
      - Without going through `help fg`, can you guess what the command `fg %1` does? and the command `fg` in general?
      - Redo the commands by noting each time the PID of the `sleep 240` process in the outputs of `ps`. What do you notice?

3. Create a file `gros_processus` whose content is the following:
    ```bash
    #!/bin/bash
    sleep 120
    echo 'Done'
    ```
4. Modify the permissions of the file `gros_processus` in order to have `x` permission. Then run the following commands and carefully observe the results:
    ```bash
    $ ./gros_processus 1
    $ C-z
    $ ./gros_processus 2 &
    $ jobs
    $ jobs -p
    $ ps
    $ fg %1
    $ C-z
    $ bg %1
    $ jobs
    $ fg %2
    $ C-z
    $ bg %2 # then wait for the processes to finish
    $ jobs
    ```
    - Which processes allow to place a process in the background? and in the foreground?
    - What difference do you notice between `./gro_processus 1` then `C-z` and directly `./gros_processus 2 &`? (Apart from 1 and 2 of course)?
    - What is the purpose of the `-p` option of the `jobs` command?
    - Without going through `help bg`, can you guess what the commands `bg %1` and `bg %2` do? and the `bg` command in general?
    - What are the different states of the tasks you have observed?

---
## Message in the bottle
!!! tip "Communicate with processes"

    When processes have been launched, we have noticed that they can be stopped, restarted and killed. For this, we used the `C-z`, `C-c`, `fg` and `bg` commands. These commands allow to communicate with the running processes. Actually, the latter send what we call *signals* to the processes. A *signal* is a message sent to a process asking it to do something.
    
    The command that allows to send signals to a process is `kill`. This command requires the PID of the process to whom to send the signal (or its task number if it is one). Thus `C-z`, `C-c`, `fg` and `bg` therefore call the `kill` command to send signals to the processes.

    There are several signals, the most common are:

    - `SIGINT` : signal sent by the `C-c` key combination. It asks the process to stop.
    - `SIGTSTP` : signal sent by the `C-z` key combination. It asks the process to pause.
    - `SIGCONT` : signal sent by the `bg` and `fg` commands. It asks the process to resume its execution.
    - `SIGTERM` : signal sent by the `kill` command by default. It asks the process to stop.
    - `SIGKILL` : It asks the process to stop immediately and causes it to crash, understand by that that the process does not have time to finish properly. It is therefore not recommended to use this signal.

    The exhaustive list of signals is available with the `kill -L` command.

    !!! warning "Who is allowed to send signals to a process?"
        To be able to affect a process, you must of course be its owner or be *root*.

### Exercise 3 - `kill` command (order 66)

1. Type the command `kill -L` and note the numbers associated with the signals `SIGINT`, `SIGTSTP`, `SIGCONT`, `SIGTERM` and `SIGKILL`.
2. Then take the `gros_processus` script from the previous exercise and test the following commands. And comment on the results.
```bash
$ ./gros_processus 1 & # this will be our process 1
$ ./gros_processus 2 & # this will be our process 2
$ ./gros_processus 3 & # this will be our process 3
$ jobs -p # note the PID of the processes, but they must have been displayed on the screen when they were launched
$ kill -SIGTSTP <PID of process 1>
$ jobs
$ kill -SIGINT %2
$ jobs
$ jobs # yes a second time
$ kill -SIGCONT %1
$ jobs
$ kill -s SIGTERM <PID process 1>
$ jobs
$ kill -9 <PID of process 3>
$ jobs
$ jobs # to see the task [3] disappear
```
3. In your opinion what is the difference between `SIGINT` and `SIGTSTP`? and between `SIGTSTP` and `SIGTERM`?
4. According to your observations on the results of question 2, in how many different ways can the `kill` command be used to achieve the same result?
---

## Other (useful) commands

### Exercise 4 - File compression and archiving

!!! tip "Compress and archive files"
    Archiving a set of files consists in grouping them into a single file. This makes it easier to store or transfer them. While compressing a file consists in reducing its size by removing redundant information. This saves storage space and possibly reduces transfer time.

    These two processes often go hand in hand. Indeed, we often compress a file before archiving it. There are several tools for compressing and archiving files.

    - `gzip` (*GNU zip*): allows to compress a file and whose files have the extension `.gz`.
    - `bzip2` (*block-sorting zip*): allows to compress a file and whose files have the extension `.bz2`.
    - `zip`: allows to compress and archive a set of files and whose files have the extension `.zip` (standard format of Windows archives)
    - `tar` (*tape archive*): allows to archive a set of files and whose files have the extension `.tar`.

    We then decompress a file according to its compression and archiving format. 
    
    - `gunzip` : allows to decompress a file compressed with `gzip`.
    - `bunzip2` : allows to decompress a file compressed with `bzip2`.
    - `unzip` : allows to decompress and extract an archive file with `zip`.
  
    !!! warning "Remark"
        `tar` allows both compression and archiving
        
        - The `-c` option of `tar` allows to create an archive.
        - The `-x` option of `tar` allows to extract an archive.
        - The `-f` option of `tar` allows to specify the name of the archive.


1. In a directory `dir` create the following files and directories:
```bash
dir
├── files
│   ├── file-a.md
│   ├── file-b.md
│   ├── file-c.md
│   ├── file-d.md
│   └── file-e.md
└── imgs
    ├── img001.png
    ├── img002.png
    ├── img003.png
    ├── img004.png
    └── img005.png
```
2. Move into the `dir` directory. Then type the following command to create an archive `files.tar` containing the files in the `files` directory:
```bash
$ tar -cvf files.tar files
```
    Then list the files in `dir`.
3. Still in `dir`. Type the following command to create an archive `imgs.tar` containing the images in the `imgs` directory:
```bash
$ tar -cf imgs.tar imgs
```
    Then list the files in `dir`.
4. What can you say about the `-v` option of `tar`?
5. Then move into the parent directory of `dir` and type the following commands:
```bash
$ tar -czvf dir.tar.gz dir
$ ls
$ gunzip dir.tar.gz
$ ls
$ tar -xvf dir.tar
```
    - After the `gunzip` command, what happened to the `dir.tar.gz` file?
    - What do you think the `-z` option of tar is for?
---

### Exercise 5 - A *very* little glance at `vim`

!!! tip "A terminal based text editor"
    `vim` is a terminal based text editor. It allows you to create, edit and view text files. It is very powerful and widely used by developers. It is very complete and has many features. It is therefore quite difficult to master. We will see some basic commands to be able to use it.

    In `vim` there are several *modes* (it is indicated at the bottom left of the window):

    - The *normal* mode: this is the default mode. It allows you to navigate through the file, copy, paste, delete, etc.
    - The *insertion* mode: it allows to insert text in the file.
    - The *command* mode: it allows to enter commands to perform actions on the file.
    - The *visual* mode: it allows to select text in the file.

    In general, to return to the *normal* mode you have to press the `ESC` key.

    - To switch from *normal* mode to *insertion* mode, press the `i` key.
    - To switch from *normal* mode to *command* mode, press the `:` key.

    In *command* mode, we will see together some basic commands:

    - `:q` : quit `vim`.
    - `:w` : save the file.
    - `:wq` : save the file and quit `vim`.
    - `:q!` : quit `vim` without saving the file.

    If you want to learn more, you can take a look [here](https://vim-adventures.com/) and [here](http://www.vimgenius.com/).

1. Type the command `vim hellovim` to create a `hellovim` file with `vim`.
2. Once in the editor, switch to insertion mode by typing the `i` key. Then write the following text:
    ```
    Hello vim !
    ```
3. Return to normal mode by pressing the `ESC` key. Then save the file by typing `:w` and exit `vim` by typing `:q`.
4. Then display the contents of `hellovim` with the `cat` command.

---

### Exercise 6 - Compile and run C programs
!!! Tip "`gcc` compiler"
    `gcc`  is the Linux C compiler. It allows to compile C code. It is widely used by developers. It is very complete and has many features. We will see a preview of its use.

    The compilation of a C program goes through several steps, which are essentially the following:

    - Precompilation: it allows to transform the source code into an intermediate code.
    - Compilation: it allows to transform the intermediate code into machine code.
    - Link editing: it allows to link the machine code with the libraries used.
    - Creating the executable: it allows to create the executable.

1. Create a `hello.c` file with the following content:
    ```c
    #include <stdio.h>

    int main()
    {
        printf("Hello world !\n");
        return 0;
    }
    ```
2. Move into the directory containing your `hello.c` file and type the command `gcc hello.c`. This command will compile your program and create an `a.out` file which is the executable of your program. Finally, type the command `./a.out` to run your program.
    
    !!! warning "Attention"
        - If you already have an `a.out` file in your directory, it will be overwritten by the `gcc hello.c` command.
        - `a.out` is the default name of the executable created by `gcc`. You can change this name by using the `-o` option of `gcc`. For example, `gcc hello.c -o hello` will create an executable `hello` instead of `a.out`.
  
3. Then download this archive [hello.tar.gz](/assets/files/hello.tar.gz).
4. Extract the files from this archive and move into the `hello` directory.
5. Type the command 
```bash
$ gcc main.c hello.c -o run
```
    to compile your program. This command will compile your program and create a `run` file which is the executable of your program. Finally, run your program with the `./run` command.
1. Delete the `run` file and then modify the `hello.c` file so that you have a deliberate error: delete the closing brace of the `void hello()` function. Then run the commands from question 5 again. What do you notice?
2. Then modify the `hello.c` file again by putting back the closing brace but add a `return 1` in the definition of the function (before the closing brace). Then run the commands from question 5 again. What do you notice?
3. Conclude on how `gcc` manages errors and warnings.
 
--- 

### Exercise 7 - `trap` command
!!! tip "Intercept signals"
    The `trap` command allows to intercept the signals sent to a process. It therefore makes it possible to define actions to be carried out when a signal is sent to a process. Its syntax is as follows:
    ```bash
    trap 'command1;command2;...' signal1 signal2 ...
    ```
    Here `command1;command2;...` is the list of *actions* to be performed upon receipt of the signal or signals in the list `signal1 signal2 ...`.

    Upon receipt of a `SIGINT`, for example, we would like to terminate our process cleanly. In this case, we can free all resources before terminating our process. (It's called a *graceful shutdown*).


1. Create a `graceful_shutdown` file with the following content:
```bash
#!/bin/bash

function cmd1()
{
    echo
    echo "Ok, I am stopping..." 
} 

function cmd2()
{
    echo
    echo "...but with grace" 
}

trap 'cmd1;cmd2;exit' SIGINT SIGTERM

while true
do
    echo "Nobody can stop me !"
    sleep 10
done
```
2. Make the `graceful_shutdown` file executable and then run it.
3. Then type the following commands and comment on the results:
```bash
$ ./graceful_shutdown
$ C-c
```
4. In your opinion, what does the `exit` command do?
5. Restart the `graceful_shutdown` script but this time in the background. Then type the following commands and comment on the results:
```bash
$ ./graceful_shutdown &
$ C-c
```
    - What do you notice? As soon as you have the hand on the terminal send a `SIGTERM` to the `graceful_shutdown` process.
    - What conclusion can you draw about `C-c` and background processes?
---