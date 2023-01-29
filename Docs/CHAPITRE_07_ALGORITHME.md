# CHAPITRE 07 – Projet – Algorithme & Code


> **Contenu:**
> - Python: `__debug__`
> - Programmation: Algorithmie
> - Projet: split_filename
> - Python: Documentation

## 0. Debug

Quand on écrit un programme, on veut parfois voir ce qui se passe à l’intérieur du programme lorsqu'il exécute. Des fois pour comprendre comment il fonctionne et souvent pour comprendre pourquoi il ne fonctionne pas! À ces moments on imprime à l’écran des variables pour voir leurs valeurs. La bonne façon de faire ça, en python, est la suivante.

```PYTHON
if __debug__:
    print(f‘variable = {variable}’)
```

Pourquoi? Parce qu’un jour tu auras fini ton programme (et oui!) et tu seras prêt à le livrer. Ce jour-là, tu vas compiler ton programme avec les options d’optimisations de python (`python –OO programme.py`) et toutes les lignes qui contiennent ces instructions ne seront pas compilées. Comme si elles n’avaient jamais été écrites. Donc tu n’auras pas à revisiter ton code et à enlever ces lignes.

L’autre avantage énorme est que si un jour tu as un problème dans ton code tu peux y retourner et toutes ces lignes de débug seront présentes pour t’aider à nouveau.

C’est tellement important que j’ai automatisé cette écriture dans PyCharm. J’ai arrangé des options de PyChrarm pour que si je tape ‘ifd’ suivi de la clé ‘tab’, PyCharm écrit pour moi tout le texte du code (sauf le nom de la variable). Je vais regarder si je peux t’envoyer ce ‘settings’ dans un fichier.

## 1. Le Code

### 1.1 Par Où Commencer?

Alors on revient à ton diagramme de design et on veut commencer à programmer. Où commence-t-on?

Par exemple, on peut commencer par le modèle. C’est là que le programme fait la vraie job. On pourrait aussi commencer par l’interface. L’avantage de commencer par l’interface c’est que tu peux voir de quoi le programme va avoir l’air, visuellement, avant de coder toute l’intelligence en arrière.

Si ton programme avait beaucoup d’intelligence d’affaire à coder on pourrait même commencer par le contrôleur. L’autre avantage de ce type de design (Model-View-Controller) c’est qu’une personne (ou une équipe) peu commencer sur l’interface pendant qu’une autre travaille sur le modèle et une autre sur le contrôleur.

Comme l’interface, dans ton cas, est un bloc monolithique (un seul ‘écran’) et que le modèle est une collection de plus petites fonctions facilement séparables et indépendantes on va commencer par le modèle, pour pouvoir prendre de plus petites bouchées à la fois.

Alors on en choisit un bloc du modèle écrit son algorithme: Prenons db_to_csv

### 1.1 Diviser Le Problème

On écrit ou on pense le problème en algorithme simple:

#### ALGORITHME A: Convertir un fichier db en un fichier xls

- Requis:
  - Écrire un fichier CSV qui contient la même information que la table d’un fichier sqlite DB
  - Le nom du fichier destination doit ‘ressembler’ au fichier source (DB)

```
1. A partir d’un fichier db existant (fichier source).
2. Créer un nom de fichier (fichier destination) il doit
    2.1 Ressembler au fichier source.
    2.2 Être unique
    2.3 Avoir l’extension appropriée
3. Convertir la table du fichier source db en format csv.
4. Sauvegarder les données en format csv dans le fichier destination.
```
Donc réalisons l‘algorithme A

- Étape 1: «à partir d’un fichier db existant (fichier source)»

Rien à faire ici. On sait que l’interface ou le contrôleur vont nous fournir un nom de fichier source.

- Étape 2: créer un nom de fichier (fichier destination).

Il y a beaucoup de requis et tout ça a l’air complexe alors on va se faire un nouvel algorithme. __Nous allons diviser ppour régner!__ Juste pour cette partie.

#### ALGORITHME B: créer un nom de fichier (fichier destination)

Requis:
- On veut un nouveau nom de fichier qui ressemble au nom du fichiersource.
- Le nom de fichier destination aura une extension différente. Cettefois-ci c’est ‘.csv’ mais il y en aura d’autres avec d’autres extensions plus tard.

- le nom du fichier destination ne doit pas exister sur le disque
 - Le fichier destination doit être dans le même répertoire que le fichier source.
