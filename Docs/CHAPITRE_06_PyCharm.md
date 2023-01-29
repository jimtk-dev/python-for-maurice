# CHAPITRE 06 PYCHARM

>**Contenu:**
>- Programmation – Contrôle des versions
>- Python - Setup PyCharm
>- Python - Les Scratchs.

Malheureusement avant de réellement commencer il faut faire ce que j’appelle la petite cuisine. Ça nous prend un comptoir, des bols, des fourchettes, une spatule, un four, des ronds de poêle, etc, etc. Une fois qu’on aura ça on peut faire à manger.

Cette étape est importante pour nous permettre de bien travailler et de garder un environnement propre dans lequel nous pourrons travailler sans nous enfarger dans les fichiers inutiles et permettra à l’outil (PyCharm) de comprendre exactement quels fichiers font partie du programme et lesquels ne le sont pas. Ce sera très important à la fin lorsque nous transformerons notre programme python en un vrai programme (.exe) que nous pouvons lancer à partir d’une icône sur le desktop de Windows™.


## 0.  Gestion Versions.

Il existe plusieurs outils de contrôle des versions (version control) tous plus resplendissants les un que les autres: subversion, cvs, et le plus populaire et le plus utilisé sur la planète: Git et Github.

Malheureusement ces applications sont beaucoup trop puissantes pour nous. Elles permettent à des équipes nombreuses de travailler sur le même code en même temps et d’importer ces changements dans des versions précédentes du code.

Pour nos besoins nous adopterons simplement une discipline de gestion des noms de fichier.

### Méthode de travail

1. On écrit un petit bout de code dans un module que l’on sauve avec le suffixe _v1 (ex: module_v1.py)
2. On teste le code de la version v1.
3. Quand tous les tests sont concluants et qu’on est certain que lepetit bout de code fonctionne bien.
4.  On incrémente le numéro de version et on sauve le fichier(module_v2.py). Attention on fait ça avant d’ajouter du nouveau code
5.  On écrit un autre petit bout de code et on le teste. Une fois la version _v2 est testée avec succès on crée le module_v3.py.
6.  Ainsi de suite jusqu’à ce que le module soit complet et testé. À ce moment on enlève le suffixe de version et on sauve le module sous son nom sans suffixe de version (module.py).
7.  On fait une sauvegarde (backup) de toutes les versions, de la documentation, et des fichiers de test et on recommence sur un autre module. Cette sauvegarde peut-être aussi simple qu’un fichier‘zip’  placé dans un répertoire backup. Par la suite on efface tousles modules qui ont un suffixe _vn.
8.  Si le module ‘module.py’ doit être modifié plus tard on fait une copie et on recommence à ajouter le suffixe au nombre suivant ou on était la dernière fois (ex: module_v9.py).

## 1.  PyCharm

### Créer Un Projet.

Comme on utilise PyCharm tous les deux (Dieu merci!) il faut savoir s’en servir. Nous allons faire table rase et partir un nouveau projet!

Note Importante: Pour faciliter grandement le travail, ce serait bien que nos répertoires de projets soit alignés (mème disque, mème nom de répertoire). Je propose d:\source\cnv . Si pour quelques raisons techniques tu ne peux pas mettre le projet à cet endroit, laisse-moi savoir ce que tu choisis et je m’enlignerai pour que ça marche. Évidemment Il n’est pas une bonne idée d’utiliser le disque ‘C:’

Alors démarre PyCharm, si tu as un projet d’ouvert fermes le (File → Close Project),  et click sur ‘New Project’ en haut a droite. Et tu arrives à l’écran suivant.

### PyCharm: Nouveau Projet

<p align="center">
    <img src="Assets\Pycharm-New-Projects-commented.png">
</p>

A. Le répertoire ou résidera le code et l’environnement. J’essaie de garder ça assez court et près du ‘Top Level’, mais je m’assure toujours que le nom est significatif. Voir note importante ci-bas

B. L’outil avec lequel l’environnent sera créé. On utilise venv parce qu’il est simple et suffisant pour nos besoins.

C Le répertoire ou Pycharm créera l’environnement virtuel, là ou les libraires externes résideront.

D. Une copie de cet interpréteur sera placée dans notre environnement. Si tu en as plusieurs d’installés sur ta machine choisis le bon. Dans notre cas ce sera l’installation originale de la version 3.8.

E & F. Ne doivent pas être sélectionnés. Tout le reste ne doit pas être sélectionné.

Finalement Appuis sur ‘Create’

### Répertoires Satellites

Une fois le projet démarré il nous reste à ajouter les répertoires nécessaires pour bien travailler. Nous allons le faire à l’intérieur de PyCharm en utilisant la fenêtre de projet.

