# CHAPITRE 02 DESIGN

+------------------------------------------------------+
|**Contenu**
| - Projet & Programmation: Design d’une application.
+------------------------------------------------------+

## 0. Diviser Pour Régner
Avant de commencer le design il y a UN principe de programmation très important qu’il faut connaître et comprendre à fond pour bien faire les choses.

Le principe le plus important: **DIVISER POUR RÉGNER**.

Il faut découper et compartimentaliser les fonctionnalités de façon à ce qu’elles puissent fonctionner sans affecter OU CONNAÎTRE ce qui se passe dans le reste du code. (Relis ça 10 fois, tous les jours, pendant une semaine! Jusqu’à ce que cela fasse partie de ta personnalité profonde).

Un bon exemple dans notre projet: la fonctionnalité ‘JSON-to-DB’. Cette partie du code n’a pas besoin de savoir à quoi ressemble l’interface graphique et ne doit pas affecter l’interface graphique (ex: changer des «labels»). JSON-to-DB a besoin de 2 noms de fichiers (un pour la lecture l’autre pour l’écriture). Elle devrait recevoir cette information en paramètres et ne rien connaître d’autre. Elle est capable de faire son travail sans aucune autre information.

POURQUOI FAIRE DE CETTE FAÇON?

- Pour pouvoir micro-manager chaque portion de code indépendamment des autres.
- Pour pouvoir écrire le code plus facilement. Quand t’as pas à penser au niveau global dans chaque fonction cela devient beaucoup plus simple. On se concentre sur une fonctionnalité et on oublie le reste. Cela rend le travail beaucoup plus facile.
- Pour faciliter la gestion des erreurs dans le code. Si DB to JSON ne fonctionne pas, l’erreur est dans DB to JSON et pas ailleurs.
- Pour faciliter les changements majeurs de code. Aujourd’hui tu écris ton interface usager avec Tkinter. Demain tu deviens un bon programmeur, et tu décides de refaire l’interface avec PyQT6 (beaucoup plus puissant, beaucoup plus complexe, beaucoup plus beau). La fonction DB to JSON, si elle a été bien écrite n’as pas besoin d’être modifié. Après-demain tu deviens un programmeur très expérimenté et ton application doit rouler sur un serveur avec une interface web. DB to JSON n’as toujours pas besoin d’être modifiée. Tu la réutilises telle quelle sans aucun changement.
- POUR POUVOIR TESTER CHAQUE PETIT MORCEAU SÉPARÉMENT.
Pour chaque 10 minutes de programmation (code écris) il doit y avoir 30 à 40 minutes de test. ET oui c’est la réalité. La programmation c’est l’étude en profondeur de tout ce qui peut mal aller!

- Si on revient à DB to JSON il peut se passer les choses suivantes :

    - Le fichier a l’extension .DB mais il contient autre chose (du texte par exemple)
    - L’usager n’a pas accès à écrire dans le répertoire destination.
    - L’usager n’a pas accès à lire dans le répertoire destination.
    - Le fichier DB est corrompu
    - L’encodage UTF-8 n’est pas respecté.
    - Le fichier DB est vide
    - Le nom de la table dans le fichier DB n’est pas celui que l’on avait assumé.
    - Le nom du fichier donné en paramètre est un répertoire (ex: c:\\) et non un fichier.
    - ET plusieurs autres

- Il est infiniment plus facile de tester une petite fonction plutôt que d’essayer de tester le programme complet. Chaque petite fonctionnalité doit être solide et à toute épreuve avant de passer à la fonction suivante. Parce que la suivante dépend souvent de la précédente!

## 1. DESIGN

Il existe plusieurs TYPES de DESIGN. Le plus moderne (relativement) le plus simple et le plus utilisé est celui qui s’appelle Model  – Vue – Contrôleur (Model/View/Controller) ou simplement MVC.

Le but de MVC est de permettre d’implémenter le principe DIVISER POUR RÉGNER à très haut niveau dans le design. C’est-à-dire de séparer et compartimentaliser les groupes de fonctionnalités. Il le fait en divisant ces groupes de fonctionnalités en 3 groupes

### 1.1 Modèle

Ça c’est tes données. C’est tout ce qui doit «dealer» avec la lecture et l’écriture des données et des fichiers. Et il faut que ça soit complètement indépendant de tout le reste.

### 1.2 Vue

La vue c’est ton interface. C’est ce que l’usager voit. Et c’est sans doute la partie la plus importante a compartimentaliser parce qu’elle peut changer souvent et en profondeur.

### 1.3 Contrôleur.

Le contrôleur c’est le pont entre ton interface usager et tes données et c’est aussi dans cette section du design que réside l’intelligence d’affaire.

Évidemment il y a très peu d’intelligence d’affaire dans ton application puisque que l’on fait simplement de la conversion de fichiers. La gestion des règles de conversion est un exemple d’intelligence d’affaire. En plus, si, par exemple tu voulais ajouter à la base de données la distance en kilomètre entre la résidence du membre et le siège social (en utilisant les codes postaux) c’est la que des calculs résideraient.

Le contrôleur effectue souvent de la gestion interne des autres fonctionnalités et contient souvent des fonctions qui ne sont pas dans le diagramme des cas d’utilisations (celui avec le bonhomme et les bulles!). C’est du code pour gérer le code.

## 2. Détails Diagramme

Le design est principalement une division d’IDÉES et pas nécessairement une division du CODE. Surtout au niveau du contrôleur.

Un exemple concret. On va sans doute regrouper toutes les fonctionnalités de conversion (modèle) dans un seul module python (ex: `control.py`) et chacune auront leur propre fonction (ex: `def db_to_json():`). Mais une fois que tu as un nom de fichier source et un nom de fichier destination tu as toute l’information nécessaire pour choisir quelle fonctionnalité de conversion doit être utilisé (grâce aux extensions des noms de fichier). On pourrait mettre un « dispatcheur » qui regarde les extensions et appelle la bonne fonction de conversion. Ce « dispatcheur » est définitivement une fonctionnalité de type contrôleur, mais il se retrouvera dans le même module (ex: `model.py`) que le modèle parce qu’il est complètement indépendant du reste.

On peut aussi avoir un bout de contrôleur dans l’interface graphique pour gérer les changements d’états de l’interface graphique qui sont indépendants des autres sections du code.

## 3. Niveau de Design

Étant donné que notre application est très simple et est écrite en programmation fonctionnelle (pas d’objet) ce diagramme est suffisant pour nous orienter vers un bon design complet. Si la complexité augmente il existe toute une panoplie de diagrammes:  Class diagram, Package diagram, Object diagram, Component diagram, Activity diagram  et j’en passe, qui peuvent permettre de designer à très bas niveau lorsque c’est nécessaire. Visite des sites sur le langage UML pour en apprendre plus.

![DESIGN DE L'APPLICATION](Assets/Design.png)
