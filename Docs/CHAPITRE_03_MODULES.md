---
title: CHAPITRE 2 DESIGN
author: Jean-Michel Talbot
previewWebRootPath: D:/source/Maurice/Documents/
---

# CHAPITRE 3 - MODULES


> **Contenu:**
> * Python: Modules
> * Python: main()


## 0. Glossaire

- **CL**: Command line. Ligne de commande du système d'opération. C'est le prompt de la fenêtre de commande DOS.

## 1. Référence

C'est le site officiel: [****https://docs.python.org/3.8/library/index.html****](https://docs.python.org/3.8/library/index.html)

Tout est là, ce n'est pas trop aride, Il y a beaucoup d'exemples et ça explique comment faire les choses comme il le faut. Il y a un «search box» en haut à droite. __Tout le reste de ce que tu peux lire sur
internet a été pris dans ce document__. Alors va à la vraie source et
sers toi-z-en.

## 2 Modules

C'est quoi un module? Un module python c'est un fichier python (avec
extension .py) qui contient du code et des variables (le moins possible de variables!). Il peut être exécuté à partir de la ligne de commande (CL) (ou à l'intérieur d'un IDE). Il peut aussi être importé par un autre module python.

Quand il est appelé de la CL tout le code qui est accoté à gauche est
exécuté en premier. Quand il est importé par un autre module tout le
code qui est accoté à gauche est exécuté au moment de l'import. C'est la raison pour laquelle on ne met jamais de code accoté à gauche.

Comme on veut avoir un meilleur contrôle de l'exécution ***TOUT LE CODE EST PLACÉ DANS DES FONCTIONS.***

Ensuite on écrit une fonction main() qui contrôle l'exécution de toutes les autres fonctions. Et finalement on appelle la fonction main() seulement si le nom du module est celui qui est appelé sur la CL.

Pour vérifier que le module est appelé sur la ligne de commande on
vérifie la valeur de la variable interne de python : `__name__` .
Quand le module est appelé sur la CL la variable `__name__` est égale à `__name__`. Quand le module est importé par un autre module la variable `__name__` sera égale au nom du module lui-même.
Donc un bon module Python ressemble à ça:

``` python
# module a.py

def addition(a, b):
    return (a + b)

def main():
    r = addition(3, 4)
    print(r)

if __name__ == '__main__':
    main()
```

Si j'écris un module `b.py` qui importe `a.py` et que j'exécute `b.py` à partir de la ligne de commande. La fonction `main()` de `a.py` ne sera jamais exécuté parce que dans `a.py __name__` sera égal à `a`.

```PYTHON
# b.py

import a

def main():
    res = a.addition(10,20)
    print(res)

if __name__ == '__main__':
    main()
```

## 3 Exercices

Démarrer Pycharm et y écrire les deux fichiers précédents. ***PAS DE CUT & PASTE*** écrit les fichiers caractères par caractères et sauves les dans le même répertoire (n' importe où), C'est comme ça qu'on apprend.

À partir de la ligne de commande (ou à l'intérieur de PyCharm en faisant
Shift-F10 ou cliques dans l'éditeur avec le bouton de droite et clique sur 'RUN') lance le programme a.py.

Remarque les choses suivantes:

1.  La première ligne qui a été exécuté est `print(f''modul a.py et __name__ ... `. Ca confirme que le code accoté à gauche est exécuté tout de suite avant même que le compilateur lise le reste du module.
2.  La valeur de `__name__` est 'main'
3.  Le résultat est 7, ce qui veut dire que python a lu tout le module   et a exécuté la 2ième ligne accotée à gauche `if __name__ == 'main'):` et a exécuté la fonction main(), qui elle a exécuté la fonction addition(3,4), mis le résultat dans la variable r et l'a imprimé à l'écran.

À partir de la ligne de commande (ou a l'intérieur de PyCharm) lance le
programme b.py

Remarque les choses suivantes:

1.  La ligne `module a.py et __name__ = ...` est exécuté en premier ! Tu lances le module b.py et la première ligne qui roule vient de a.py! Sans que tu l'aie appelé. Ça c'est le genre de chaos infernal que l'on veut éviter à tout prix et la raison pour laquelle on ne met pas de code accoté a gauche.
2.  Le résultat de cette ligne est aussi très intéressant. Dans le     module a.py la variable `__name__` est égale à 'a'. Donc quand python va exécuter la ligne : `if __name__== 'main'` du module a.py, la condition est fausse, et la fonction `main():` de a.py ne sera jamais appelée.
3.  Après avoir exécuté la ligne de a.py python exécute ensuite la  première ligne accotée à gauche de b.py et le résultat est que la variable `__name__` de b est égale à 'main'.
4.  Donc le main() de b.py sera exécuté et que fait-il? Il appelle la fonction d'addition de a.py avec les paramètres 10 et 20, a.addition fera le calcul et retourne le résultat (30) qui sera mis dans la variable `res` et finalement imprimé à l'écran.
5.  Il faut aussi s'intéresser à ce qui ne s'est pas produit! La     fonction main de a.py n'a jamais été exécutée. On aurait pu écrire n'importe quoi comme code dans la fonction main() de a.py et il ne sera jamais exécuté! Gardes ça dans ta manche on va s'en servir tantôt.

