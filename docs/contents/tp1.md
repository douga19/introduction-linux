# TP1 - First commands

!!! info "General instructions"
    - Dans tous les exercices, la chaine `$ ` en début de ligne représente l'invite de commande (le *prompt*) et il ne faut pas la taper.
    - Pour l'instant, chaque fois que vous ouvrez un terminal, vous êtes invités à entrer la commande suivante, (suivie, comme toujours de la touche entrée) pour des raisons pédagogiques :

            $ PS1='$ '


## Exercice 1

1. Try out the following commands in a terminal. Describe in one sentence its usefulness, indicate the name of the command, its number of arguments and its arguments.

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
    -   `echo      Hello,        world!`

2. Press on the right arrow key of your keyboard or `C-p` (the `Ctrl` key at the same time as the `p` key) several times, until the command `who` is displayed. Now press the down arrow key or type `C-n` until the command `uname -m -r` is displayed and then press enter. Note what these shortcuts are for and learn them.
3. Press `C-l`. Note what this shortcut is for and learn it.
4. Without explicitly write the command, display the command `cal 3 2022`, *without executing it* (i.e. without pressing enter).
5. Press `C-u`. Note what this shortcut is for and learn it.
6. Display again the command `uname`, without typing it nor executing it. Then press `C-d`. What happened ?
7. Clear the current command line with a keyboard shortcut and then type `C-d`. What happened ?
8. Open again a terminal and type `C-p` several times. Comment.
9. Close the terminal using keyboard shortcuts.

::: exo
**Exercice 2**.

1.  *Ouvrir un nouveau terminal et entrer la commande suivante, en
    respectant scrupuleusement sa syntaxe :*

        $ PS1='$ '

2.  *Entrer la commande `pwd` (pour *print working directory*),
    c'est-à-dire, afficher le nom du répertoire courant) et noter ce qui
    est imprimé à l'écran : c'est le chemin absolu de votre *home*,
    répertoire personnel.*

3.  *Entrer successivement les commandes `cd ..` (avec un espace entre
    `cd` et `..`) et `pwd`, jusqu'à ce que le résultat ne change plus.
    Commenter.*

4.  *Entrer la commande `cd` (sans argument), puis `pwd`. Commenter.*

5.  *Entrer la commande `cd /`, puis `pwd` et `ls`.*

6.  *Entrer la commande `cd /usr/include`. Utiliser la commande `ls`. À
    quoi semble servir ce répertoire ?*

7.  *La commande `cat` (pour *concatenate*) permet d'afficher un ou
    plusieurs fichiers donnés en argument (à la suite) dans le terminal.
    La commande `wc` (pour *word count*) affiche (dans cet ordre) le
    nombre de lignes, de mots et de caractères des fichiers donnés en
    argument, puis, s'il y en a plusieurs, les sommes de ces nombres
    pour tous les fichiers. Afficher le contenu le nombre de lignes du
    fichier `stdlib.h`. Donner le nombre total de lignes des fichiers
    `stdlib.h` et `stdio.h`.*

8.  *Entrer les commandes `cd ..`, `pwd` puis `ls`.*

9.  *Entrer les commande `cd share/man`, puis `pwd` et `ls`. Pouvez-vous
    deviner ce que désignent certains des résultats affichés ?*

10. *Entrer la commande `ls /bin`. Certains noms vous sont-ils familiers
    ?*

11. *Le caractère **\~** (qui se lit *tilde*) est saisi au clavier avec
    la combinaison de touches `Alt Gr-2`. Entrer la commande `echo ~`,
    puis la commande `cd ~`. Qu'a fait le shell au caractère `~` ?*

12. *Représenter les répertoires et fichiers mentionnés dans l'exercice
    sous la forme d'une arborescence (c'est-à-dire comme un arbre
    généalogique).*
:::

::: exo
**Exercice 3**.

1.  *Assurez-vous que vous êtes bien dans votre répertoire personnel et
    listez son contenu.*

