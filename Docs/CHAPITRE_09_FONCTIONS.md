# CHAPITRE 09 - Fonctions
>**Contenu:**
> - Python – Fonctions
> - Python - Arguments de fonctions
> - Design et programmation – Diviser pour régner
> - Python – Shallowcopy et deepcopy

## 0. DÉFINITION DE FONCTIONS

Une fonction est un ensemble d’instructions ordonnées, regroupées sous un même nom et réutilisable. Une fonction peut recevoir des paramètres (ou arguments) en entrée et, dans le cas de python, retourne toujours une valeur.

### Syntaxiquement:

__LE MOT ‘DEF SUIVIS D’UN NOM, SUIVI DE PARENTHÈSES ET DE DEUX
POINTS DÉFINISSENT LA DÉCLARATION D’UNE FONCTION.__

Exemple 1:

```python
def addition(a,b):
     return a+b
```

La fonction addition prend 2 paramètres, `a` et `b`, et retourne la somme de ces deux paramètres. Pour utiliser cette fonction de façon correcte il est important de recueillir le résultat (la valeur retournée) dans une variable lors de son utilisation:

Exemple 2:

```python
res = addition(3,4)
print(res)
==> Résultat: 7
```

Exemple 3:

```python
def print_separateur():
    print(‘=’*10)
```

La fonction print_separateur ne prend aucun argument et imprime simplement 10 fois le caractère ‘=’. Cette fonction retourne la valeur None. Ceci ce fait implicitement sans que la fonction n’utilise le mot clé return. Pour le prouver roulons le code suivant dans le même module:

```python
a = print_separateur()
print(a)
==> Le résultat : None
```

## 1. APPELLES DE FONCTIONS

Afin d’utiliser une fonction il faut l’appeler. L’appel de fonction se fait simplement en utilisant le nom de la fonction, suivis des parenthèses contenant les paramètres nécessaires à la fonction ou aucun paramètre si c’est le cas.

***LE NOM DE LA FONCTION SUIVI DES PARENTHÈSES DÉFINISSENT UN APPEL DE FONCTION.***

Un nom de fonction sans les parenthèses est un objet (comme tout en python est un objet) qui peut être assigné à une autre variable et utilisé de cette façon. Donc notre fonction addition peut être assignée (`=`) à un autre nom (une variable) et utilisé à partir de ce nom de variable.

Testons la chose avec le programme suivant.

```python
# module: assigne_fonction.py

def addition(a,b):
    return a+b

def main():
    operation = addition
    res = operation(3,4)
    print(res)

if __name__ == '__main__':
    main()
```

Copier le programme précédent dans PyCharm et le rouler.

La première ligne de main() se lit comme suit: la variable `operation` contient la fonction `addition`.

Le programme `assigne_fonction.py` prouve qu’il est possible de manipuler les fonctions comme n’importe quelle variable. On peut les assigner à d’autres variables, les mettre dans une liste ou un tuple, les envoyer comme paramètres à d’autres fonctions, etc. bref tous ce que l’on peut faire avec une variable on peut le faire avec une fonction.

### Exercices Groupe 1
```python
# module fonction_liste.py

def addition(a,b):
    return a+b

def multiplication(a,b):
    return a*b

def main():
    # une liste de fonctions
    algebres = [addition, multiplication]
    # utilisation de l'item 0 de la liste: addition
    res = algebres[0](3,4)
    print(res)
    # utilisation de l'item 1 de la liste: mutiplication
    res = algebres[1](3,4)
    print(res)

if __name__ == '__main__':
    main()
```

COPIER le code de fonction_liste.py dans Pycharm et le rouler.

### Exercices 1

À l’intérieur du module fonction_liste.py

**Exercice 1:**

Écrire une fonction puissance qui prend deux paramètres (a,b) et qui retourne la valeur de ‘a’ à la puissance ‘b’ (a<sup>b</sup>).

**Exercice 2:**

Intégrer la nouvelle fonction puissance à la liste de fonction algebre et ajouter le code nécessaire dans `main()` pour que puissance soit appelée de la même façon que addition et multiplication.