- Décision: Depuis le début on dit que le nom du fichier destination doit ressembler au nom de fichier source et qu’il doit être unique. Alors ici on prend la décision:
    - Le nom de fichier destination aura le même répertoire que lefichier source.
    - Le nom du fichier lui-même sera le même que le fichier sourceavec en plus le suffixe ‘_nn’ ou nn est un numéro séquentielcommençant à 01et terminant à 99.
    - Et l’extension sera celle demandée pour le format du fichier destination.


__ALGORITHME B__
```
1. Extraire les composant du nom de fichier source (répertoire, nom, extension (sans le point))
2. Répète:
        2.1. Ajoute ‘_nn’ au nom de fichiers (commence à ‘_01’)
        2.2. Ajoute l’extension du fichier destination au nom de fichier
        2.3. Ajoute le répertoire au début du nom de fichier.
        2.4. Si le nom de fichier n’existe pas sur le disque
            2.4.1. Quitte la boucle ‘Répète’
3. Nous avons le nom du fichier destination.
```

L’algorithme B est très complexe et assez long. Prenons le premier morceau:
```
«Extraire les composant du nom de fichier source (répertoire, nom, extension (sans le point)):»
```
OK! Bingo! Ça c’est assez petit pour être codé directement. On va écrire le code pour ça.

Ce que l’on va coder est l’étape 1 de l’algorithme B qui lui est l’étape 2 de l’algorithme A.

Encore une fois on a __DIVISER POUR RÉGNER__. On a maintenant un tout petit problème à régler et on peut oublier tout le reste et se concentrer là-dessus.

NOTE IMPORTANTE SUR LA RÉALITÉ: J’ai fait tout le processus précédent mentalement sans rien écrire et pas nécessairement de façon linéaire. J’ai presque tout de suite compris que je devais briser le nom du fichier source en ses composantes. J’ai eu une vague idée du suffixe nécessaire ‘_nn’ et du processus pour vérifier son existence. Mais j’ai laissé ça de côté pour me concentrer sur le code de la séparation du nom de fichier source.

### 1.2 Coder Une Partie du problème

#### 1.2.1 Recherche

Maintenant nous devons écrire une fonction en Python qui sépare un nom de fichier en ses composantes. Allons voir ce que python a à offrir. J’ouvre mon browser internet et je vais sur le site de la documentation de python 3.8: https://docs.python.org/3.8/contents.html

Dans la boite de recherche en haut a droite je rentre «split filename into components»

Pour ça je reçois une centaine de résultats et je regarde rapidement les titres de chacun. Les 5 premiers ne ressemblent pas à mon problème. Le sixième dit: os.path — Common pathname manipulations.

Ça ressemble à mon problème. Et en plus je viens d’apprendre que le mot ‘pathname’ est plus descriptif de ce que je recherche. Alors je navigue à os.path. Il y a un paragraphe descriptif que je lis et par la suite un encadré en jaune qui dit:
> «See also: The pathlib module offers high-level path objects».

Cela semble très intéressant parce que plus c’est «high-level» moins il y a de détails à manipuler. Je clique sur pathlib.

Ça semble vraiment complexe tout ça. Y’a un diagramme et une phrase en dessous qui dit:
> If you’ve never used this module before or just aren’t sure which class is right for your task, Path is most likely what you need. ….

Bon  on va utiliser Path mais est-ce que ça fait ce que j’ai besoin? Allons voir sur le reste des internets: dans google on rentre «python use pathlib to split pathname»  Tout ce qui parle de os.path ne m’intéresse pas puisque je veux Pathlib. Le 4ᵉ choix est:
> «Python 3's pathlib Module: Taming the File System»

Et c’est un lien de RealPython.com un bon site qui donne habituellement d’excellentes réponses (l’expérience m’a appris ca!). Alors j’y vais!
https://realpython.com/python-pathlib/

Sur le site de RealPython.com je scroll rapidement les grands titres de chaque section et je m’arrête sur:
>«Picking Out Components of a Path».

Y’a plusieurs exemples et c’est exactement ce dont j’ai besoin. Ça y est, j’ai trouvé le code à utiliser. Donc en suivant les exemples j’écris le petit programme suivant:

#### 1.2.1 Test de l’information découvertes
```PYTHON
    from pathlib import Path
    pfn = Path('e:/source/cnv/testfiles/test.db')
    print (f"repertoire:{pfn.parent}")
    print (f"nom de fichier:{pfn.stem}")
    print (f"Extension:{pfn.suffix}")
```