2.  *Entrer la commande `mkdir tp_shell` (pour *make directory*,
    c'est-à-dire créer un répertoire). Lister le contenu du répertoire
    personnel et du répertoire `tp_shell`.*

3.  *Entrer la commande `mkdir abeilles tp_shell/tp1 ~/arbres`.
    Qu'a-t-elle fait ? Parmi ses arguments, lesquels sont des chemins
    absolus et lesquels sont des chemins relatifs ? (indice : voir le
    résultat de `echo ~/arbres`).*

4.  *Que fait la commande suivante ?*

        $ mkdir -p vivant/plante/fleur tp_shell/tp1/exos/ex1/

5.  *Le shell `bash` (qui est votre shell par défaut) a une
    fonctionnalité qui permet de gagner énormément de temps et d'éviter
    les fautes de frappe : la complétion automatique. Elle se fait avec
    la touche tabulation (la touche à gauche de la touche `a`). Saisir
    les caractères suivants (la touche tabulation est représentée
    ci-dessous par `<Tab>`) et voir le résultat dans le terminal :*

        $ mkd<Tab> vi<Tab><Tab><Tab>roses

6.  *Lorsque plusieurs choix sont possible, tabulation ne provoque pas
    de complétion, mais appuyer deux fois de suite sur cette touche
    liste les choix possibles : essayer avec*

        $ ls a<Tab><Tab>

7.  *La commande `rmdir` (pour *remove directory* ) permet de supprimer
    des répertoires. La tester avec la commande*

        $ rmdir vivant tp_shell/tp1/exos/ex1

    *puis supprimer le sous-répertoire `tp1` du répertoire `tp_shell`.*

8.  *La commande `touch` permet (entre autres choses) de créer des
    fichiers (normaux) vides. Observer le résultat de la commande
    (exécutée depuis votre répertoire personnel) :*

          $ touch ~/arbres/hello.c abeilles/truc.txt bidule

    *en tapant*

        $ ls ~/arbres abeilles/ .

    *Remarque : `.` désigne le répertoire courant.*

9.  *La commande `mv` pour *move*, permet de déplacer ou de renommer des
    fichiers. Observer avec `ls` le résultat de chacune des commandes
    suivantes :*

        $ mv arbres/hello.c arbres/bonjour.c
        $ mv abeilles arbres vivant/
        $ mv bidule vivant
        $ mv vivant vie

    *Compléter la phrase suivante : Si le dernier argument de `mv` est
    un répertoire existant, alors , sinon `mv` doit avoir arguments et
    son premier est .*

10. *La commande `cp` pour *copy* , permet de copier des fichiers et des
    répertoires. Observer le résultat des commandes suivantes :*

        $ cp vie/arbres/bonjour.c salut.c
        $ mkdir copies
        $ cp salut.c vie/abeilles/truc.txt copies
        $ cp vie/bidule tp_shell copies
        $ cp -R vie/bidule tp_shell copies
        $ cp vie copie_vie
        $ cp -R vie copie_vie

    *Décrire le fonctionnement de la commande `cp`, selon que son
    dernier argument est un répertoire existant ou non et que l'option
    `-R` est présente ou non.*

11. *Enfin, la commande `rm` (pour *remove* ) permet de supprimer
    fichiers et répertoires. Observer le résultat des commandes
    suivantes :*

        $ rm vie/bidule
        $ rm copies
        $ rm -r copies
        $ rm -R copie_vie
        $ rm -i vie/arbres/bonjour.c vie/abeilles/truc.txt

12. *Supprimer tous les fichiers et répertoires créés pendant cet
    exercice.*
:::

::: {#exo:arbo .exo}
**Exercice 4**. *Créer l'arborescence suivante. Le **\~** représente le
répertoire personnel de l'utilisateur. Les répertoires sont en gras. Les
répertoires **Mail**, **Rapport** et **Web** seront créés en une seule
commande à l'aide de `mkdir`.*

*Utiliser la commande `touch` pour créer les fichiers ordinaires et un
éditeur de texte (par exemple `gedit`) pour entrer des phrases (peu
importe lesquelles) dans ces fichiers.*

::: center
:::

*À partir du répertoire personnel faites les actions suivantes (il
existe plusieurs solutions possibles) :*

1.  *Aller directement dans **\~**`/Rapport/Docs/Afaire`*

2.  *De là, passer dans **\~**`/Rapport/Docs/Fait` et y copier le
    fichier `rapport.txt`. Rappel : le répertoire courant peut être
    désigné par `.` (un point).*

3.  *Renommer cette copie `rapport_copie.txt`*

4.  *Revenir dans **\~**`/Rapport`*

5.  *Sans changer de répertoire, regarder avec la commande `cat` le
    contenu de `index.html`*

6.  *Sans changer de répertoire, lister le contenu du répertoire
    **Web**.*

7.  *Revenir dans **\~** et supprimer toute l'arborescence.*
:::

::: exo
**Exercice 5**. *Comme vu en cours, les commandes shell peuvent être
soit des commandes internes (ou primitives) du shell, soit des fonctions
shell, soit des alias, soit des commandes dites externes, c'est-à-dire
des programmes compilés ou des scripts installés sur le système.*

*Pour chaque nom de commande qui apparaît dans les exercices précédents,
dire avec la commande `type` à quelle catégorie il appartient (ne pas
oublier `type`).*

*Quels répertoires contiennent la plupart des programmes installés sur
le systèmes ?*
:::

La commande `man` fournit de l'aide *pour les commandes externes*. Pour
les primitives de `bash`, on peut utiliser la commande `help`.

::: exo
**Exercice 6**.

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