**Exercice 3:**

Remplacer le code de main() de façons a ce que chaque fonction présente dans la liste algebre soit appelée à l’intérieur d’une boucle for qui itère sur les items (fonctions) de la liste algebre.


## 2. FONCTION EN PARAMETRES

Maintenant que nous savons manipuler les fonctions dans des variables, apprenons à les utiliser comme paramètres d’autres fonctions. C’est la leur force.

```python
# modules fonction_param.py

def addition(a,b):
    return a+b

def multiplication(a,b):
    return a*b

def applique_1d(operation, matrice, scalaire):
    """ applique une operation algebrique aux membre d'une
        matrice a 1 dimension.
    Args:
        operation: fonction qui sera utiliser pour 'combiner'
        les items de la matrice avec la valeur scalaire
        matrice: liste
        scalaire: valeur a combiner aux item de a_list

    Returns:
    list: une nouvelle matrice sur laquelle le scalaire a ete opere
    """
    res = []
    for x in matrice:
        res.append(operation(x,scalaire))
    return res

def main():
    matrice_test = [1,2,3,4,5,6,7]
    # fait l'addition scalaire de la matrice
    methode = addition
    new_list = applique(methode, matrice_test, 3)
    print(new_list)
    # multiplies produit scalire de la matrice par 5
    methode = multiplication
    new_list = applique(methode, matrice_test, 5)
    print(new_list)

if __name__ == '__main__':
    main()
```

Copier ce programme dans PyCharm et le sauver sous le nom fonction_param.py

Le programme précédent se lit de la façon suivante:

Au début du programme deux fonctions très simples sont définies. La fonction `addition` qui prend 2 paramètres et retourne la somme de ces deux paramètres. Et la fonction `multiplication` qui prend 2 paramètres et retourne la multiplication de ces 2 paramètres.

La fonction suivante est le cœur du programme. Cette fonction se nomme `applique_1d` et reçois 3 paramètres: une fonction (operation) une liste (matrice), une valeur (scalaire). Elle crée une nouvelle liste (res) qui recevra des items. La boucle `for` itère sur les items de la matrice et à chacun de ces items on applique la fonction operation avec la valeur scalaire.

Enfin la fonction main(). On crée d’abord une liste `matrice_test` pour servir d’exemple. Ensuite on met la fonction addition dans la variable `methode`, et on appelle la fonction applique avec COME PARAMETRES la 'methode', la 'matrice_test' et la valeur '3'. Finalement on imprime le résultat de cet appel.

Ensuite on répète le même code avec cette fois-ci la fonction multiplication.

### Exercice: 2

- 2.1 Ajouter au code du module `fonction_param.py`. Écrire une fonction puissance qui retourne prend 2 arguments (a et b) et qui retourne ‘a’ à la puissance ‘b’ (a<sup>b</sup> ). Ajouter le code nécessaire à la fonction main pour appliquer notre nouvelle fonction puissance à tous les membres de la liste.

- 2.2 Re-écrire la fonction applique avec une compréhension de liste plutôt qu’une boucle `for`.

- 2.3 Dans la fonction main(), la variable methode n’existe que pour la démonstration. Changer le code de main() de façon à ce que cette variable ne soit plus utilisée. (c’est plus pythonic!)

- 2.4 Dans main(), mettre les 3 fonctions (addition, multiplication et puissance) dans une liste et appeler applique avec chacune des fonctions dans la liste. Faire le tout à l’intérieur d’une boucle for.

- 2.5 Refaire l’exercice 2.4 en mettant le tout dans une compréhension de liste (évidemment le résultat sera une liste).

- 2.6 Mettre les fonctions addition, multiplication et puissance dans un module séparé (operations.py), et les importer et les utiliser dans fonction_param.py.

### Réflexions!
Prends un moment pour réaliser ce qui vient de se passer et aller un peu plus loin de façon très simple.

On a pris un tout petit problème additionner ou multiplier 2 nombres. Ensuite, sans changer le code de nos opérations simples, nous avons ajouté un niveau de complexité en appliquant notre opération sur une liste.

