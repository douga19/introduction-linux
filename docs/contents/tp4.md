---
title: Lab4 - Text filters, redirection and pipes
---

# Lab4 - Text filters, redirection and pipes

!!! info "Instructions"

    - We recall that in all exercises the `$` at the beginning of the command represents the prompt, it is not to be entered when you write a command line.
    - For each new command, do not hesitate to consult its manual page with the `man` command, or to use the `--help` option (if it is available) to know what it does.
    - Do not hesitate to review the previous Lab if needed.

## Standard streams and redirection

!!! tip "Standard output redirection"

    A large number of commands that we have seen so far write their result on the terminal. For example `ls, echo, cat,...`. We say that these commands write on the *standard output* (which is *connected* to the terminal).

    It is possible to *redirect* the standard output to a file using the `>` character. For example:
    ```bash
    $ ls ~ # displays the contents of the home directory on the standard output
    $ ls ~ > list_files.txt # redirects the standard output to the list_files file
    ```

    !!! warning "Warning"
        The redirection of the standard output will create the `list_files.txt` file if it does not exist.

        The redirection overwrites the contents of an existing file. If we want to add the result to the end of the file, we use the `>>` character (we call this the *append* mode).

---
###  Exercise 1 : Standard output redirection (STDOUT)

1. Try the following commands and observe their results:
   ```bash
    $ echo "Am I on the terminal?"
    $ echo "Or in the file?" > file.txt
    $ cat file.txt
    $ echo "And me?" > file.txt
    $ cat file.txt
    $ echo "I don't want to empty the file" >> file.txt
    $ cat file.txt
    $ echo "I want to empty the file" 1> file.txt
    $ cat file.txt
    $ echo "I add myself at the end of the line" 1>> file.txt
   ```
2. Recall the use of `cat` command (man `cat`) and from the results of the previous commands:

    - What is the difference between `>` and `>>` ?
    - What is the difference between `1>` and `>` ?
    - What is the difference between `1>>` and `>>` ?

3. Move into your home directory and type the following command:
    ```bash
    $ ls > list_files.txt; cat list_files.txt
    ```
    - What does this command ?
    - Can you guess why the string `list_files.txt` appears in the content of `list_files.txt`

### Exercise 2 : Count headers (1)

1. Using the standard output redirection, create a file `include_files.txt` that lists all the files in the directory `/usr/include` whose name ends with `.h`.
2. Count the number of `.h` files in the `/usr/include` directory (hint: `wc`).
3. Finally add the sentence `There are <number> .h files in the /usr/include directory` at the end of the `include_files.txt` file.

### Exercise 3 : Standard error redirection (STDERR)

1. In a directory `dir` create a file `file-1.txt` whose content is `Hello world !`.
2. Then create a copy of `file-1.txt` named `file-2.txt`. Remove all read permissions on `file-2.txt`.
3. Then type the following command and note the results (we will have errors!):
    ```bash
    $ cat file-1.txt file-2.txt file-3.txt
    ```
4. Which command succeeded? and which commands failed and why?
5. Then redirect the standard output of the previous command to a file `result.txt`. Observe what is displayed on the terminal, and observe the contents of the file `result.txt`.
6. Then type the following command and note the results:
    ```bash
    $ cat file-1.txt file-2.txt file-3.txt 1> result.txt 2> error.txt
    ```
7. Observe the contents of `result.txt` and `error.txt`. What do they contain? In your opinion what does `1>` and `2>` mean? Draw a conclusion on the difference between standard output and standard error.

---
!!! tip "Standard input redirection"

    Some commands *read* information from the terminal. For example `tr, read,...`. We say that these commands read on the standard input (which is also *connected* to the terminal).

    But many commands also read on the terminal if no file name is given to them as an argument. For example `cat, grep, sort,...`.

    It is possible to redirect the standard input of a command to a file using the `<` character. For example:
    ```bash
    $ cat < file.txt
    ```
    This command displays the contents of the `file.txt` file on the standard output. We say that the `file.txt` file is *connected* to the standard input of the `cat` command.

    !!! warning "Warning"
        The `file.txt` file must exist and we must have the `read` permission otherwise the `cat` command will fail.
---

### Exercise 4 : The return of the `cat`

1. Take a look at the manual of the `cat` command and find out how it works when it is not given a file as an argument.
2. Then test the following command:
   ```bash
   $ cat
   hello<newline>
   world<newline>
   C-d # press the Ctrl key and the d key at the same time
   ```
    How many arguments did the `cat` command receive? What did she display? Why ?
3. Then test the following command:
   ```bash
   $ cat > catout.txt
   hello<newline>
   world<newline>
   C-d # press the Ctrl key and the d key at the same time
   ```
    Then display the contents of the `catout.txt` file. What does it contain ? Why ?
4. Finally type the following command:
    ```bash
    $ cat < catout.txt
    $ cat 0< catout.txt
    ```
    - How many arguments did the `cat` command receive? What did she display?
    - What is the difference between `<` and `0<` ?

### Exercise 5 : Count headers (2)

We are going to redo the same exercise as exercise 2 but this time using the redirection of the standard input.

1. Create a `include_files.txt` file that lists all the files in the `/usr/include` directory whose name ends with `.h`.
2. Then type the following command and comment on its result:
    ```bash
    $ wc -l < include_files.txt
    ```
3. Then enter the following command and comment on its result:
    ```bash
    $ wc -l < include_files.txt >> include_files.txt
    ```
    and observe the last line of the `include_files.txt` file.
