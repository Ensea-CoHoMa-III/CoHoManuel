# GIT & GITHUB

**<u>I. Le setup de git</u>**

Il est preferable d'être sous linux, ça rend tout plus simple : autant pour le dev que pour l'installation et l'utilisation de git. Quoi qu'il en soit, l'installation suit la même logique sur tous les OS.

* **Installation**
  
__Etape 0 :__ (Windows) Télécharger git [ici](https://git-scm.com/download/win).

__Etape 1 :__ Installer git
* *(Linux)* En fonctionde votre distribution, utilisez votre package manager habituel :
    * *Debian/Ubuntu* : `sudo apt-get install git`
    * *ArchLinux* : `sudo pacman -S git`
    * *Fedora* : `sudo dnf install git`
    * ...
* *(Windows)*  Ouvrir le .exe téléchargé et suivre les instructions OU Desinstaller Windows et installer linux 
* *(Mac)* Installer via Homebrew : `brew install git`
  
__Etape 2 :__ Vérifier l'installation
* *(Linux)* Ouvrir un terminal et taper `git --version`
* *(Mac)* Ouvrir un terminal et taper `git --version`
* *(Windows)* Ouvrir git bash et taper `git --version`

__Etape 3 :__ Créer un compte sur [GitHub](github.com) (si ce n'est pas déjà fait).

Idéalement, il faut utiliser votre compte ENSEA : ça vous donnera accès à Copilot (nottament) et vous serez plus rapidement invité sur le projet CoHoMa

__Etape 4 :__ Prevenir le prof de l'ENSEA pour qu'il vous ajoute au projet CoHoMa sur GitHub.

* **Configuration de git**

__Etape 1 :__ Ouvrir un terminal
* *(Linux)* Ouvrir un terminal 
* *(Windows)* Ouvrir git bash

__Etape 2 :__ Configurer votre nom d'utilisateur et votre adresse email
```bash
    git config --global user.name "<votre pseudo github OU votre nom>"
    git config --global user.email "<votre adresse email github>"
```

__Etape 3 :__ *(Linux et Mac)* ajouter une clé SSH au compte GitHub

Sous linux et mac, il est impossible de se connecter à un compte GitHub sans clé SSH. Il faut donc en générer une et l'ajouter à votre compte GitHub.

1. Dans le terminale, taper la commande suivante : `ssh-keygen -t rsa -b 4096 -C "<votre adresse email github>"`
2. Appuyer sur "Entrée" pour accepter le nom de fichier par défaut.
3. Entrer une passphrase et appuyer sur "Entrée"
4. Aller lire le contenu de la clé SSH générée : `cat ~/.ssh/id_rsa.pub`
5. Copier le contenu de la clé SSH (selecionnez avec votre souris puis CTRL+SHIFT+C)
6. Aller sur votre compte GitHub, dans "Settings" puis "SSH and GPG keys"
7. Cliquer sur "New SSH key"
8. Coller la clé SSH dans le champ "Key"
9. Donner un titre à la clé SSH (par exemple "PC de <votre nom>")
10. Cliquer sur "Add SSH key"
11. Retourner sur le terminal et lancer un ssh-agent : `eval "$(ssh-agent -s)"`
12. Ajouter la clé SSH à l'agent : `ssh-add ~/.ssh/id_rsa`

***Attention :*** Il est possible que l'agent SSH ne démarre pas automatiquement au démarrage de votre session. Il faut donc le lancer manuellement à chaque fois que vous ouvrez une nouvelle session OU Trouver un moyen d'automatiser le lancement de l'agent SSH au démarrage de votre session... Mais je vais pas vous aider là-dessus : bon courage !

__Etape 4 :__ Configurations de certains automatisme de git

**TODO mais je n'ai pas encore exploré les options de git.**

Et voilà, git est installé et configuré sur votre machine ! Vous pouvez maintenant l'utiliser pour le projet CoHoMa.

**<u>II. Les commandes de base</u>**

Git est un outil de gestion de version. Il permet de suivre les modifications apportées à un projet au fil du temps. Il est donc essentiel de bien comprendre comment l'utiliser pour éviter de perdre des données ou de faire des erreurs. Pour travailler sur un projet versionner il faut initialiser un dépôt git appelé repository (ou repo). 

* **Initialiser un dépôt git**  
`git init <nom_du_dépôt>`

Vous permet de créer un nouveau dépôt git dans le répertoire courant. Une fois le dépôt créé, les commandes git pourront être utilisées.  

Cependant, si vous voulez plutôt contribuer à un projet déjà existant, il faut cloner le dépôt.

* **Cloner un dépôt git**  
`git clone <url_du_dépôt> <nom du dossier de destination>`

  * Pour trouver le lien de votre répo, rendez-vous sur la page de votre répo github et cliquez sur le bouton vert "Code". Vous aurez le choix entre deux protocoles : HTTPS et SSH.
    * **Si vous êtes sous Windows**, utilisez le lien HTTPS. (mais passez sous linux quand même, c'est mieux)
    * **Si vous êtes sous linux**, utilisez le lien SSH. Il sera peut-etre nécessaire d'entrer votre passphrase SSH.
  * Si vous ne spécifiez pas de nom de dossier de destination, le dépôt sera cloné dans un dossier du même nom que le dépôt. Si vous le spécifiez, un dossier du nom que vous avez spécifié sera créé et le dépôt sera cloné à l'intérieur. 

Maintenant qu'un dépôt git est créé ou cloné, on va voir les différentes actions possibles sur un dépot git.

* **Indexer les fichiers**
`git add <nom_du_fichier | des fichiers | .>`

Cette commande va permettre d'ajouter un ou plusieurs fichiers à l'index git. L'index git est une sorte de zone tampon entre le répertoire de travail et le dépôt git. Il permet de préparer les fichiers avant de les valider dans le dépôt. 
  
  + Si vous voulez indexer **tous les fichiers** du répertoire courant, utilisez `git add .` (le point signifie "tous les fichiers du répertoire courant").
  +  Si vous voulez indexer **un fichier/dossier spécifique**, utilisez `git add <nom_du_fichier>`.
  +  Si vous voulez indexer **plusieurs fichiers/dossiers**, utilisez `git add <nom_du_fichier_1> <nom_du_fichier_2> ...`.

Nous verrons plus tard comment desindexer un fichier (c'est à dire le retirer de l'index git) et/ou annuler les modifications apportées à un fichier.


* **Valider les fichiers : commit**
`git commit -m "<message_de_commit>"`

Cette commande va permettre de valider les fichiers indexés dans le dépôt git. Le message de commit doit être explicite et décrire les modifications apportées aux fichiers. Il est important de bien rédiger le message de commit pour faciliter la compréhension des modifications apportées au projet, mais nous reviendrons sur ce point plus tard, dans la section "Bonnes pratiques". 

* **Afficher l'état du dépôt** `git status`  

Cette commande va permettre d'afficher l'état du dépôt git. Elle va indiquer les fichiers modifiés, les fichiers indexés et les fichiers non suivis. C'est une commande très utile pour savoir où en est le dépôt git.

* **Afficher l'historique des commits** `git log`
Cette commande va permettre d'afficher l'historique des commits du dépôt git. Elle va afficher la liste des commits, avec le hash du commit, l'auteur, la date et le message de commit. C'est une commande très utile pour suivre l'évolution du projet et comprendre les modifications apportées au fil du temps. Pour la rendre plus lisible, il est possible d'ajouter des options :
```bash
    git log --oneline
    git log --graph
    git log --oneline --graph --decorate
```

Parfait, on a maintenant les commandes de bases pour utiliser git LOCALEMENT. Maintenant, on va voir comment interagir avec un dépôt distant (remote). Il faut savoir que git est un outil de gestion de version distribué. Cela signifie que chaque utilisateur a une copie complète du dépôt sur sa machine. Il est donc possible de travailler hors ligne et de synchroniser les modifications avec le dépôt distant plus tard.

* **Ajouter un dépôt distant** `git remote add origin <url_du_remote>`

Vous aurez besoin de cette commande si vous avez créé un répo local et que vous souhaitez le publier sur github. Avant de faire cette commande il faut donc créer le répo sur github.  
"origin est me nom par défaut du remote. Vous pouvez le changer si vous le souhaitez, mais c'est une bonne pratique de garder ce nom par défaut.

Pour s'assurer que le remote a bien été ajouté, vous pouvez utiliser la commande suivante : `git remote -v`. 

* **Pousser les modifications vers le dépôt distant** `git push [origin] [<nom_de_la_branche>]`

Cette commande va permettre de pousser les modifications **Locales** vers le répo **distant**. Mais regardons la commande dans le détail :
* `git push` : Pousse les modifications vers le remote par défaut (origin)
* Ajouter `origin` : Pousse les modifications vers le remote "origin" (si vous avez plusieurs remotes) (ce qui est rare et pas notre cas ici)
* Ajouter `<nom_de_la_branche>` : Pousse les modifications vers la branche spécifiée. Si vous ne spécifiez pas, elle poussera vers la branche en cours. Cependant, il est préférable de toujours se mettre dans la branche sur laquelle vous voulez pousser les modifications avant de faire un `git push` et vous n'utiliserez JAMAIS la commande `git push` pour push une autre branche. (cf bonnes pratiques)
* Lors du premier push, il faut ajouter l'option `-u` pour lier la branche locale à la branche distante. Cela permet de ne pas avoir à spécifier le nom de la branche à chaque fois. Par exemple : `git push -u origin <nom_de_la_branche>`. Il existe un second cas d'utilisation de l'option `-u` mais nous ne l'aborderons pas ici

Je reviendrais sur le concept de branche plus tard, mais sachez que c'est un concept fondamental de git. Il est donc important de bien comprendre comment ça fonctionne et de savoir s'en servir. 

Voyons maintenant comment se tenir à jour par rapport au dépôt distant.

* **Update les informations du dépôt distant** `git fetch --all`

Tout dabord, il faut savoir que git ne synchronise pas automatiquement les informations du dépôt distant et c'est le role de cette commande. Sans vous expliquer en détail pourquoi, sachez que vous n'utiliserez que `git fetch --all`. Elle permet de mettre à jour les infos du dépot distant pour TOUT : branche, commits, tags, etc. Maintenant que le répo est à jour, on va pouvoir récupérer les modifications du dépôt distant et les appliquer à notre répo local. 

* **Récupérer les modifications du dépôt distant** `git pull`

Cette commande va permettre de récupérer les modifications du dépôt distant et de les appliquer à votre répo local. Attention toutefois à plusieurs choses :
* Il faut d'abord faire un `git fetch --all` pour mettre à jour les informations du dépôt distant. Si vous ne le faites pas, vous risquez de récupérer des modifications qui ne sont pas à jour, ou simplement de ne pas récupérer les dernières modifications.
* Aucune modification non indexée ne doit être présente dans le répertoire de travail avant de faire un `git pull`. 
* Si vous tentez un git pull sur une branche qui a des commits non poussés, vous serez confronté à des conflits et nous verrons plus tard comment les résoudre... Donc, le plus possible, évitez.

Bien, vous avez maintenant les commandes de base necessaire pour utiliser git. C'est le stricte minimum pour pouvoir travailler sur le projet CoHoMa dans les secteur "non informatique". Avec ça, vous pourrez :

* Continuer un projet déjà existant
* Créer un nouveau projet
* Ajouter des fichiers
* Modifier des fichiers

Cependant, il y a encore beaucoup de choses à voir sur git, à commencer par... Comment réparer ses erreurs ? (car vous en ferez forcément même si vous êtes très prudents (d'ailleurs, même moi j'en fais (souvent))). 

**<u>III. Les commandes correctives</u>**

On va donc voir comment corriger ses erreurs avec git, du plus simple et local au plus complexe et distant.
La première chose à savoir faire est de savoir annuler les modifications apportées à un fichier. Il y a plusieurs façons de le faire, en fonction de l'état du fichier. **Mais attention, ces commandes *sont destructives* et ne peuvent *pas être annulées*. Il est donc important de bien réfléchir avant de les utiliser.**

* **Annuler les modifications apportées à un fichier indexé** `git checkout -- <nom_du_fichier>`

Cette commande va permettre d'annuler les modifications apportées à un fichier indexé. Elle va remettre le fichier dans l'état dans lequel il était lors du dernier commit. 

* **Annuler les modifications apportées à un fichier non indexé** `git restore <nom_du_fichier>`

Cette commande va permettre d'annuler les modifications apportées à un fichier non indexé. Elle va remettre le fichier dans l'état dans lequel il était lors du dernier commit.

Bien, maintenant que vous savez annuler les modifications apportées à un fichier, on va voir comment desindexer un fichier. C'est à dire comment retirer un fichier de l'index git sans le supprimer du répertoire de travail.

* **Desindexer un fichier** `git restore --staged <nom_du_fichier>`

Cette commande va permettre de retirer un fichier de l'index git sans le supprimer du répertoire de travail. Elle va remettre le fichier dans l'état dans lequel il était au moment de l'indexation. Tips suplémentaire, si vous souhaitez desindexer et annuler les modifications apportées à un fichier, il est possible d'utiliser la commande `git reset HEAD <nom_du_fichier>`. 

Ca me fait une super transition pour la commande suivante qui permet, elle, de remettre le répo dans létat d'un commit précédent.

* **Remettre le répo dans l'état d'un commit précédent** `git reset --soft <hash_du_commit | HEAD~X >`

J'appuie là dessus car il ne faut pas se tromper sur le rôle de cette commande : elle permet de revenir en arrière dans l'historique des commits mais ***NAFFECTE PAS*** l'historique des commits.  
En gros, il faut voir le versionning comme une tete de lecture sur une bande (HEAD) et que chaque commit est un point sur cette bande. Lorsqu'on a recourt à la commande `git reset`, on deplace la tête de lecture sur un commit précédent.   
Ce déplacement peut être destructif ou non destructif ET il peut affecter le répertoire de travail ou non. Une fois la tête de lecture déplacée, toutes les commandes git affectant le répo (`git commit` par exemple) auront lieu à partir de ce commit. Il est donc important de bien réfléchir avant de l'utiliser.

Voyons la commande dans le détail :
* `git reset` : Remet le répo dans l'état du commit spécifié
* `--soft ` : Remet le répo dans l'état du commit spécifié et garde les modifications apportées depuis ce commit. C'est à dire que les fichiers modifiés seront toujours présents dans le répertoire de travail et indexés. C'est une commande non destructrice et il est possible de revenir en arrière. Cependant, on y a rarement recours.

* `<hash_du_commit>` : Hash du commit sur lequel vous voulez revenir. Il est possible de le trouver en faisant un `git log` et en copiant le hash du commit souhaité
* `HEAD~X` : Permet de revenir en arrière de X commits par rapport à la tête. Par exemple, `HEAD~2` permet de revenir en arrière de 2 commits par rapport à la tête. Il est possible d'utiliser `HEAD^` pour revenir au commit parent de la tête, mais c'est un peu plus compliqué à expliquer et très peu utilisé donc je ne vais pas m'étendre là-dessus.

Maintenant que vous savez comment revenir en arrière dans l'historique des commits, on va voir comment renommer et supprimer ou revenir en arrière sur un commit. Commencons par le plus simple : renommer un commit.

* **Renommer un commit** `git commit --amend -m "<nouveau_message_de_commit>"`

Cette commande renomme le dernier commit... Mais attention, elle modifie l'historique de commit, alors cette opération n'est possible que ***si le commit n'a pas été poussé sur le dépôt distant***. Dans le cas contraire, nous verrons dans un instant comment le faire, mais il faut vraiment éviter d'en arriver là.

* **revenir en arrière sur un commit** `git revert <hash_du_commit>`

Cette commande créer un nouveau commit qui annule les modifications apportées par le commit spécifié. Donc aucun souci si le commit a été poussé sur le dépôt distant, car on ne modifie pas l'historique des commits, on l'étend. Ce n'est pas une commande qu'on utilise souvent, mais il est utile de la connaitre et son utilisation sera expliquée dans la section "Bonnes pratiques".

* **Supprimer un commit** `git reset --hard <hash_du_commit | HEAD~X>`

Cette commande ci est destructrice et affecte le répertoire de travail ainsi que l'historique des commits. Elle remet le répo dans l'état du commit spécifié et supprime tous les commits suivants. Il est donc impossible de revenir en arrière une fois la commande exécutée. Il faut donc vraiment réfléchir avant de l'utiliser. Une fois fait, les commits que vous ajouterez seront ajoutés à la suite. ATTENTION : Si vous avez déjà poussé le commit sur le dépôt distant, vous aurez un problème et vous ne pourrez plus push normalement, donc faites bien attention.

C'est la que les dernières commandes interviennent. Elles auront beaucoup de conséquences pout vos collaborateurs, donc il faut vraiment informer les autres membres de l'équipe si ça doit arriver : on s'attaque à la correction d'erreur sur le répo distant.

* **Modifier l'historique des commits poussé** `git push --force`

C'est le dernier recours. Cette commande va permettre de forcer le nouvel historique des commits sur le dépôt distant en ecrasant l'historique des commits précédents. Faire ça est très risqué et il faut vraiment être sur de ce qu'on fait. 

Maintenant, vous savez comment corriger la majorité des erreurs que vous pourrez rencontrer sur git. Avec ces outils, vous devriez plutôt bien vous en sortir et pouvez être confiant quant à votre capacité à interagir avec les projets. 


Cependant, pour que nous puissions à plusieurs sur un projet, il faut savoir comment gérer les branches et les conflits. C'est un concept fondamental de git et très utile pour travailler en équipe. 



**<u>IV. Les commandes de gestion de branches et des conflits</u>**

**<u>V. Les commandes de fusion</u>**

**<u>VI. Les bonnes pratiques (OBLIGATOIRES)</u>**



**<u>A. Rappel des commandes</u>**

**<u>B. Rappel des bonnes pratiques</u>**