Qui produit l'output suivant:

```
repertoire:e:\source\cnv\testfiles
nom de fichier:test
Extension:.db
```

Et je vois que tout fonctionne correctement. Sauf le fait que l’extension vient avec le point il faudra régler ça. Pour le faire je vais dans ma boite à outils (mon cerveau avec son expérience!) et je sais que le découpage des séquences peut facilement m’aider à le faire (le découpage est expliqué dans une des prochaines pages). Alors je corrige mon petit programme comme suit:

```PTYHON
    from pathlib import Path
    pfn = Path('c:/source/cnv/testfiles/test.db')
    print (f"repertoire:{pfn.parent}")
    print (f"nom de fichier:{pfn.stem}")
    print (f"Extension:{pfn.suffix[1:]}")
```

Et j'obtiens l'output suivant:

```
repertoire:c:\source\cnv\testfiles
nom de fichier:test
Extension:db
```

OK je suis correcte je peux maintenant passer à l’écriture de mon module.

NOTE IMPORTANTE SUR LA RÉALITÉ: Ma boite à outils contenait déjà la connaissance de pathlib et de Path, mais j’ai refait le processus de recherche pour te montrer ce que c’est. Le grand danger d’internet c’est la quantité de vieilles affaire qui y traînent. Tout le monde dit d’utiliser os.path, mais os.path est la vielle solution qui existe depuis la nuit des temps alors il y a beaucoup d’information là-dessus. Pathlib est la solution moderne qui existe seulement depuis Python 3.4 et encore peu de choses ont été écrites à son sujet. Dans ce cas-ci, la bonne solution est plus difficile à trouver que la mauvaise! Comment on fait pour savoir que pathlib est la bonne solution? On lit des livres ou on connaît quelqu’un qui l’a déjà dans sa boite a outils!

### 1.3 Création Module

Donc je suis prêt créer mon module. Il faut que je lui trouve un nom. Un bon nom. Je peux l’appeler modele car c’est le niveau modele du design de mon application, mais dans ce cas tous les modules pour le reste de ma vie s’appelleront modele! Ce module contiendra les fonctions de conversion de fichiers, ces fichiers seront transformés d’un format à un autre, alors je l’appellerai:

> file_transform.py

Dans PyCharm, avec notre projet ‘cnv’ ouvert, on vas dans le menu `File`, `option New`, et dans le menu tu choisis `Python File` (attention ce n’est pas toujours la première option), et finalement tu rentres le nom du fichier: `file_transform_v1.py` et tu fais `enter`.

On est maintenant dans un nouveau module et on peux copier le code suivant:
```PYTHON
from pathlib import Path

def split_filename(filename):
    """
    Extrait les morceaux d'un nom de fichier
    :param filename: le nom de fichier choisi par l'usager
    :return: tuple de strings:les morceaux du nom de fichier dans cet ordre:
                    le prefix (drive and directories),
                    le nom de fichier lui meme sans extension
                    l'extension sans le point '.'
    """
    pfn = Path(filename)
    return pfn.parent, pfn.stem, pfn.suffix[1:]
```

### 1.4 Détail Du Code

Allons-y ligne par ligne. C'EST LA SEULE FAÇON DE BIEN COMPRENDRE UN PROGRAMME!

> from pathlib import Path

Importe de la librairie (module) pathlib l’objet Path. En important seulement l’objet Path je peux le référencer directement dans mon programme je n’aurai pas besoin de le précéder du nom du module. Si j’avais écrit: `import pathlib` Il aurait fallu référencer Path en écrivant (par exemple dans le cas de l’attribut ‘parent’): `pathlib.Path.parent` qui signifie: `MODULE●OBJET_DANS_LE_MODULE●ATTRIBUT_DE_L_OBJET`.

Mais comme j’ai juste besoin de l’objet Path je l’importe directement par son nom et j’y fais aussi référence de la même manière.

Autres avantages: mon code exécute plus rapidement et il est plus petit. Puisque je n’ai pas tous le module à importer.

> def split_filename(filename):

