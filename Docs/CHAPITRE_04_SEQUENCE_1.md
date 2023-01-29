# CHAPITRE 04 : SÉQUENCE I


> **Contenu**
>  - Python: Listes
>  - Python: Tuples
>  - Python: Dictionnaires
>  - Python: Ensembles

## 0. Structure Composées

Python est un des premiers langages de programmation à avoir des structures de données composées directement fournis par le langage. En python on les appelle séquences ou collections. Elles sont utilisées partout et il faut bien les maîtriser. Voici les plus importantes et comment travailler avec elles.

## 1. Listes

#### NOTE IMPORTANTE MÉTHODE DE TRAVAIL:

Si tu lis ce qui suit sans rien faire d’autres, tu auras l’impression d’avoir compris. Si tu retapes tous ces petits exemples dans un programme python non seulement tu auras vraiment compris, mais en plus tu l’auras appris. Et ça c’est ce qui est important.

```PYTHON
var_lst = [1, 23.5, True, "Texte", [1,2,3]]
```

Alors voici ce que l’on voit dans cet exemple:
- Les listes contiennent plus qu’une valeur.
- Il peut y avoir différents types de valeurs à l’intérieur d’une liste incluant des types composées (liste, tuples, dictionnaires).
- Dans notre cas : un entier (1), un réel (23.5), un booléen (True), une chaîne de caractères (‘Texte’) et une liste ([1,2,3]).
- Les listes sont délimitées par les caractères ‘[‘ et ‘]’. Les membres d’une liste sont séparés par une virgule.

**LES ‘BRACKETS’: ‘[‘  ‘]’  DÉTERMINENT UNE LISTE.**

### Items et Indexation

Les items d’une liste peuvent être référés par un index (qui commencent à 0 à partir de la ‘gauche’ et qui commence à -1 à partir de la ‘droite’). Et les membres d’une liste sont mutables (peuvent être changés)

### Utilisation

- Imprimer une liste

    ```PYTHON
    print(f' la liste est: {var_lst}') # ou
    print(var_lst)
    ```

- Lire la 1<sup>ière</sup> valeur dans la liste.

    ```PYTHON
    r = var_lst[0]
    ```

- Assigner la valeur 48 au 3<sup>ième</sup> item de la liste

    ```PYTHON
    var_lst[2] = 48
    ```

- Imprime le 4ᵉ élément de la liste:

    ```PYTHON
    print(f‘var_lst[3] = {var_lst[3]}’)
    ```

- Imprime le dernier élément de la liste. On indexe en négatif (à partir de la droite)

    ```PYTHON
    print(f‘var_lst[-1] = {var_lst[-1]}’)
    ```

- Itérer sur les membres d’une liste. ***Il n’est pas nécessaire d’utiliser un index***:

    ```PYTHON
    for valeur in var_lst:
        print(f’ valeur = {valeur}’)
    ```

- Itérer sur les membres d’une liste avec un compteur:

    ```PYTHON
    for i, valeur in enumerate(var_lst):
         print(f’ index = {i} valeur = {valeur}’)
    ```

- Ajouter un membre à la fin d’une liste:

    ```PYTHON
    var_lst.append(‘nouvel item’)
    ```

- Allonger une liste avec une autre:

    ```PYTHON
    var_lst.extend([3, ‘texte2’, 45.1])
    ```

- Vérifier si une certaine valeur fait partie de la liste:

    ```PYTHON
    if ‘Texte’ in var_lst:
        print("’Texte’’ est dans la liste")
    else:
        print("’Texte’’ n’est pas dans la liste")
    ```

- Mesurer la longueur d’une liste

    ```PYTHON
    nombre_delements = len(var_lst)
    ```

- Accéder à un élément plus ‘loin’ que la grandeur de la liste cause une erreur

    ```PYTHON
    var_lst[52] = 52

    Traceback (most recent call last):
    File "test_liste.py", line 2, in <module>
    var_lst[52] = 52
    IndexError: list assignment index out of range
    ```

***Les membres d’une liste restent dans l’ordre dans lequel ils ont été ajoutés à la liste.***

### EXERCICES

Re-Écrire tout ce beau code dans un petit programme. Changer le contenu de la liste var_lst et recommencer!

## 2. TUPLES

Les tuples sont des types composés très léger (ils coûtent peu d’effort de la part du compilateur). ILS SONT IMMUABLES (on ne peut pas changer la valeur d’un membre d’un tuple). Ils sont idéaux pour combiner ensemble les valeurs de retours des fonctions et pour tous les petits objets qui vont bien en groupe de 2 ou plus. En exemples: (nom, prénom), (valeur et son index), (paramètres de fonction), etc.

    ```PYTHON
    var_tpl = (1, 2, ’jean’, 3.1415926, [1,2,3] )
    ```

