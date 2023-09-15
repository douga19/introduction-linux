---
title: Lab3 - Working environment
---

# Lab3 - Working environment

!!! info "Instructions"

    - We recall that in all exercises the `$` at the beginning of the command represents the prompt, it is not to be entered when you write a command line.
    - For each new command, do not hesitate to consult its manual page with the `man` command, or to use the `--help` option (if it is available) to know what it does.


## Shell variables

!!! tip "Definition and usage of shell variables"
    
    A variable is a name that is associated with a value. In shell, variables are strings. The **development** of a variable is the replacement of the variable name by its value.

    For example, the variable `PS1` is the variable that contains the shell prompt. In the previous labs, when you typed the command `PS1='$ '`, you assigned the string `$<space>` to the variable `PS1`. When the shell displays the prompt, it develops the variable `PS1` and displays the string `$<space>`.

    Shell variables are environment variables. They are accessible to all processes launched by the shell. They can be listed with the `env` or `printenv` command. They can also be listed with the `set` command which also lists the internal variables of the shell (see the `set` manual page for more details).
---

### Exercise 1 : Shell variables

1. Type the following commands in a terminal:
```bash
$ file_name=hello.c
$ echo file_name
$ echo $file_name
$ echo ${file_name}
$ touch $file_name
$ echo $file_namepp
$ echo ${file_name}pp
$ rm ${file_name}
```
1. Recall what the `echo` command does. In your opinion, what is the purpose of the `$` character in front of the variable name `file_name`?
2. What happens if you ask the shell to display the contents of a variable that does not exist?
3. What happens if you put a space between the variable name and the equal sign `=`? And between the equal sign and the value?
4. Enter the following commands and try to comment on their effect:
```bash
$ subject=Alice verb=likes do=programming
$ sentence="$subject $verb $do."
$ echo $sentence
$ subject=Bob verb=eats do=salad
$ echo $sentence
$ echo "$subject $verb $do."
```

## Special characters and inhibition
!!! tip "Special characters"

    Some characters have a special meaning for the shell: they are said to be *special*. Conversely, a character that has no other meaning than itself is said to be *literal*. We list below the special characters; most of them will be seen in detail later in the course.
    
    - `; <newline> | &` They end the command that precedes them. We used `<newline>` to represent the *new line* character that is entered with the Enter key. The special character `|` is entered with the key combination `Alt Gr-6` (`Option-Shift-l` under mac), it is called *pipe*. The special character `&` is entered with the key combination `Alt Gr-8` and is used to launch commands in the background.
    - `< >` called chevrons, they allow *redirections*.
    - `( )` to group commands and run them in a sub-shell.
    - `$` for variable development, arithmetic development and command substitution.
    - `` ` `` called backtick or backquote is for command substitution (old syntax). It is entered on the keyboard with the key combination `Alt Gr-7` followed by a space.
    - `<space> <tab>` delimit command names and arguments.
    - `\ ' "` the backslash, the single quote and the double quote which precisely allow to inhibit special characters, that is to make them have their literal meaning.

    Then, the following characters have a special meaning in certain contexts and must therefore sometimes be inhibited:
    
    - `* ? ]` For path name development.
    - `#` To write comments (unless it is in the middle of a word).
    - `~` For tilde development (home directory).
    - `=` For variable assignment.
    - `%` For task control (job control).
---

### Exercise 2 : Backslash inhibition (`\`)
1. Test the following commands.
```bash
$ echo a b
$ echo a\ \ \ b
$ touch empty\ file
$ rm empty file
$ rm empty\ file
$ echo 3$canadians
$ echo 3\$canadians
$ echo ; echo *
$ echo \; echo \*
$ echo "hello"
$ echo \"hello\"
$ echo 'hello'
$ echo \'hello\'
$ echo \
$ echo \\
```
1. Referring to the previous questions, answer the following questions:
    - What does the `\` character in front of another character than `<newline>` do (we recall that the character `<newline>` is the one that results from pressing the Enter key on the keyboard)?
    - What is the purpose of the character string `\<newline>`?
    - How can we get a literal `\` character? How to display `\\` using the `echo` command?


### Exercise 3 : Simple quotes inhibition (`'`)
!!! info "Remark"
    The `-i` option of the `rm` command allows you to request confirmation before deletion.

1. Test the following commands:
```bash
$ touch 'this is an horrible name for a file'
$ rm -i this is an horrible name for a file
$ rm -i 'this is an horrible name for a file'
$ touch p; echo is the * character special ? and ?
$ echo 'is the * character special ? and ?'
$ echo 'actually, even the end of line<newline>is a normal character between<newline>apostrophes'
$ echo 'isn't it only simple quote that is special between simple quotes ?'
```
    where `<newline>` is to be typed with the Enter key of your keyboard.
2. At the sight of the previous experiments (and others to be invented if necessary), answer the following questions:
    - What are the characters that are special between apostrophes?
    - How to get an apostrophe in a string between apostrophes (tricky question)?
    - How, with a combination of strings between apostrophes and a backslash inhibition, to obtain with `echo` the following display?
    ```bash
    Can't we inhibit a variable development (like $var); for example between simple quotes ?
    ```

### Exercise 4 : Double quotes inhibition (`"`)

