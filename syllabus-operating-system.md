
    Introduction et prérequis
        Rôle d'un système d'exploitation et histoire des systèmes UNIX
        Architecture des systèmes Unix
        Le système GNU/Linux
        Tâches effectuées par le noyau Linux
        La norme POSIX  
        Programmation en C et outils de compilation
        Différence entre libc et appels système
        Le système d'interprètes de commandes shell (exemple : bash)
        Le man (comment utiliser la commande man)
        Format des commandes (cmd -options -- option arg1 arg2 ...)
        Basic shell commands: man, ls, cd, cp, mv, pwd, cat, wc, less, grep
        Commandes Linux
            Commandes Linux de base
                Format d'une commande Linux
                Exemples pratiques: man, ls, cd, cp, mv, pwd, cat, wc, less, grep, cat, less, file, rm, find
        Programmation
            Utilisation d'un éditeur de texte pour écrire des programme en C: gedit et emacs
            Utilisation de gcc pour la compilation
            Arguments du main
            perror

    Entrée et sortie standard
        Commandes shell de gestion de fichiers et redirections (<, >, &>, | ...)
        Descripteurs de fichiers
        Les canaux stdin, stdout et stderr
        L'appel système open avec ses options, paramètres, droits ...
        Lire le manuel d'open (man 2 open)
        L'appel système read(), write(), close() avec ses différentes options, paramètres.
        Commandes Linux
            Commandes de redirection (> >> < 2> &> |)
            Commandes: file, cat , ls
        Programmation
            Appel système
                open(O_READONLY, ORDWR...), read, write, close

    Organisation du système de fichiers
        Arborescence du système de fichiers Linux
        Organisation du disque dur
        Organigramme d'une partition UNIX
        Système de fichiers /dev
        Partitions et périphériques de stockage (/dev/sda...) et l'outil fdisk
        inodes
        Types de fichiers (bloc, caractère, lien symbolique, ...)
        Droits d'accès (ls -l, chmod, chown...)
        lseek, dup, dup2 appel système
        Système de fichiers /proc
        Commandes Linux
            ls -l et permissions
            chmod
            chown
        Programmation
            lseek()
            dup
            dup2

    Notion de processus
        Définition d'un processus (pid, ppid, ...)
        Commandes de manipulation des processus : top, ps, bg, fg, jobs...
        Arbre de processus (init ...)
        Priorité : mode utilisateur / mode noyau
        Système de fichiers /proc
        Appels système getpid(), getpgrp(), getppig(), setpgrp()
        Appels système getuid(), geteuid()
        Ordonnancement (R, T, S, D, Z...)
        Appel système fork()
        Appel système wait(), waitpid()...
        Appel système exec(), execl(), execv(), execve()
        Commandes Linux
            Mise en pratique des commandes : top, ps, bg, fg, jobs, top, htop
            Système de fichiers /proc
        Programmation
            Appel système fork()
            Appel système wait(), waitpid()...
            Appel système exec(), execl(), execv(), execve() 
    Signaux
        Introduction à la communication entre processus
        Signaux (kill -l) et leurs différents rôles
        Les commandes bash kill() et trap()
        Appel système signal() et fonction raise() de la libc
        Redirection des signaux avec l'appel système sigaction()
        Commandes Linux
            Mise en pratique des commandes : kill -l , kill trap
        Programmation
            Appels système kill, signal et sigaction 





