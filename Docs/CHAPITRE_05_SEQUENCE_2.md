# CHAPITRE 05 SÉQUENCE II

>**Contenu**
>- Python: Découpage
>- Python: Chaîne de caractères

## 0. Découpage
Dans le tutoriel des listes, et des tuples mon but était de t’introduire aux séquences et te donner ce qu’il faut pour arriver aux dictionnaires le plus tôt possible. Il y a une capacité des séquences que j’ai laissées de côté, mais c’est maintenant temps d’y arriver: le découpage des séquences (‘slicing’)

Le slicing est une fonctionnalité syntaxiquement très simple (c’est facile à écrire), mais le résultat peut être très difficile à prévoir. Beaucoup d’encre (et de transfert de données) ont coulé pour expliquer le slicing. Je vais essayer de rendre ça bref et concis.
Toutes les séquences (liste, tuple, chaîne de caractères) peuvent être découpées. La syntaxe est simple la voici:

```PYTHON
sequence[startindex:endindex:step]
```

En voici un exemple

```PYTHON
lst =[0,1,2,3,4,5,6,7,8,9]
print(lst[2:5:2])
==> [2, 4]
```

Voici ce qui se passe dans lst[2:5:2]
- Le premier 2 indique l’index dans la séquence ou le découpage commence (0,1,2).
- Le 5 indique l’index dans la séquence ou le découpage termine (0,1,2,3,4,5).
- Le 2ᵉ 2 indique l’intervalle de sélection. Dans ce cas-ci on dit: retourne 1 item sur 2.

Tous les indices de découpage sont optionnels et les valeurs par défauts sont `[ 0: len(lst): 1]`

ET TOUS CES INDICES PEUVENT ÊTRE NÉGATIFS!

Le découpage retourne toujours une copie de l’objet (séquence) qui est découpé. La séquence elle-même n’est pas modifié. Je pourrais en parler pendant des heures à t’expliquer tous les détails mais une image vaut mille mots. Donc voici mille mots:

<p align="center">
    <img src="Assets\Asset_1_2x.png">
</p>

Le grand truc de la compréhension du découpage est que l’index, dans les accès par index, se fait sur l’item de la séquence.

__Le découpage, lui, se fait ENTRE les items de la séquence__.

Tout ça peut donner le vertige tellement ça peut devenir complexe mais c’est toujours utilisé pour à peu près pour les mêmes choses. Ci-dessous tu trouveras les utilisations classiques du découpage qui couvrent 99 % des utilisations.


### Découpage - Utilisation

- Faire une copie d’une séquence

    ```PYTHON
    copy_lst = lst[:]
    ```

- Tous les items d’une séquence sauf le dernier

    ```PYTHON
    lst_sans_dernier = lst[:-1]
    ```

-  Tous les items d’une séquence sauf le premier

    ```PYTHON
    lst_sans_premier = lst[1:]
    ```

- La séquence inversée

    ```PYTHON
    lst_inverse = lst[::-1]
    ```

- Les n premiers items d’une séquence

    ```PYTHON
    lst_n_premiers = lst[:n]
    ```

- Les n derniers items d’une séquence

    ```PYTHON
    lst_n_derniers = lst[-n:]
    ```

- Un item sur 2 à partir du premier item (nombres pairs!)

    ```PYTHON
    lst_pair = lst[::2]
    ```

- Un item sur 2 à partir du deuxième item (nombres impairs)

    ```PYTHON
    lst_impair =lst[1::2]
    ```

## 1. CHAÎNES DE CARACTÈRES

Note: À partir de maintenant je vais utiliser le mot ‘string’ au lieu de ‘chaîne de caractères’. Merci.

Donc les strings sont des objets. Mais ce sont des objets très spéciaux. Ce sont des séquences comme les listes, mais ils sont IMMUABLES comme les tuples. Et évidemment leut contenu se limite à des caractères.

Copie ce qui suit dans un fichier python "scratch", lis-le très bien, exécute-le et joues un peu avec :