En mathématiques les matrices en 2 dimensions sont une collection de valeurs placées en ligne et en colonne (comme une feuille Excel). Les opérations matriciel-scalaire applique une opération avec une seule valeur (un scalaire) sur toutes les valeurs de la matrice.

En python on peut représenter les matrices en 2 dimensions comme des listes de listes ou chaque sous-liste est une ligne donc:

`mat_2d = [[1,2,3], [4,5,6], [7,8,9]]`


Donne la matrice:
```
1 2 3
4 5 6
7 8 9
```

Si on veut maintenant appliquer nos opérations sur une matrice en 2 dimensions, on ne commence pas à écrire une longue fonction complexe, on écrit une fonction qui réutilise applique_1d sur chacune des lignes:

```PYTHON
def applique_2d(operation, mat_2d, scalaire):
    res = [applique_1d(operation, mat_1d, scalaire) for mat_1d in mat_2d]
```

On est rendu à faire de l’algèbre linéaire relativement complexe seulement en construisant sur des fonctions très simples d’une seule ligne.

***Ça c’est du DIVISER POUR RÉGNER de la meilleure variété.***

- À chaque niveau de complexité qu’on a ajouté, on est jamais revenus en arrière pour modifier nos fonctions simples de départ.

- Toutes nos fonctions, à tous les niveaux, sont réutilisables. On peut utiliser matrice_1d ou addition sans problème.

- On peut ajouter une fonction à très bas niveau (ex: division) et toutes les fonctions de plus hautes complexités vont pouvoir l’utiliser tout de suite, sans changements de code.

- Le code n’existe qu’a une seule place. Si on a un problème dans une opération, on a pas à le corriger pour matrice_1d, matrice_2d etc. On a juste à le corriger dans la fonction d’opération.

- On peut ajouter matrice_3d sans difficulté parce qu’on a une base de départ solide.

Bref, ce qu’on vient de faire est du code parfait. C’est rare, savoure-le!

### Exercices 3

   Implémenter matrice_2d dans fonction_param.py

## 2. Parenthèse python: shallowcopy deepcopy.

___À lire attentivement:___

Les variables de type composées mutables (listes, dictionnaires, objets) ne sont pas copiées dans une nouvelle variable lors de l’assignation ( = ).

Autre formulation: Si on assigne une liste (a) à une variable (b). b ne contient pas une copie de la liste a. b contient la même liste!

Exemple de l’explication:

```python
a=[1,2,3]
b=a
print(f" b = {b})
b[0]=1000
print(f" b = {b})
print(f" a = {a})
```

Le programme ici produira l’output suivant:

```python
b = [1,2,3]
b = [1000, 2, 3]
a = [1000, 2, 3]
```

___Changer la valeur de b,  change la valeur a!___

Cet effet s’appelle le shallowcopy (copie en surface). Ce qui se produit c’est que b=a ne fait pas une copie de la variable a dans la variable b, il donne un autre nom (b) à la variable a.

Pourquoi? Pour sauver de l’espace et du temps. Nos petits exemples ne causeraient pas de problèmes, mais une liste de 10 000 dictionnaires prendrait plusieurs minutes à se copier en mémoire et ça c’est inacceptable.

Il existe une façon de circonvenir au problème en utilisant le module ‘copy’ de la librairie standard.

```python
import copy

a = [1,2,3]
b = copy.deepcopy(a)
b[0]=1000
print(a)
print(b)
```

Ça peut sembler épouvantable, mais en fait c’est très rarement problématique. Pour te donner un exemple, mon application de moniteur cardiaque a 8500 lignes de code qui manipule des listes sans arrêts et j’ai dû utiliser deepcopy une seule fois!

L’important c’est d’être au courant de cet état de fait parce que cela affecte aussi le passage de paramètres aux fonctions.

## 3. Arguments - Passation

Note: les mots: paramètres et arguments sont utilisés ici comme synonymes, et ont la même signification.

Analysons en profondeur le code suivant

```python
def f1(p1,p2):     # 2
   return(p1+p2)   # 3


r = f1(10,20)      # 1
print(r)
```

