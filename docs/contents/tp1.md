---
title: TP1 - First commands
---

# TP1 - First commands

!!! info "General instructions"
    - In all exercises, the `$ ` chain at the beginning of the line represents the command prompt and should not be typed.
    - For now, each time you open a terminal, you are prompted to enter the following command, (followed, as always, by the enter key) for pedagogical reasons:

            $ PS1='$ '


## Exercise 1 : First commands

1. Try out the following commands in a terminal. Describe in one sentence its usefulness, indicate the name of the command, its number of arguments and its arguments. For example, the first command is `date`, it has no argument and its usefulness is to display the current date and time.
    -   `date`
    -   `cal`
    -   `cal 3 2022`
    -   `who`
    -   `who am i`
    -   `  who  am   i`
    -   `uname`
    -   `uname -m -r`
    -   `uname -mrs`
    -   `echo Hello, world!`
    -   `echo \ \ \ \Hello,        world!`
2. Press on the right arrow key of your keyboard or `C-p` (the `Ctrl` key at the same time as the `p` key) several times, until the command `who` is displayed. Now press the down arrow key or type `C-n` until the command `uname -m -r` is displayed and then press enter. Note what these shortcuts are for and learn them.
3. Press `C-l`. Note what this shortcut is for and learn it.
4. Without explicitly write the command, display the command `cal 3 2022`, *without executing it* (i.e. without pressing enter).
5. Press `C-u`. Note what this shortcut is for and learn it.
6. Display again the command `uname`, without typing it nor executing it. Then press `C-d`. What happened ?
7. Clear the current command line with a keyboard shortcut and then type `C-d`. What happened ?
8. Open again a terminal and type `C-p` several times. Comment.
9. Close the terminal using keyboard shortcuts.

## Exercise 2 : Directories and files

1. Open a terminal and type the following command, respecting its syntax:

        $ PS1='$ '
2. Type the command `pwd` (for *print working directory*), that is, display the name of the current directory) and note what is printed on the screen: it is the absolute path of your *home*, personal directory.
3. Type the command `cd ..` (with a space between `cd` and `..`) and then `pwd`. Repeat these two commands several times until the result remains the same. What happened ?
4. Type the command `cd` (without argument), then `pwd`. Comment.
5. Type the command `cd /`, then `pwd` and `ls`.
6. Type the command `cd /usr/include`. Use the command `ls`. What does this directory seem to be used for ?
7. The `cat` command (for *concatenate*) displays one or more files given as arguments (one after the other) in the terminal. The `wc` command (for *word count*) displays (in this order) the number of lines, words and characters of the files given as arguments, then, if there are several, the sums of these numbers for all the files. Display the contents of the `stdlib.h` file and the number of lines of this file.
8. Type the commands `cd ..`, `pwd` and `ls`.
9. Type the commands `cd share/man`, then `pwd` and `ls`. Can you guess what some of the displayed results refer to ?
10. Type the command `ls /bin`. Are some of the names familiar to you ?
11. The **`~`** character (which is read *tilde*) is entered on the keyboard with the key combination `Alt Gr-2`. Enter the command `echo ~`, then the command `cd ~`. What did the shell do to the character `~` ?
12. Represent the directories and files mentioned in the exercise as a tree (i.e. as a genealogical tree).

## Exercise 3 : Manipulating directories and files (1)

1. Make sure you are in your home directory and list its contents.
2. Type the command `mkdir tp_shell` (for *make directory*, i.e. create a directory). List the contents of the home directory and the `tp_shell` directory.
3. Type the command `mkdir abeilles tp_shell/tp1 ~/arbres`. What did it do ? Among its arguments, which are absolute paths and which are relative paths ? (hint: see the result of `echo ~/arbres`).
4. What does the following command do ?

        $ mkdir -p vivant/plante/fleur tp_shell/tp1/exos/ex1/

5. The `bash` shell (which is your default shell) has a feature that saves a lot of time and avoids typos: automatic completion. It is done with the tabulation key (the key to the left of the `a` key). Enter the following characters (the tabulation key is represented below by `<Tab>`) and see the result in the terminal:

        $ mkd<Tab> vi<Tab><Tab><Tab>roses

6. When several choices are possible, tabulation does not trigger completion, but pressing the tabulation key twice in a row lists the possible choices: try with

        $ ls a<Tab><Tab>

7. The `rmdir` command (for *remove directory*) allows you to delete directories. Test it with the command

        $ rmdir vivant tp_shell/tp1/exos/ex1

and then delete the subdirectory `tp1` from the directory `tp_shell`.
8. The `touch` command allows (among other things) to create empty (normal) files. Observe the result of the command (executed from your home directory):

        $ touch ~/arbres/hello.c abeilles/truc.txt bidule
    
    by typing
    
        $ ls ~/arbres abeilles/ .
    
    !!! note inline end
        `.` refers to the current directory.

9. The `mv` command for *move*, allows you to move or rename files. Observe with `ls` the result of each of the following commands:
        
        $ mv arbres/hello.c arbres/bonjour.c
        $ mv abeilles arbres vivant/
        $ mv bidule vivant
        $ mv vivant vie

10. The `cp` command for *copy*, allows you to copy files and directories. Observe the result of the following commands:

        $ cp vie/arbres/bonjour.c salut.c
        $ mkdir copies
        $ cp salut.c vie/abeilles/truc.txt copies
        $ cp vie/bidule tp_shell copies
        $ cp -R vie/bidule tp_shell copies
        $ cp vie copie_vie
        $ cp -R vie copie_vie

    Describe the operation of the `cp` command, depending on whether its last argument is an existing directory or not and whether the `-R` option is present or not.        