4. Finally, we would like the last line of the `include_files.txt` file to be the sentence `There are <number> .h files in the /usr/include directory`. Where `<number>` is the result of `wc -l < include_files.txt`.

    Find a command that allows you to do this using both the standard output and standard input redirection.

    !!! info "Hint"

        - To remove the last line, we can redo the command from the first question.
        - Then think of the `echo` command and the command substitution.

## Pipes

!!! tip "Pipes"
    A *pipe* is a mechanism that allows you to connect the standard output of a command to the standard input of another command. We use the `|` character to create a pipe.

    That is to say for
    ```bash
    $ cmd1 | cmd2
    ```
    The standard output of `cmd1` is connected to the standard input of `cmd2`.
---

### Exercise 6 : Count headers (I promise it's the last one)

1. Test the following command and comment on its result:
    ```bash
    $ ls /usr/include/*.h | wc -l
    ```
    Where is the result of the `ls` command redirected? Where is the standard input of the `wc` command redirected? Where is the result of `wc` displayed?
2. Then display the sentence `There are <number> .h files in the /usr/include directory` on the terminal using the `echo` command and command substitution (hint the command to use and that of question 1).
3. Finally, enter the following command and comment on its result:
    ```bash
    wc -l $(ls /usr/include/*.h)
    ```
4. In your opinion why is the result of the last command different from that of question 1?
---

## Text filters

!!! tip "What is it ?"
    *Text filters* are commands that read or can read from their standard input and write modified data to their standard output.

    Here are some of the most common:

     - `head` : displays the first lines of its input;
     - `tail` : displays the last lines of its input. With the -f option (to follow, continue to display the end of the file when it is updated) it is one of the favorite commands of system administrators;
     - `grep` : one of the best known commands, displays lines matching a string, or more generally a regular expression in its input;
     - `cut` : selects fields or characters in each line of the standard input;
     - `sort` : sorts its standard input according to criteria.
     - `tr` : replaces characters in its standard input.
     - `uniq` : removes consecutive identical lines in its standard input.
---

### Exercise 7 : Frère Jacques

1. Create a `fj` file containing these lines:
    ```bash
    Frère Jaques, 
    Frère Jacques,                    
    Dormez-vous,
    Dormez-vous,
    Sonnez les matines,
    Sonnez les matines !
    Ding !
    Ding ! 
    Dong !
    ```
    with the `echo` command (**the `<newline>` character corresponds to the enter key on your keyboard**):
    ```bash
    $ echo 'Frère Jaques,<newline> 
    > Frère Jacques,<newline>                     
    > Dormez-vous,<newline> 
    > Dormez-vous,<newline> 
    > Sonnez les matines,<newline> 
    > Sonnez les matines !<newline> 
    > Ding !<newline> 
    > Ding !<newline> 
    > Dong !' > fj
    ```
2. Then test the following commands and observe their results:
    ```bash
    $ cat fj
    $ head fj
    $ tail fj
    $ head -n 2 fj
    $ tail -n 3 fj
    $ grep "Dormez" fj
    $ grep -v "Dormez" fj
    $ grep "dormez" fj
    $ grep -i "dormez" fj
    $ sort fj
    $ uniq fj
    $ cut -c 1 fj
    $ cut -c 2 fj
    $ cut -c 1-3 fj
    $ cut -d ' ' -f 1 fj
    $ cut -d ' ' -f 1,2 fj
    ```
    - Where are the results displayed?
    - What are the `-n` options of `head` and `tail` for?
    - What is the `-v` option of `grep` for? What is the `-i` option of `grep` for?
    - What are the `-c` and `-d` options of `cut` for?

3. Then test the command
    ```bash
    $ tr a-z A-Z fj
    ```
    In your opinion why does the command fail?
4. Then type the following commands and comment on its result:
    ```bash
    $ tr a-z A-Z < fj
    $ tr S D < fj
    $ tail -n 3 fj | tr D B >> fj
    $ cat fj
    ```
    What can you conclude about the `tr` command?


### Exercise 8 : Sort files by size

!!! tip "Base name"
    The base name of a file is the name of the file without its extension. For example the base name of the file `/usr/include/stdio.h` is `stdio`.

In this exercise, we would like to display on the terminal the base name of the 10 smallest files (bytesize-wise) (in size in bytes) among the `.h` files in the `/usr/include` directory.

Using the `wc`, `sort`, `cut`, `head` (or possibly `tail`) commands, and the pipe redirections, write a command that displays the base name of the 10 smallest files (bytesize-wise) among the `.h` files in the `/usr/include` directory.

!!! info "Hint"

    - The `-c` option of `wc` gives you the number of bytes in a file.
    - The `-n` option of `sort` allows you to sort the lines of a file in numerical order.
    - The `-d` option of `tr` removes the characters received as the first argument instead of replacing them.

If you have `gcc`, you should end up with the following files:
```bash
pool
wait
syslog
syscall
lastlog
termio
stab
memory
re_comp
alloca
```
### Exercise 9 : Solo `grep`

!!! tip "`grep` and directories"
    
    - The `-r` option of `grep` allows you to pass a directory as an argument. And asks him to search in all the files in this directory.
    - The `-l` option of `grep` allows you to only display the name of the files that contain the searched string.

Using `grep` and possibly other commands, find a command line that allows you to:

1. Display the value of `RAND_MAX` (it is a constant of the C standard library).
2. Display the absolute path of the files that contain the string `127.0.0.1` in the files of `/etc`.
3. Display only the name of the files that contain the string `127.0.0.1` in the files of `/etc`. (hint: there is a command called `rev`).
4. Display the path of the home directory of the `games` user.