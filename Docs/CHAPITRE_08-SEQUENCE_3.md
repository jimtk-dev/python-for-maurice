# CHAPITRE 08: SEQUENCE 3

> **Contenu:**
> - Python: La compréhension

## 0. Révision Mathématiques

N’aie pas peur c’est très simple et c’est surtout pour assurer que le vocabulaire est bien en place.

<p align="center">
    <img src="Assets\exposants.png">
</p>

On dit que 16 est une puissance de 2. C’est la quatrième. 2<sup>4</sup> se lit: 2 exposant 4.

## 1. COMPRÉHENSION DE LISTE

> ***NOTE***: Nous utilisons le mot liste au sens large, car la compréhension de liste s’applique à toutes les séquences: list, string, tuple, dictionnary et autres.

> ***AUTRE NOTE***: Comme le découpage, la compréhension de liste peu devenir un charabia difficile à comprendre et l’on ne doit pas l’utiliser à outrance. Évidemment ce qui est un charabia pour un débutant peut être quelque chose de facilement compréhensible pour un expert. Le niveau d’outrance varie avec l’expérience!

### 1.1  Complexité 0

En python la compréhension de liste (list comprehension) est une technique de programmation qui permet de grandement réduire l’effort du traitement des membres d’une liste.

Voici comment ce traitement est habituellement fait:

```python
# programme qui imprime une liste des carrées des nombres de 1 a 20
entiers = list(range(1,21))  # une liste d’entier de 1 a 20
resultats = []               # une liste vide
for entier in entiers:
    resultats.append(entier**2)
print(resultats)
```

Ce genre de traitement d’items de liste (ou de tuple, string, etc) est si souvent nécessaire qu’ils ont construit une façon plus simple de l’écrire: La compréhension de liste. Voici l’exemple du code précédent écrit avec cette technique:

```python
# programme qui imprime une liste des carrées des nombres de 1 a 20
resultats = [nombre**2 for nombre in range(1,21)]
print(resultats)
```

OK, étudions la ligne

```python
[nombre**2 for nombre in range(1,21)]
```

Le premier et le dernier caractères sont des crochets (‘ [ ] ‘) cela signifie que le résultat sera une liste. Si on avait mis, par exemple, des parenthèses le résultat eut été un tuple.

Le groupe `nombre**2` représente le traitement qui sera fait à chaque item de la séquence source et le résultat de ce traitement sera placé dans la liste finale. Notes que nous avons appelé l’item source ‘nombre’, nous aurions pu lui donner un tout autre nom à notre guise.