Donc les membres d’un tuple sont séparés par des virgules et le tuple est délimité par des parenthèses ‘(‘ et ‘)’. Dans notre exemple ont définis un tuple qui contient 5 éléments: l’entier 1, l’entier 2, la string ‘jean’, le réel 3.1415926 (pi), et finalement la liste [1,2,3].

***LA VIRGULE ENTRE 2 VALEURS (OU VARIABLES) DÉTERMINE UN TUPLE***

Ex: `a = 1,2`  ⇐ C’est un tuple

Les membres d’un tuple sont référés de la même façon que les listes. Évidemment toutes les méthodes qui modifient le contenu d’un tuple causent une erreur puisque les tuples sont immuables.

### Utilisations
- Imprimer un tuple:

    ```PYTHON
    print(f'var_tpl = {var_tpl}')  # ou
    print(var_tpl)
    ```

- Accéder à un élément (par index)

    ```PYTHON
    print(f'var_tpl[1] = {var_tpl[1]}')
    ```

- Les tuples aussi peuvent être référencés par la ‘droite’

    ```PYTHON
    print(f'var_tpl[-1] = {var_tpl[-1]}')
    ```

- Itérer sur les membres d’un tuple:

    ```PYTHON
    for valeur in var_tpl :
        print(f'valeur = {valeur}')
    ```

- Itérer sur les membres d’un tuple avec un compteur

    ```PYTHON
    for c, v in enumerate(var_tpl):
        print(f'index {c} de var_tpl est {v}')
    ```

- Rechercher une valeur dans un tuple

    ```PYTHON
    x = [1,2,3]
    if x in var_tpl :
        print(f'la valeur {x} est dans var_tpl')
    else:
        print(f"la valeur {x} n'est pas dans var_tpl")
    ```

- Mesurer la longueur d’un tuple

    ```PYTHON
    nombre_delements = len(var_tpl)
    ```

- Essayer de changer un item produit une erreur (IMMUABLES)

    ```PYTHON
    var_tpl[1] = 25     # produit une erreur
    Traceback (most recent call last):
    File "tuple.py", line 2, in <module>
        var_tpl[1] = 25
    TypeError: 'tuple' object does not support item assignment
    ```

Juste pour te frotter le coconut avec de la laine d’acier 
On a une liste à l’intérieur de notre tuple. On a dit que les éléments d’une liste sont mutables (peuvent changer) mais que les éléments à l’intérieur d’un tuple sont immuables (ne peuvent pas être changés). Alors qu’est-ce qui est vrai ici !

```PYTHON
# ca c’est notre liste [1,2,3]
print(var_tpl[4])
# si j’ajoute un autre index ([]) je rejoins un seul item de la liste
# ca devrait donné 2, l’element a l’index 1 de la liste [1,2,3]
print(var_tpl[4][1])
# Pis la, si j’essaie de le changer
var_tpl[4][1] = 25    # ben maudine!
# ca  fonctionne !!!!
print(var_tlp)        # surprise.
var_tpl[4] = [5,6,7]  # Mais si je change la liste au complet. BOUM !
```

## 3. Dictionnaires

Les dictionnaires sont sans doute le type composé le plus important de python. Ils sont d’une richesse inégalée dans tous les langages de programmation. A tel point qu’on peut dire qu’un programme python qui n’utilise pas au moins un dictionnaire n’est pas correct.

Il faut les apprendre et les comprendre de façon à ce que leur utilisation soit une seconde nature. Ça devrait être aussi facile d’écrire un dictionnaire que de créer une variable simple (genre ```a=3```). Allons-y

Les dictionnaires sont des collections de groupe de 2 items: une clé et une valeur. Un dictionnaire peut contenir n'importe quelle quantité de groupe clé-item.

Les clés peuvent être de n’importe lequel des types de base (int, float, str, etc) ***MAIS LA CLÉ DOIT ÊTRE UNIQUE DANS LE DICTIONNAIRE***.
Les valeurs n’ont pas besoin d’être uniques et peuvent être des types de base (int, str, float, etc ) ou des types composés comme des listes, des tuples et même des dictionnaires!

La syntaxe des dictionnaires:

```PYTHON
var_dct = { ‘un’: 1, ‘deux’: 2 }
```

Chaque item clé-valeur est séparé par un deux-points, les items sont séparés par des virgules et le dictionnaire au complet est délimité par des accolades { et }.