Dans PyCharm par le menu View → Tool Windows → Project ou (comme un pro) par le clavier ‘alt’+’1’. Ce sont des switch on/off alors si la fenêtre disparaît, refait les instructions pour qu’elle apparaisse. Dans cette fenêtre tu vas cliquer avec le bouton de droite de la souris là ou est le top répertoire (voir image)

<p align="center">
    <img src="Assets\Pycharm-newDirectory.PNG">
</p>

Lorsque tu cliques à droite sur le répertoire du dessus, il t’apparaîtra un menu, glisses la souris sur la première option (‘NEW’).
Il t’apparaîtra un autre menu dans lequel tu choisis ‘DIRECTORY’.

Enfin il t’apparaîtra une toute petite fenêtre pour entrer un nom de répertoire. Écrits ‘Docs’ (sans les guillemets) et appui sur Enter.
Refait tout ça une deuxième fois et crée un autre répertoire du nom de ‘testfiles’

Refait tout ça une 3ᵉ fois et crée un répertoire du nom de ‘Backup’

### Exclusion des Répertoires

Après avoir créé ces répertoires il faut maintenant expliquer a PyCharm que ces répertoires ne sont pas du code et qu’il ne faut pas qu’ils les incluent dans la distribution finale du programme. Pour ce faire on marque ces répertoires comme étant exclus (‘Excluded’).

Dans la fenêtre du projet (project window) place la souris sur le nom du répertoire Docs (que tu viens de créer) et clique sur le bouton de droite. Il apparaîtra un menu qui a la fin offre l’option ‘Mark Directory as…’, glisses-y ta souris et un petit menu te permettra de choisir l’option ‘Excluded’. Dans la ‘Project window’ la petite image du dossier à côté du nom du répertoire changera de couleur (dans mon cas rouge).

Refait ça pour les répertoires ‘testfiles’ et ‘backup’. À la fin ta fenêtre de projet devrait ressembler a ça:

<p align="center">
    <img src="Assets\final_directories.PNG">
</p>

ON EST PRÊT À CODER!

Ne t’en fait pas si tu te trompes. On peut facilement tout effacer et recommencer.

### En Cas d'Erreur

Si c’est le cas. Ferme le projet (File→ Close Project,  dans la fenêtre de pycharm qui contient la sélection de projets, sélecte le projet et en cliquant sur le bouton de droite et choisi l’option ‘Remove from recents project  Delete’). Une fois que c’est fait, va dans ‘windows explorer’  navigue au répertoire du projet (d:/source) et efface ‘delete’ le répertoire cnv.
ET recommence l’exercice!

## ADDENDUM: Méthode de travail

Tout au cours de l’exercice qu’on entreprend et dans les nombreux emails que nous échangerons je te dirai souvent: «Écrit le programme suivant et roules le». La technique d’écrire des petits programmes pour vérifier une solution, s’assurer que le découpage d’une liste est correct ou qu’une méthode fonctionne comme tu penses est très courante. En fait cette méthode de travail porte fruits parce qu’elle permet au programmeur de découvrir par lui-même le fonctionnement des choses et quand on apprend de cette façon ça le fixe en mémoire (et dans notre boite a outils) de façon très solide. On a rien inventé ici: c’est en programmant qu’on apprend à programmer!.

Cette méthode est tellement courante que PyCharm a intégré cette façon de faire efficacement. Quand on écrit ce genre de petits programme, comme sur un papier brouillon, on ne veut pas avoir à le nommer, à le gérer dans notre environnement ou dans notre espace de travail ou a le sauver quelque part. Pycharm s’occupe de toute cette cuisine pour toi avec les ‘SCRATCH’

### Fichiers 'Scratch'

- Va dans le menu File → New Scratch File
- Choisi Python dans la fenêtre des choix.

Aussitôt Pycharm t’ouvres une fenêtre programme avec un nouveau nom (Scratch01.py).Tu peux y écrire ton programme' le rouler (Shift-F10 ou bouton de droite→ Run), regarder l’output, le modifier, le re-rouler et tester tout ça pendant des jours si tu le veux. Une fois que tu es satisfait tu peux copier le code qui t’intéresse (si il y en a) dans ton module important et fermer la fenêtre du scratch. Il est disparu! Il n’est pas dans ton environnement, il ne t’ennuie pas et si jamais tu veux le revisiter, tu peux le retrouver profondément dans l’espace de PyCharm dans

```
C:\Users\{username}\AppData\Roaming\JetBrains\PyCharmCE2021.2\scratches\scratch_01.py
```

Pour donner un exemple. Afin d’écrire les documents que j’envoies, je vérifie chaque petit morceau de code dans PyCharm pour m’assurer que ça roule sans erreur. Je suis rendu à Scratch_143.py (c’est 143 petits programmes!)