```PYTHON
# 3 strings délimitées différemment
s1 = 'abcdef'
s2 = "abcdef"
s3 = """abcdef
        uvwxyz"""
# s3 est  string multi-ligne Ce n'est pas un commentaire ni une documentation (DocString)
# CAR IL N'EST PAS PLACÉ DIRECTEMENT SOUS UNE DÉCLARATION DE FONCTION
print(f" s1 = {s1}\n s2 = {s2}\n s3 = {s3}")
# on peut accéder à chaque caractère par index (comme une liste). Le premier caractère:
print(f"s1[0] = {s1[0]}")
# Le dernier caractère, facilement par la droite (index négatif)
print(f"dernier caractere par la droite = s1[-1] = {s1[-1]}")
# Mesurer la longueur (le nombre d’items (caractères)) comme une liste:
print(f"longueur de s1 = len(s1) = {len(s1)}")
print(f"longueur de s3 = len(s3) = {len(s3)}")
# Itérer sur les caractères de la string avec une boucle 'for'
for caractere in s2:
    print(f"Caractere de s2 = {caractere}")
# refaire la même chose en les comptant avec ‘enumerate’ (comme une liste)
for num,car in enumerate(s2):
    print(f"Caractere #{num} de s2 = {car}")
# Vérifier l'appartenance d'un item à la string avec 'in'
if 'a' in s1:
    print("'a' est dans s1")

if 'ab' in s1
    print("'ab' est dans s1")

# Vérifier la non-appartenance d'un item a la string avec 'not in'
if 'h' not in s1:
    print("'h' n'est pas dans s1")
if 'yz' not in s1:
    print("'xz' n'est pas dans s1")
# et finalement on peut les découper ('slicer')
print(f"les 2 premiers caracteres s1[:2] {s1[:2]}")
print(f"tous les caracteres sauf le dernier s1[:-1] {s1[:-1]}")
print(f"tous les caracteres sauf le premier s1[1:] {s1[1:]}")
print(f"les caracteres a l'envers' s1[::-1] {s1[::-1]}")
# LES STRINGS SONT IMMUABLES, on ne peut pas les changer
# PAS COMME LES LISTES
# MAIS COMME LES TUPLES. Essayons s2[0] = 'z'
s2[0] = 'z'
```

Les chaînes de caractères ont aussi tout une collection de méthodes pour les manipuler. Voici les plus populaires données en exercices.
Exercices:
En utilisant l’information dans la documentation python à:
https://docs.python.org/3/library/stdtypes.html?highlight=set#string-methods

Complète le programme de la page suivante:

### Exercices

```PYTHON
# Programme à compléter (copier le programme dans pycharm)
def section(title):
    print("="*80)
    print(title)
s = 'maurice arNOLD'
section("CHANGEMENT DE CASE")
print(f"s = {s}")
# imprime s en majuscule .upper()
# met ton code sous le commentaire. Par exemple: print(f"s.upper() = {s.upper()}")
# imprime s en minuscule .lower()

# imprime s avec seulement la premiere lette en majuscule .capitalize

# imprime s avec la premiere lettre de chaque mot en majuscule .title()

section("TROUVER UN SOUS-STRING DANS UNE STRING")
# # Ne jamais oublier que les strings sont des sequences
# # et que l'on peut utiliser les fonctionnalités des sequences
# Est-ce que la chaine ‘au’ est dans s (in)

# Est-ce que la string commence par la lettre ‘a’ .startswith

# Est-ce que la string commence par la lettre ‘m’ .startswith

# Est-ce que la string commence par la lettre ‘a’ a l’index 1 .startswith

# Est-ce que la string commence par les lettres ‘au’ a l’index 1  .startswith

# Est-ce que la string termine par les lettres ‘au’ .endwith

# # les fonctions find, rfind retourne le premier index ou la sous-string
# # a été trouvé ou -1 si non trouvé
# Quel est le premier index de la string ‘a’ dans s .find

# Quel est le dernier index de la string ‘a’ dans s .rfind

# Quel est le premier index de la chaine ‘z’ find

section("JOINDRE ET SEPARER (.join et .split)")
s = "Autrefois le rat des villes Invita le rat des champs"
print(f"s = {s}")
# faire une liste des morceaux de s entre les espaces split()

# faire une liste des morceaux de s separes par le mot rat split()

# #ET la methode inverse .join(sep)
l = s.split(' ')
print(f"l = {l}")
# joindre la liste l en une string en ajoutant les espace .join

# Joindre les items de l sans ajouter quoique ce soit. .join

l = s.split('rat')
print(f"l = {l}")
# Joindre les items de l en ajoutant chat entre les items join

section("REPLACE")
print(f"s = {s}")
# remplace les ‘rat’ par des ‘chat’ dans la string s .replace
```