__LES ACCOLADES (‘{‘ ET ‘}’) ET LE DEUX-POINT DÉTERMINENT UN DICTIONNAIRE.__

### Utilisation

- Définir un dictionnaire

    ```PYTHON
    var_dct = { ‘un’: 1, ‘deux’: 2 }
    ```

- Accéder à une valeur se fait en utilisant la clé comme index

    ```PYTHON
    valeur = var_dct['un']
    ```

- Évidemment cette clé peut être dans une variable

    ```PYTHON
    clef = ‘un’
    valeur = var_dct[clef]
    ```

- Changer la valeur associée à une clé.

    ```PYTHON
    var_dct['un'] = 23
    ```

- Ajouter un item (groupe clé valeur)

    ```PYTHON
    var_dct['trois'] = 3
    ```

- Éffacer un item (clé & valeur)

    ```PYTHON
    del var_dct['deux']
    ```

- Vérifier la présence d'une clé sans créer une erreur (arrêt du programme) si elle n'y est pas.

    ```PYTHON
    valeur = var_dct.get('un', -1)
    if valeur != -1:
        print(f"Clé 'un' trouvee valeur={valeur}")
    else:
        print(f"Clé 'un' NON trouvée")
    valeur = var_dct.get('deux', -1)
    if valeur != -1:
        print(f"clé 'deux'trouvée valeur={valeur}")
    else:
        print(f"clé 'deux' NON trouvé")
    ```

__ET LES 3 CHOSES LES PLUS IMPORTANTES___

- Parcourir le dictionnaire avec les clés et ses valeurs

    ```PYTHON
    for cle, valeur in var_dct.items():
        print(f"Clé = {cle} et sa valeur ={valeur}")
    ```
- Extraire une liste des clés

    ```PYTHON
    liste_des_cles = var_dct.keys()
    ```

- Extraire une liste des valeurs

    ```PYTHON
    liste_des_valeurs = var_dct.values()
    ```

### Exercices

Re-écris tous les exemples précédents avec un dictionnaire différent par exemple :

```PYTHON
var_dct_2 = { 1: ‘un’, 2: ‘deux’ }
```

## 4. Ensembles (set)

Les ensembles sont des séquences très spéciales, rarement utilisées mais qui ont parfois une grande utilité.

Les ensembles (set) sont des groupes non-ordonnées d’items uniques. Ces items peuvent être des entiers, des réels ou des strings mais ne peuvent pas être des listes, des dictionnaires ou des tuples.
mon_set = { 1,2,4,8 }

__LES ACCOLADES ‘{‘ ET ‘}’ ET LA VIRGULE ENTRE LES VALEURS DÉTERMINENT UN SET__

Les sets permettent, comme les listes, permettent de vérifier si une ou des valeurs font partie du set avec les fonctions ‘in’ et ‘not in’. Mais comme les sets sont non ordonnées ils ne permettent pas l’utilisation des index et du découpage.

Les sets ont une utilisation assez complexe qui ré-implémente les symboles mathématiques pour l’application des règles des mathématiques des ensembles. La plupart de ces fonctions retournent un nouveau set.

### Utilisation

- Union (tous les membres de set1 et set2).

    ```PYTHON
    set3 = set1 | set2
    ```

- Différence (les membres qui ne sont pas communs aux deux sets).

    ```PYTHON
    set3 = set1 ^ set2
    ```

- Sous-Ensemble  (set1 est entièrement compris dans set2).

    ```PYTHON
    set3 =  set1 ≤ set2
    ```

- Sur-Ensemble (set1 inclus tous les membres de set2).

    ```PYTHON
    set3 = set1 > set2
    ```

- Disjonction (aucun item n’est commun entre les deux sets).

    ```PYTHON
    # return (True or False)
     set1.isdisjoint(set2)
     ```
- Intersection: (le set des membres qui sont communs au deux sets).

    ```PYTHON
    set3 = set1 & set2
    ```

La particularité la plus intéressante des sets est que tous les membres doivent être uniques et que si un item se retrouve 2 fois (ou plus) lors de la création du set, les membres qui se répètent ne seront présents qu'une seule fois!

```PYTHON
mon_set = {1,2,2,2,2,4,8}
print(mon_set)
⇒ {1,2,4,8}
```

Cette caractéristique est utilisée régulièrement pour enlever les doublons d’une liste. On crée un set à partir d’une liste et on fait une liste avec le résultat (on s’en sert ici pour enlever ‘l’écho’):

```PYTHON
ls1 = ["allo","allo","allo","bonsoir","bonsoir","bonsoir"]
ls2 = list(set(ls1))
print(ls2)
⇒ ['allo', 'bonsoir']
```