Lors de l’exécution du code:

1 – On appelle f1 avec les paramètres 10 et 20

2 - f1 reçoit les valeurs 10 et 20 de la façon suivante:

```
    p1 = 10
    p2 = 20
```

3 - Exécution du reste de la fonction f1 avec
    p1 et p2 comme variables locales

Ce qui est important ici est que les paramètres, lors de l’appel, sont passés à la fonction par une assignation (=) à des variables locales a f1.

___ET CETTE ASSIGNATION SUIT LES MÊMES RÈGLES QUE NOUS AVONS VUES DANS LA SECTION PRÉCÉDENTE (SHALLOWCOPY DEEPCOPY). C’EST-A-DIRE QUE LES LISTES ET LES DICTIONNAIRES NE SERONT PAS COPIÉES DANS LES NOUVELLES VARIABLES.___

Preuve:

```python
def f1(l1):
    l1[0] = "nouveau"
    return(l1)

a = [1,2,3,4]
print(f"a = {a}")
r = f1(a)
print(f"r = {r}")
print(f"a = {a}")
```

Résultat

```
a = [ 1, 2, 3, 4]
r = ['nouveau', 2, 3, 4]
a = ['nouveau', 2, 3, 4]
```

La variable globale ‘a’ a été changée par la variable locale l1 à l’intérieur de la fonction f1.

### EXERCICE: 3.1

Utiliser la librairie copy et adapter le programme précédent pour que la fonction f1 retourne la même valeur sans affecter la variable a.

## 4. Arguments 2 – Types

Python offre 2 type d’arguments. Les arguments positionnels et les arguments nommés.

### 4.1 Arguments Positionnels

(anglais: positional arguments).

C’est le type le plus courant ou les valeurs des paramètres de l’appel sont passés à la fonction dans l’ordre ou ils sont donnés. Selon leurs positions.

Exemple

```python
def f1(a,b,c):
	pass

f1(3,2,1)
```

Dans cet exemple la valeur 3 sera assigné à la variable a, la valeur 2 à la variable b et la valeur 1 à la variable c.

__Tous les paramètres positionnels sont obligatoires et doivent être tous fournis lors de l’appel de la fonction. Dans l’exemple précédent si l’appel de la fonction était  f1(3,2), cet appel causerait une erreur qui arrêterait le programme.__

### 4.2 Arguments Nommés

(anglais: keyword arguments)

Exemple
```python
def f1(a=0,b=0,c=0):
    print(a,b,c)

f1(c=3,a=1)
f1(4,3,2)
```

Syntaxe: Dans la déclaration de fonction les arguments nommés sont assignés à une valeur par défaut.

Dans l’appel de la fonction ils peuvent être nommés par la variable qui les recevra et être assigner une valeur.

Ils peuvent aussi être utiliser poisitionnelement, en ce cas les valeurs sont assignées dans l'ordre de la declaration de la fonction

__Les arguments nommés sont optionnels et ne sont pas forcé à suivre un ordre prescrit. Il est possible de ne pas les nommer et d’utiliser seulement leurs positions, en ce cas ils doivent suivre l’ordre dans lequel ils sont dans la déclaration de la fonction.__

### 4.3 Utilisation

___IL EST POSSIBLE D’UTILISER LES DEUX TYPE D’ARGUMENTS POUR UNE FONCTION___

Exemple

```python
def f1(a,b,c=10,d=4)  # 1
    print(a,b,c)

f1(2,3)               # 2
f1(4,5,d=200)         # 3
f1(1,2,3,4)           # 4
```

1. Déclaration: 2 arguments positionnels et 2 arguments nommés.
2. 1er Appel: seulement les 2 arguments positionnels.
3. 2ᵉ Appel:  les 2 arguments positionnels et le 4ᵉ arguments nommés.
4. 3ᵉ Appel: Lorsque l’on mixe les types d’arguments, les arguments retiennent leurs caractéristiques: les  positionnels sont obligatoires et ordonnés, les nommés sont optionnels et non ordonnés.