La déclaration de notre fonction. Le mot clé `def` annonce au compilateur que le texte qui suit est une fonction. `split_filename` est le nom de la fonction. C’est un très bon nom. C’est un verbe (split) suivi du nom d’une chose sur laquelle ce verbe agit (filename). Il n’y a aucun doute sur ce que fait cette fonction. Entre parenthèses nous retrouvons les paramètres que cette fonction recevra lors de son appel. Dans notre cas il n’y en a qu’un seul: une chaîne de caractères ET ON ASSUME QUE CETTE CHAÎNE DE CARACTÈRES EST UN NOM DE FICHIER.

```
    """
    Extrait les morceaux d'un nom de fichier
    :param filename: le nom de fichier choisi par l'usager
    :return tuple de strings:les morceaux du nom de fichier dans cet ordre:
                    le prefix (drive and directories),
                    le nom de fichier lui meme sans extension
                    l'extension sans le point '.'
    """
```

C’est la documentation de notre fonction, appelée: `‘DOCSTRING’`. C’est sans doute le morceau le plus important. __Note que cette documentation se trouve directement sous la déclaration de notre fonction, la ligne suivant notre déclaration__. Pas deux ou trois lignes après, tout de suite après. C’est grâce à cette syntaxe (ligne suivante) que c’est une documentation. Si la même chaîne de caractères se trouvait 2 lignes après la déclaration le compilateur ne reconnaîtrait pas cette chaîne comme étant la documentation.

Séparer un nom de fichier en ses composantes est une fonctionnalité dont tu auras besoin des dizaines de fois dans ta vie de programmeur. Si elle est bien documenter tu n’auras jamais à la ré-écrire. En fait la documentation est tellement importante que je lui dédie une page complète dans les pages suivantes.

```Python
    pfn = Path(filename)
```

La première ligne de notre fonction. Elle est décalée vers la droite de 4 espaces pour montrer qu’elle appartient à la fonction `split_filename`. `Path(filename)` crée un objet Path à partir du nom de fichier `filename`.

Créer un objet Path se dit comme suit: _Instancie un objet avec la classe Path avec le paramètre `filename`_. Une fois cet objet instancié on le met dans la variable 'pfn'. 'pfn’ n’est pas un bon nom de variable c’est trop court et la vraie définition de cette variable est path_filename. Mais je me le permets parce que cette variable est utilisée une seule autre fois dans la ligne suivante.

À la fin de l’exécution de cette ligne nous avons un objet de la classe Path dans notre variable pfn.

```python
    return pfn.parent, pfn.stem, pfn.suffix[1:]
```

La dernière ligne est complexe et fait beaucoup de chose en même temps.

Mais elle très pythonic et ‘relativement’ facile a comprendre. Cette ligne de code est, elle aussi, décalée vers la droite de 4 espaces pour montrer qu’elle appartient à la fonction `split_filename`.

Donc on fait un `return` qui signifie que la fonction terminera. Ce `return` est suivis de 3 variables qui signifie que ces 3 variables seront retournées par la fonction. Ce qui implique que le code qui appellera `split_filename` aura accès aux valeurs de ces variables.

> pfn.parent

Est la valeur de l'attribut `parent` de l'objet `pfn` de la classe `Path`.

Et selon la documentation il contient __un objet de classe Path__ qui est le répertoire complet, sans le nom de fichier et sans l’extension, de la variable ‘filename’ avec lequel cet objet fut crée.

> pfn.stem

Est la valeur de l'attribut 'stem' de l'objet pfn de la classe Path. Et selon la documentation il contient une chaîne de caractères qui est le nom de fichier (sans repertoire et sans extension) de la variable ‘filename’ avec lequel cet objet fut crée.

> pfn.suffix

Est la valeur de l'attribut `suffix` de l'objet `pfn` de la classe `Path`. Et selon la documentation il contient une chaîne de caractères qui est l’extension (avec le point) de la variable ‘filename’ avec lequel cet objet fut crée.

> pfn.suffix[1:]

On sait que pfn.suffix est une chaîne de caractères. Comme les listes et les tuples, les chaînes de caractères sont des séquences comme toutes les séquences elles supportent la fonctionnalité de découpage. Le découpage [1:] est un classique qui retourne une nouvelle chaîne de caractères comprenant tous les caractères de la chaîne originale SANS LE PREMIER CARACTÈRE.
Donc on a l’extension de `filename` sans le point.

```python
    pfn.parent, pfn.stem, pfn.suffix[1:]
```

Ces trois variables sont séparées par des virgules. Lorsque des variables ou des valeurs sont séparées par des virgules elles deviennent automatiquement un TUPLE. Donc notre programme retourne un tuple contenant ces trois valeurs, comme indiqué dans la documentation.

