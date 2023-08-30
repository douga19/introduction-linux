# [TI307] - Introduction aux systèmes GNU/Linux

Dans ce tutoriel, nous allons voir comment vous pourrez directement disposer d'un environnement Linux dans Windows en utilisant *Windows Subsystem for Linux* (WSL).

## Activation du WSL
1. Dans la barre de recherche Windows, tapez *"Activer ou désactiver des Fonctionnalités Windows"*.
>> Capture fenêtre
2. Vous verrez apparaître une boîte de dialogue dans laquelle nous allons cocher des options.
3. Cochez les options: **Sous-système Windows pour Linux** et **Plateforme de machine virtuelle**. Ensuite cliquez sur Ok. 
>> Capture fenêtre
4. La boîte de dialogue vous indiquera éventuellement de redémmarer votre ordinateur pour que les changements soient pris en compte.

## Installation d'une distribution GNU/Linux (nous allons installer Debian)
1. Ouvrez ensuite *Windows Store* et tapez dans la barre de recherche **debian**. Une fois que **Debian** est proposé dans les suggestions, cliquez dessus.
2. Cliquez sur Installer.
>> Capture fenêtre
3. À la fin du téléchargement (environ 80Mo), cherchez Debian dans la barre de recherche Windows, et cliquez dessus.
4. Un émulateur de terminal nommé *Debian* va s'ouvrir et finaliser l'installation.
>> Capture fenêtre
5. Dans ce même terminal, une fois l'installation terminée, on vous demandera d'entrer un nom d'utilisateur et un mot de passe. Notez que pour des raisons de sécurité, le mot de passe que vous allez tapez ne va pas apparaître en clair, vous pourriez avoir l'impression de ne rien taper, mais en fait si.
>> Capture fenêtre
6. Une fois votre login et mot de passe renseigné, voilà! Vous avez désormais un système GNU/Linux (en ligne de commande) installé dans Windows.

## Naviguer dans l'arborescence WSL depuis Windows
1. Ouvrez un explorateur de fichier depuis Windows.
2. Dans la barre d'adresse, saisissez: `\\wls$`, puis tapez sur entrée.
>> Capture fenêtre
3. À partir de là, vous pourrez accéder à votre répertoire personnel en cliquant sur `home` puis sur le dossier dont le nom est votre `login`. 
4. À présent vous êtes en mesure de récupérer vos fichiers debian depuis Windows.
5. Afin de tester que tout va bien, dans le terminal debian entrez la commande suivante:
```bash
touch file.txt
```
puis depuis l'explorateur de fichiers Windows vérifiez que le fichier a bien été créé dans votre repertoire personnel (il vous faudra éventuellement actualiser la fenêtre avec `F5`).
6. Éditez ensuite `file.txt` dans un éditeur de texte depuis Windows, puis enregistrer.
>> Capture fenêtre
7. Retournez enfin dans le terminal debian pour vérifier que le fichier a bien été modifié. Tapez la commande:
```bash
cat file.txt
```
8. Vous remarquerez un petit problème avec les fins de ligne, Windows et Unix les gèrent de manières différentes (nous en reparlerons).

## Installer des paquets sous Debian avec `apt`
La plupart des distributions GNU/Linux permettent d'installer des programmes, des bibliothèques (ensemble de programmes), des logiciels précompilés en passant par des *dépôts (repositories en ang.)* en ligne. Les programmes et les bibliothèques présents dans ces dépôts sont appelés des *paquets (packages en ang.)*.

L'installation de ces paquets sont effectués par un ... *gestionnaire de paquets*. Sous Debian et ses dérivés, le gestionnaire de paquets s'appelle `apt`.

Comme ces paquets sont installés sur le système, pour tous les utilisateurs, seul l'administrateur du système est autorisé à les installer, mais vous pourrez prendre ce rôle.

La commande `sudo` permet d'exécuter la commande qui la suit en tant qu'administrateur. Il vous sera demandé votre mot de passe (une fois pas session).

Installons alors quelques paquets.

1. Dans un premier temps, mettez à jour la base de données et les paquets déjà installés en tapant dans votre terminal Debian:
```bash
sudo apt update
sudo apt upgrade
```
Cette étape peut prendre plus ou moins de temps suivant votre connexion internet.
2. Une fois les mises à jour effectuées, nous allons installer 3 paquets : les éditeurs de texte `nano` et `vim` et le compilateur c `gcc` avec la commande suivante:
```bash
sudo apt install nano vim gcc
```
3. Il est également possible de rechercher des paquets par nom ou par mot-clé grâce à l'action `search` de la commande `apt`.
>> Capture fenêtre
4. Pour supprimer/desinstaller un paquet, on utilise l'action `remove` de la commande `apt`:
```bash
sudo apt remove nano
```
5. Enfin, certaines bibliothèques deviennet inutiles une fois que les paquets qui les ont utilisées sont supprimés. L'action `autoremove` permet de faire le ménage en désinstallant les bibliothèques devenues inutiles.
```bash
sudo apt autoremove
```