___RÈGLE IMPORTANTE: SI ON UTILISE LES 2 TYPES D’ARGUMENTS, LES ARGUMENTS POSITIONNELS DOIVENT TOUS APPARAÎTRE AVANT LES ARGUMENTS NOMMÉS ET CE AUSSI BIEN DANS LA DECLARATION DE LA FONCTION QUE DANS L'APPEL DE CETTE FONCTION.___

Exemple:

```python
def f1(a=4,b):  # cause une erreur dans la declaration de fonction
f1(a=4,3)       # Cause aussi une erreur lors de l'appel
```

## 5. Arguments – UNPACKING

Dans le chapitre `SEQUENCE 3` nous avons brièvement touché le sujet du déballage (unpacking) des séquences. Nous avons vu le déballage implicite des tuples:

```python
t = (1,2)
a, b = t
print(a)
print(b)
```

Ce petit programme imprimera :

```
1
2
```

On dit que le tuple t est déballé dans les variables a et b.

Ce déballage peut se faire sans assignation en utilisant l’operateur ‘star’ *.

Exemple:
```python
l = [1,2,3,4,5]
print(l)
print(*l)
```

Ce programme imprimera:

```
[1, 2, 3, 4, 5]
1 2 3 4 5
```

La différence peut paraître subtile dans un print, mais `*l` représente 5 valeurs libres qui ne sont pas dans une structure de données.

_EXACTEMENT COMME DES PARAMÈTRES POSITIONNELS!_

Donc:
```python
def f1(a,b,c):      # f1 accepte 3 arguments positionnels
    return (a+b)*c  # retourne la somme des 2 premiers multiplié par le 3ᵉ

l = [1,2,3]
r = f1(*l)          # On déballe la liste `l` pour s’en servir comme paramètres
print(r)

==> Résultat: 9
```

___ET POUR LES PARAMÈTRES NOMMÉS ON UTILISE DES DICTIONNAIRES.___

Note: pour les dictionnaires il faut doubler l’opérateur star ‘*’ (une fois pour les clés et une fois pour les valeurs)

```python
def f2(a=1,b=2,c=3):  # f1 accepte 3 arguments nommés
    return (a+b)*c    # retourne la somme de a et b multiplié par c

d = {'a':10,          # On crée le dictionnaires des  paramètres
     'b':20,
     'c':30 }
r = f1(**d)           # Et on le déballe pour appeller f1
print(r)
```

ET on peut utiliser les deux dans un seul appel a une fonction complexe:

```python
def window(sizex, sizey, title = ‘’, scrollbar=False):
    print(f"Largeur de fenetre: {sizex}")
    print(f"Hauteur de fenetre: {sizey}")
    print(f"Titre de fenetre: {title}")
    print(f"Presence de scrollbar: {scrollbar}")

sizes = [300,200]
decors = { 'title': 'Fenetres principales'}
window(*sizes,**decors)
```

Dans l’exemple précédent remarque le dictionnaire décor. Il ne contient qu’un seul des 2 paramètres nommés. Les paramètres nommés restent facultatifs même s’ils proviennent d’un dictionnaire.

Ce genre de mélange de paramètres est souvent utilisé dans les packages d’interface graphique (Tkinter, PySide6, etc) ou les fonctions ont de nombreux paramètres, certains étant obligatoires et d’autre facultatifs.

Comme exemple: l’objet Tkinter.label, accepte 18 arguments, 1 argument obligatoire et 17 autres optionnels!

REMARQUEZ ICI QUE L’ÉTOILE ‘*’ EST UTILISÉE LORS DE L’APPEL DE LA FONCTION POUR DÉBALLER LES PARAMÈTRES.

Il EST POSSIBLE D’UTILISER L’ÉTOILE DANS LA DÉCLARATION DE FONCTION POUR PRODUIRE L’EFFET INVERSE, C’EST-À-DIRE EMBALLER LES ARGUMENTS POUR LES METTRE DANS UNE LISTE OU UN DICTIONNAIRE. C’EST CE QUI PERMET D’AVOIR DES FONCTIONS QUI ACCEPTE UN
NOMBRE VARIABLE & INCONNU DE PARAMÈTRES.