C’est la fin de notre fonction de 2 lignes!

### 1.5 Tester Code

Nous reviendrons beaucoup plus en détail sur les test, mais en attendant nous voulons quand mêne verifier que notre fonction exécute correctement.

Ajoutons une fonction main à notre module pour pouvoir le tester. Notre module complet devient donc:

```python
from pathlib import Path

def split_filename(filename):
    """
    Extrait les morceaux d'un nom de fichier
    :param filename: le nom de fichier choisi par l'usager
    :return: tuple de strings:les morceaux du nom de fichier dans cet ordre:
                    le prefix (drive and directories),
                    le nom de fichier lui meme sans extension
                    l'extension sans le point '.'
    """
    pfn = Path(filename)
    return pfn.parent, pfn.stem, pfn.suffix[1:]

def main():
    testfilename = "e:/conv/testfiles/cf.db"
    p,n,e = spit_filename(testfilename)
    print(f"split_filename pour {testfilename}")
    print(f"Repertoire parent = {p}")
    print(f"Nom de fichier    = {n}")
    print(f"Extension         = {e})

if __name__ == '__main__':
    main
```

__Petite parenthèse sur l’objet Path du module pathlib__

Path est le seul objet de toutes les librairies python qui utilise une lettre majuscule. La raison est que quand ils ont développé la librairie pathlib (lors de la version 3.4) ils se sont rendu compte qu’il y avait déjà des millions de lignes de code, écrites par les programmeurs python partout à travers le monde, qui contenait une variable qui s’appelait ‘path’ (parce que c’est très courant de manipuler un ‘path’). Alors plutôt que d’obliger des milliers de programmeurs à ré-écrire des millions de lignes de code, ils ont nommé l’objet ‘Path’ avec une lettre majuscule. Y’a une leçon là-dedans: Il ne faut pas utiliser de lettres majuscules dans les noms de variables de nos programmes en python!

## 2. DOCUMENTATION

> EN PYTHON, TOUT EST UN OBJET.

Bien que nous essayerons le moins possible d’aller vers la programmation par objets, pour te laisser le temps de digérer le matériel avant de trop en mettre et de t’étouffer, puisque tout en python est objet tu devras t’y frotter un peu.

Donc les listes, les tuples, les dictionnaires et tous les autres types, même les petits entiers (int) sont des objets. Même les fonctions que tu écris sont des objets. Chaque variable que tu utilises est un objet. Les classes que tu utilises pour instancier les objets sont des eux-mêmes des objets. S’en est étourdissant!

La preuve c’est qu’au lieu de coder `x=3` tu peux très bien `coder x = int(3)` qui ce lit comme suit: utilise la classe `int` pour créer un objet de type `int` (integer) avec la valeur 3 et mets cet objet dans le conteneur appelé `x`.

La 2ième preuve: écrit le programme suivant (2 lignes dans un scratch) et regarde le résultat!

```python
print(int)
print(str)
```

Alors c’est quoi un objet? Un objet c’est l’instanciation d’une classe.

Alors c’est quoi une classe? Une classe c’est la définition d’un TYPE d’objet.

Cette définition contient des variables (appelées attributs) et des fonctions (appelées méthodes) qui agissent sur les attributs.

On va arrêter là pour la programmation par objets on en a assez pour faire ce qu’on a à faire.

TOUS les objets en python ont certains attributs (des variables définies dans leur classe) communs. Ils ont tous un attribut `__doc__` qui contient la documentation de l’objet et un attribut `__class__` qui contient le nom de la classe a partir de laquelle ils ont été instanciés (le nom de leur type).

Donc tu peux faire et voir ce que le programme imprime à l’écran.

``` python
x=3
print(x.__class_)
print(x.__class__.__name__)
print(x.__doc__)
```

Si tu veux voir quelque chose de très intéressant écrit le code suivant:

``` python
from pathlib import Path
print(Path.__doc__)
```

Eh oui! La documentation de Path est à l’intérieur du code de Path?!?! On n'a pas le code source de Path, mais on peut voir la documentation de cet objet. N’est-ce pas merveilleux. Prépare-toi à sursauté! Dans notre module `file_transform.py` ajoutes les 2 lignes suivantes à la fin et complètement accotée à gauche:

```python
print(split_filename.__class__.__name__)
print(split_filename.__doc__)```
```

Exécute notre module! Merveilleux n'est-ce pas!