11. Finally, the `rm` command (for *remove*) allows you to delete files and directories. Observe the result of the following commands:

        $ rm vie/bidule
        $ rm copies
        $ rm -r copies
        $ rm -R copie_vie
        $ rm -i vie/arbres/bonjour.c vie/abeilles/truc.txt

12. Delete all files and directories created during this exercise.

## Exercise 4 : Manipulating directories and files (2)

!!! failure ""
    mila ampiana sary

Create the following tree structure. The `~` represents the user's home directory. The directories are in bold. The **Mail**, **Rapport** and **Web** directories will be created in a single command using `mkdir`.

Use the `touch` command to create the ordinary files and a text editor (e.g. `gedit`) to enter sentences (no matter which) in these files.

From your home directory, perform the following operations (there are several possible solutions):
1. Go directly to `~/Rapport/Docs/Afaire`.
2. From there, go to `~/Rapport/Docs/Fait` and copy the file `rapport.txt` there. Reminder: the current directory can be designated by `.` (a dot).
3. Rename this copy `rapport_copie.txt`.
4. Go back to `~/Rapport`.
5. Without changing directories, display the content of the file`index.html` using the `cat` command.
6. Without changing directories, list the contents of the `Web` directory.
7. Get back into `~` and delete the whole tree structure of this exercise.

## Exercise 5 : Built-in commands

!!! info ""

    Shell commands can be either internal (or primitive) shell commands, shell functions, aliases, or external commands, i.e. compiled programs or scripts installed on the system. 
    
1. For each command name that appears in the previous exercises, say with the `type` command which category it belongs to (don't forget `type`).
2. Can you guess which directories contain most of the programs installed on the system ?

!!! info ""

    The `man` command provides help *for external commands*. For `bash` primitives, you can use the `help` command.

## Exercise 6

1.  *Entrer la commande `ls`. À quoi servent les options `-l` et `-a` ?
    Taper sur la touche `q` pour sortir de l'aide et les tester.*

2.  *À l'aide du manuel, dire à quoi sert l'option `-f` de la commande
    `rm` et comment on peut supprimer un fichier dont le nom commence
    par un tirer (comme par exemple `-f`).*

3.  *À l'aide du manuel, décrire l'utilité de l'option `-k` de la
    commande `man`. La tester pour lister les navigateurs web installés
    (et documentés) sur le système.*

4.  *À l'aide de la commande `help`, obtenir de l'aide sur les commandes
    `echo` et `type` intégrées au shell `bash`.*

5.  *Voir la page de manuel de `touch`. À quoi sert ce programme, si ce
    n'est à créer des fichiers vides ?*

6.  *Revoir la page de manuel de `man`. Dans quelle section sont les
    programmes et les commandes du shell ? Dans quelle section sont
    documentées les bibliothèques (comme la bibliothèque standard du C)
    ? Expliquer la différence entre les deux commandes suivantes :*

        $ man 1 printf
        $ man 3 printf

7.  *Dans la page de manuel de `mv`, observer les deux premières lignes
    de la partie `SYNOPSIS`. Que signifient les crochets ? les points de
    suspension ? Si besoin, se reporter au manuel de `man`.*
:::

Pour rappel, les caractères jokers sont seulement :

`*`

:   : correspond à toute chaîne de caractère (éventuellement vide) sauf
    les chaînes commençant par le caractère `.` dans le cas où `*` est
    en début de chaîne ;

`?`

:   : correspond à un caractère quelconque ;

`[ ]`

:   : correspond à un (et un seul) caractère à l'intérieur des crochets.
    On peut utiliser des intervalles, comme dans `[a-z]` qui correspond
    à une seule lettre minuscule ou dans `[0-5]` qui correspond à un
    seul chiffre entre $0$ et $5$. On peut inverser la recherche en
    faisant commencer l'intervalle par `^` : par exemple `[^0-9]`
    correspond à un caractère qui est tout sauf un chiffre.

Plus d'information dans `man bash` à la rubrique Développement des
chemins (*pathname expansion*).

::: exo
**Exercice 7**. *Créez le répertoire `tp_joker` dans votre répertoire
personnel. Déplacez-vous dans ce répertoire. Créez les fichiers (vides)
suivants : `annee1` `Annee2` `annee4` `annee45` `annee41` `annee510`
`annee_saucisse` `annee_banane` `bonbon`*

1.  *Essayer de prévoir le résultat des commandes suivantes, puis les
    tester :*

        $ echo *
        $ echo *_*
        $ echo [ab]*
        $ echo [^ab]*
        $ echo c*
        $ echo ??????

2.  *Lister tous les fichiers :*

    1.  *se terminant par `5`*

    2.  *commençant par `annee4` ;*

    3.  *commençant par `annee4` et de 7 lettres maximum ;*

    4.  *commençant par `annee` dont le sixième caractère n'est pas un
        chiffre ;*

    5.  *contenant la chaîne `ana` ;*

    6.  *commençant par `a` ou `A` ;*

    7.  *dont l'avant-dernier caractère est `4` ou `1` ;*

3.  *Lister les fichiers cachés (c'est-à-dire ceux commençant par le
    caractère `.`) situés dans votre répertoire personnel.*

4.  *Lister les fichier commençant par `std` et se terminant par `.h`
    dans le répertoire `/usr/include`.*

5.  *Lister les fichiers se trouvant dans un répertoire
    arrière-petit-enfant de la racine, commençant par une lettre `w`
    majuscule ou minuscule et se terminant par `.h`.*
:::