Exemple

```python
def fonctionvar(*args):
    # tous les arguments sont emballés dans la liste args
    print(args[0])
	  for i in args:
       print(i)

fonctionvar(1,2,3,4,5)
fonctionvar('a','b','c')
fonctionvar(10,20,30,40,50,60,70,80,90)
```

Ou avec des dictionnaires:

```python
def fonctiondict(**kargs):
    for k,v in kargs.items():
        print(k,v)

fonctiondict(un=1,deux=2,trois=3)
fonctiondict(a=1,b=2)
fonctiondict(un='a')
```


Évidemment python étant python il est possible d’utiliser les deux en même temps!

Exemple:

```python
def f_var_dic(*args,**kargs):
    for i in args:
       print(i)
    for k,v in kargs.items()
       print(k,v)

f_var_dic(1,2,3,quatre=4,six=6)
f_var_dic()
f_var_dic(six=6)
f_var_dic(1,2)
```

Cette technique est utilisée, entre autres, pour recevoir les paramètres de la ligne de commande lors du lancement d’un programme et pour tout autre fonction qui peut prendre un nombre inconnu de paramètres. Aussi, encore une fois pour les appels de fonctions complexes des modules d’interfaces graphiques.

Bon c’est le temps de pratiquer tout ça.

### Exercices 5: Groupe 1

- Exercice 4.1

Écrire une fonction qui prend un nombre inconnu d’arguments positionnels seulement, qui imprime le nombre d’arguments et les arguments un à un et finalement retourne la somme des arguments.

- Exercice 4.2

Quand on travaille avec des interfaces graphiques chaque objet a une diarrhée d’arguments: la couleur du fond, la couleur du texte, la police de caractères, la largeur de bande sur le côté, etc, etc. Pour nous simplifier la vie dans nos applications nous bloquons certaines de ces options pour donner un style cohérent à nos objets. Comme exemple on veut que toutes les ‘label’ contenant du texte ait la même couleur de fond (background), sans devoir la paramétriser à chaque fois Nous faisons ça en enveloppant les appels à une fonction pour qu’il passe par notre fonction. C’est une technique de design qui s’appelle les décorateurs. On ajoute, ou soustrait, de la fonctionnalité à un objet (fonction) existant, bref on le décore.

Regardez le programme tk_lafontaine.py à la page suivante et remarquez comment l’appel a la fonction  tk.label est lourd. Un programme avec interface de ce genre peut avoir des dizaines de ‘label’ partout à travers le code. Si les appels de chaque fonction sont aussi lourds le code le sera aussi. Copier le programme dans PyCharm et l’essayé.

```python
 # tk_lafontaine.py
import tkinter as tk
import tkinter.font as tkfont

lafontaine = """La Cigale, ayant chanté
Tout l'été,
Se trouva fort dépourvue
Quand la bise fut venue :
Pas un seul petit morceau
De mouche ou de vermisseau."""

root = tk.Tk()

# place un label sur la fenetre root
message = tk.Label(root, text=lafontaine, background='#ADD8FF',
                   font=tkfont.Font(family='Arial',size=14,
                   slant='italic'),
                   justify=tk.LEFT,padx=2,pady=2,borderwidth=4)

message.pack()
```

Le but de l’exercice est d’envelopper la fonction tk.label en forçant les paramètres que nous voulons forcés et en laissant les paramètres que nous voulons disponible à l’utilisateur de la fonction tk.label.

Les paramètres disponibles, que nous permettons de changer, seront: la fenêtre mère (root), le texte (text) et la largeur des cotés (borderwidth). Tous les autres paramètres sont forcés et doivent avoir la valeur de l’exemple ci-haut.

Le design de la solution ressemblera à ça (pour l’enveloppe de la fonction tk.label):

```python
def mon_label(parametres):
    #verification et ajustement de parametres recu
    #ajout des parametres fixes (forcés)
    msg = tk.label(mettre les bons parametres)
    return msg
#et son utilisation
message = mon_label(parametres)
```

Bonne chance!