1. Test the following commands and note your observations:
```bash
$ echo "? * and [ are used for path name expansion"
$ echo "~ is the expansion of the home directory"
$ echo "Between \" , we can also <newline> write on several<newline> lines"
$ name=Alice
$ echo '$name '
$ echo "$name writes a shell script"
$ echo "\$name writes a shell script"
$ echo "the absolute path to your home directory is `pwd`"
$ echo "the absolute path to your home directory is \`pwd\`"
$ echo "the absolute path to your home directory is $(pwd)"
$ echo "the absolute path to your home directory is \$(pwd)"
$ echo "It is known than 2 + 2 is $((2 + 2))"
$ echo "It is known than 2 + 2 is \$((2 + 2))"
$ echo "\\\\\"\$\`\*\'"
```
2. Try those commands on a terminal and note their results:
```bash
$ myvar ="Alice<newline> and<newline>Bob"
$ echo $myvar are doing a lot of things
$ echo "$myvar are doing a lot of things"
```
3. From the previous experiments (and others to be invented if necessary), answer the following questions:
    - What are the characters that are special between double quotes?
    - What is the role of the `\` character between double quotes? In what context is it special, literal?
    - What are the developments that never take place between double quotes?
    - In your opinion, why have several inhibition mechanisms been created?

## Pathname expension
!!! tip "Pathname expension"
    
    When a path contains wildcards (Ref. last exercise of Lab1), the shell expands it by replacing the special characters `*`, `?` and `[` by the names of the files that match the regular expression that results from the extension of the path. This mechanism is called *pathname expansion*.

    For instance, if the current directory contains the files `a`, `b`, `c`, `d` and `e`, then the path `a*` is expanded to `a`, the path `?` to `a b c d e` and the path `[a-c]` to `a b c`.
    
    Pathname expansion is performed by the shell, before the command is executed. If no file matches the regular expression, the shell leaves the path as it is.
---

### Exercise 5 : Files and images

1. Create a directory `dir` and create the empty files `file-1.txt`, `file-2.txt`, `file-3.txt`, `file-4.txt`, `file-5.txt`, `file-6.txt`, `file-7.txt`, `file-8.txt`, `file-9.txt`, `config-a.txt`, `file-b.txt` in it.
2. Also create in `dir` the following empty files `img-1.png`, `img-2.png`, `img-3.png`, `img-4.png`, `img-5.png`, `img-6.png`, `img-7.png`, `img-8.png`, `img-9.png`.
3. Then create in `dir` two subdirectories `files` and `imgs`.
4. Using the pathname expansion and the `mv` command, move the `.txt` files to the `files` directory. Do the same for the `.png` files in the `imgs` directory.
5. Give the expression that recognizes the files `config-a.txt` and `file-b.txt`. Then remove the files corresponding to this expression. (Thanks to the pathname expansion, you can do it in a single command).
6. Delete the directory `dir` and its contents.

### Exercise 6 : Brace expansion

1. Try the following commands and observe their results:
```bash
$ echo {a, b, c, d}
$ echo {a..d}
$ echo {a..d..2}
$ echo {1, 2, 3, 4, 5, 6, 7, 8, 9}
$ echo {1..9}
$ echo {1..9..2}
```
2. What does the `echo {a..d}` command ? What is the role of the comma `,` in the brace expansion ?
3. What does the `echo {a..d..2}` command ? What is the role of the `2` in the brace expansion ?
4. Test the following commands and observe their results.
```bash
$ echo {a..d}*
$ echo {a..d}.*
$ echo {a..d}.txt
```
6. Create a directory `dir`. Move to it. Using brace expansion, in a single command, create the empty files `file-1.txt`, `file-2.txt`, `file-3.txt`, `file-4.txt`, `file-5.txt`, `file-6.txt`, `file-7.txt`, `file-8.txt`, `file-9.txt`.
7. Move all `.txt` files to a directory `dir/files`.
8. Create a directory `dir/imgs`. Move to it. Using brace expansion, in a single command, create the empty files `img001.png`, `img002.png`, `img003.png`, `img004.png`, `img005.png`, `img006.png`, `img007.png`, `img008.png`, `img009.png`.
9. Delete the directory `dir` and all its contents.


## Command substitution
!!! tip "Command substitution"
    
    Command substitution is a mechanism that allows the result of a command to be inserted into a string of characters.

    Command substitution in a string of characters is another facility offered by the shell. It allows you to capture the output of a command and assign it to a variable or use it as an argument to another command. Since many Linux commands generate output, command substitution can be very useful.

    There are two syntaxes for command substitution: the old syntax with backticks (`` ` ``) and the modern syntax with parentheses `$(...)`. The old syntax is deprecated because it does not allow command substitutions to be nested. We will not present it here.
---

### Exercise 7 : Simple command substitution

1. Try the following commands and observe their results:
```bash
$ date
$ echo date
$ echo $(date)
$ today=$(date)
$ echo $today
$ echo "Today is $(date)"
```
2. What does the `echo $(date)` command do? What is the role of the `$` in front of the opening parenthesis `(`?
3. Then type the following commands and observe their results:
```bash
$ prefix="Today is"
$ echo $prefix $(date)
$ echo $prefix $today
$ echo ${prefix} ${today}
$ sentence=${prefix} ${today}
$ sentence="${prefix} ${today}"
$ echo $sentence
$ echo "$sentence"
```
4. Can you deduce the role of the English quotes in command substitution?
5. What is the difference between `$(...)` and `${...}`?

### Exercise 8 : Nested command substitution

1. Test the following commands and observe their results:
```bash
$ echo $(echo $(date))
$ echo $(echo $(echo $(date)))
$ echo $(echo $(echo $(echo $(date))))
$ echo $(echo $(echo $(echo $(echo $(date)))))
```
2. Then type the following commands:
```bash
$ echo
```
    Without executing the following command, can you predict its result?
    ```bash
    $ echo $(echo $(echo $(echo $(echo))))
    ```
