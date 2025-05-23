# GIT

<u>**I. Le setup de git**</u>

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

**<u>III. Les commandes correctives</u>**

**<u>IV. Les commandes de gestion de branches</u>**

**<u>V. Les commandes de fusion</u>**

**<u>VI. Les bonnes pratiques (OBLIGATOIRES)</u>**



**<u>A. Rappel des commandes</u>**

**<u>B. Rappel des bonnes pratiques</u>**