Finalement nous avons une boucle `for`,  qui nous fournis des valeurs d’entiers en itérant sur un itérateur `range(1,21)`. Ceci est notre séquence source. Nous avons pu ainsi nous débarrasser de la liste intermédiaire ‘entiers’ du programme précédent. Notes que nous aurions pu la garder bien que ce ne soit pas de bonne manière si elle n’a pas d’autres utilisations dans notre programme. En voici l’exemple (nous avons aussi modifié le nom de la variable 'nombre’ pour démonstration)

```python
# programme qui imprime une liste des carrées des nombres de 1 a 20
entiers = list(range(1,21))
resultats = [valeur**2 for valeur in entiers]
print(resultats)
```

### 1.2 Complexité 1

Compliquons les choses un tout petit peu!
On veut comme résultat d’un programme une liste de tuple de 2 items qui contiennent le nombre ET son carré pour les nombres de 1 à 20. Donc ce que l’on veut est:

```python
[(1,1), (2,4), (3,9), (4,16)…  …(20,400)]
```

Donc la ligne de notre petit programme devient

```python
resultats = [(entier, entier**2) for entier in range(1,21)]
```

La boucle ‘for’ reste la même, mais le traitement fait a chaque item a changé. Le résultat final reste une liste puisque toute l’expression est délimitée par des crochets ‘ [ ] ’. Les items que l’on veut dans notre liste sont des tuples qui eux sont délimités par des parenthèses ‘( )’ séparés par une virgule ‘,’. La valeur de ‘entier’ est utilisée 2 fois pour créer ce tuple. Un membre du tuple est la valeur elle-même de ‘entier’ et l’autre membre du tuple est la valeur de ‘entier’ au carré.


### 1.3 Complexité 2

Ça peut devenir beaucoup plus complexe et, par le fait, beaucoup plus puissant. Garde en mémoire que le niveau de compréhension de la complexité varie avec l’expérience.

Supposons qu’on a deux liste d’entiers `ls1=[1,2]` et `ls2=[3,1]` et nous voulons une liste de tuples de 2 items ou le premier item vient de la liste ‘ls1’ et le deuxième item vient de la liste ‘ls2’. MAIS nous ne voulons pas de tuple ou le premier item du tuple est égale au deuxième item du tuple. En programmation ‘ancienne’ nous écririons.

```python
# groupe en tuple les items de deux listes si ils sont differents
ls1 = [1,2]
ls2 = [3,1]
res = []
for item1 in ls1:
    for item2 in ls2:
        if item1 != item2:             # si les items sont different
            res.append((item1, item2))  # ajoute le tuple (item1,item2)
print(res)
```

Le même programme avec la compréhension de liste

```python
ls1 = [1,2]
ls2 = [3,1]
res = [(item1,item2) for item1 in ls1 for item2 in ls2 if item1!=item2]
print(res)
```

Remarques comment la ligne de notre compréhension de liste se lit exactement comme notre programme ‘méthode ancienne’. Dans ce vieux programme nous avons 3 lignes qui se lisent

`
for item1 in ls1:    for item2 in ls2:   if intem1 != item2:
`

ET c’est exactement ce que nous avons dans notre compréhension de liste!

Remarques aussi comment le format de la compréhension de liste ressemble à une ‘query SELECT’ de SQL. Au début on a le résultat, suivi du groupe de données dans lequel on puise les résultats, suivis de la condition qui contraint les résultats, En exemple:

```SQL
SELECT nom, prenom FROM crpf WHERE ville=’Quebec’
```

Parenthèse de programmation 3: La ligne de notre compréhension de liste précédente est lourde et longue:

```python
res = [(item1,item2) for item1 in ls1 for item2 in ls2 if item1!=item2]
```

Les variables item1 et item2 prennent toute la place et leur durée de vie ou portée (en anglais scope) est limité a notre expression. C’est-à-dire que ces variables n’existent plus une fois que cette ligne a été exécutée. Quand des variables ont une courte portée on utilise en général des noms de variables courts. Ce que l’on perd en détail on le gagne en facilité d’écriture et de lecture.

Dans un vrai programme professionnel cette ligne serait:

```python
res = [(a,b) for a in ls1 for b in ls2 if a!=b]
```

### 1.4 Complexité 3

Continuons avec les merveilleux dictionnaires.

Supposons que l’on veut un dictionnaire qui a comme clé un entier et chaque clé est associée à une valeur qui est la liste de ses puissances de 2 à 4. comme suit:
```
entier_puissances = { 1:[1,1,1],
                      2:[4,8,16],
                      3:[9,27,81],
                      4:[16,64,256] }
```

En programmation non-Pythonic on écrirait :

```python
entier_puissances = {} # un dictionnaire vide
for entier in range(1,5):
    puissances=[]  # une liste vide de départ
    for exposant in range(1,5):
        puissances.append(entier**exposant) # ajoute la puissance dans la liste
    # a ce point, la liste de puissances est faite
    # ajoutons la cle (entier) et sa valeur associées (nos puissances)
    # au dictionnaire.
    entier_puissances[entier] = puissances
print(entier_puissances)
```

En programmation Pythonic on écrit:

```python
entier_puissances = {en:[en**exp for exp in range(1,5)] for en in range(1,5)}
print(entier_puissances)
```

Donc si on révise la ligne en question:

Notre expression est délimitée par des accolades ‘{ }’ et les deux membres du résultat sont séparés par un deux point ‘ : ’ donc le résultat de tout ça sera un dictionnaire.

La clé des items de notre dictionnaire sera la valeur ‘en’ (abrégé d’entier). D’où vient la valeur ‘en’? De la boucle for exprimée à la fin de l’expression (`for en in range(1,5)`)
.
La valeur associée à la clé en sera une liste que nous exprimons par une autre compréhension. Une deuxième compréhension à l’intérieur de notre compréhension.

Cette deuxième compréhension est délimitée par des crochets ‘[ ]’ donc le résultat sera une liste. Ce qui est merveilleux ici c’est que cette compréhension de second niveau a accès à la valeur de ‘en’ de la compréhension de premier niveau! Donc on utilise la valeur de ‘en’ pour créer la liste de ses puissances. Que seront les items de la liste? Ils seront ‘en’ exposant ‘exp’ (abrégé d’exposant) et d’où vient ‘exp’? De la boucle ‘for’ qui itérera de 1 a 4.


### 1.5 Application

C’est bien beau tout ça de faire des carrés de nombre entier mais que fais-ton de cette technique dans la vraie vie?

Faisons un vrai programme qui utilise cette fonctionnalité.

Je veux avoir une liste des noms de tous les fichiers sous un répertoire. Pas les répertoires sous un répertoire juste les fichiers. On va retrouver notre ami pathlib! Tu peux copier et rouler ça, mais tu devras changer le répertoire dans la fonction main
from pathlib import Path

```python
def fichiers_pythonic(repertoire):
    # folder sera l’objet de la classe Path
    folder = Path(repertoire)
    # verifions que le folder existe
    if not folder.exists():
        return []       # il n’existe pas. retourne une liste vide
    # verifions que c’est un repertoire et non un fichier
    if not folder.is_dir():
        return []       # pas un repertoire retourne une liste vide
    # quand on est pythonic
    return [entry for entry in folder.iterdir() if entry.is_file()]

def main():
    fichiers = fichiers_pythonic(r'D:\source\Maurice\Documents')
    [print(fichier) for fichier in fichiers]

if __name__ == '__main__':
    main()
```

J’ai utilisé 4 méthodes de l’objet Path!

`Path.exists()`: retourne True si le répertoire (ou le fichier) existe sur le disque, sinon False.

`Path.isdir()`: retourne True si le path est un répertoire (pas un fichier), sinon False.

`Path.isfile()`: comme tu le devines, retourne True si le path est un fichier, sinon False.

`Path.iterdir()`: est un itérateur qui retourne un à un le contenu du répertoire. Il retourne tous les fichiers et tous les répertoires qui sont sous un répertoire sans discriminations.

Va voir a description et les exemples de ces méthodes sur https://docs.python.org/3/library/pathlib.html#methods

Alors dans notre programme on a deux compréhensions.

Celle dans la fonction fichiers_pythonic et celle dans la fonction main().
La première construit une liste (puisqu’elle est délimitée par ‘ [ ]’) qui donne des items `entry`. D’où viennent ces items? De la boucle `for` qui itère sur le contenu du répertoire `folder` donné par `folder.iterdir()`. Chacune de ces `entry` sera ajoutée à la liste seulement si cette `entry` est un fichier. Cette contrainte est assurée par la condition
`if entry.isfile()` de notre compréhension.

La deuxième est un peu comique. C’est une compréhension de liste, mais on se fout du résultat! Tout ce que l’on veut c’est que le print soit exécuté pour tous les éléments de la liste. On ne récupère pas la liste elle-même puisqu’elle ne contienra que des valeurs nulle (None).

### 1.5  Possibilités

Bon. Ce que tu peux faire maintenant.

Expérimenter avec la compréhension de liste avec des listes, des tuples et SURTOUT des dictionnaires. Les dictionnaires sont plus complexes mais combien plus puissant.

Imagine, (ou encore mieux, code-le) que tu as un dictionnaire comme suit:

```python
membre_d = {'nom': '',
            'prenom': '',
            'telephone': '',
            'ville': '',
            'actif': ''
            }
```

Maintenant imagine que t’as une liste de dictionnaires membres. ET maintenant imagine comment tu pourrais facilement fouiller dans cette base de données avec des compréhensions de listes. C’est-ti pas merveilleux ça!

De façon plus légère, chacun des membres de la liste pourrait être des tuples qui contiennent la même information sans les noms de champs :

```python
[ ( ‘Talbot’, ‘Jim’, ‘161-803-3988’, ‘Quebec’, ‘oui’), (‘Linda’ , ‘Millot’, ‘314-159-2653’, ‘Stoneham’) ]
```

Exercices:
A. Pour rester dans les mathématiques, faire une liste de strings des valeurs de pi ou chaque membre a une décimale de plus que le précédent. Comme suit:

```python
[ ‘3’, ‘3.1’, ‘3.14’, 3.’141’, ‘3.1415’ …. ]
```

Pour ce faire tu auras besoin des trucs suivants
```python
from math import pi # la constante pi
```

et la fonction ‘built-in’ `round` qui s’utilise comme suit:

```python
res = round(x,i)
```

ou x est un nombre réel (genre pi mettons!) et i est le nombre de décimales désirées (après le point).

Truc pour apprendre: écrit le programme en programmation standard (boucle for) et ensuite convertir le en compréhension.
