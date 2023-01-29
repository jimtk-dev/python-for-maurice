---
title: APPRENRE PYTHON
author: Jean-Michel Talbot
previewWebRootPath: D:/source/Maurice/Documents/
---

# CHAPITRE 01: REQUIS

> Contenu
>> Projet & Programmation: Les Requis.

## 0 Diagramme
:memo: LE DIAGRAMME SE TROUVE A LA FIN DU DOCUMENT

Dès qu’un programme offre plus que 2 ou 3 fonctionnalités je me fais un diagramme des requis. C’est simple à faire (le tien m’a pris 15 minutes) et ça me permet de pas me perdre. ET en le faisant ça me donne des idées de fonctionnalités à ajouter ou à enlever ou à grouper. Si tu as une imprimante ça vaut la peine de l’imprimer pour pouvoir faire des ajouts et corrections dès que l’idée t'en vient.

Officiellement ce type de diagramme fait partie de UML (Unified Modeling Language) et c’est officiellement le format du digramme des cas d’utilisations («USE CASE»).

C’est un diagramme extrêmement important: C’EST TA ‘CHECKLIST’ DE CE QUE TU DOIS FAIRE.

## 1. Détail Diagramme

Le petit bonhomme c’est l’usager. Dans d’autres programmes il peut y en avoir plusieurs qui ont des rôles différents et accès à des fonctionnalités différentes. Par exemple dans une application pour l’école tu pourrais avoir un usager élève, un parent et un professeur.

La grande boite rectangulaire marquée «SYSTEM» c’est ton application.

Chaque bulle représente une fonctionnalité que tu dois offrir que l’on appelle un cas d’utilisation (Use Case).Comme tu vois sur le diagramme il y a 4 fonctionnalités qui sont offertes directement à l’usager (pointes le sur le document pour activer la lecture active!):

- Choisir un fichier
- Choisir le format de conversion (a quoi l’usager veut convertir ce fichier)
- Lancer la conversion
- Quitter l’application

Toutes les autres fonctionnalités sont aussi des choses que ton logiciel doit offrir mais qui sont utilisées indirectement par l’usager. Exemple, la fonctionnalité «garder et fournir répertoire courant» est une fonctionnalité assez standard dans toutes les applications. Quand l’usager ouvre un fichier une première fois il navigue à un répertoire et choisi un fichier. La deuxième fois qu’il le fait, pour lui sauver du temps, on l’amène directement au même répertoire qu’il avait choisi précédemment pour lui éviter de refaire toute la navigation.

ATTENTION: CE DIAGRAMME NE DIT JAMAIS «COMMENT» FAIRE. IL DIT «QUOI» FAIRE.

Des fois on triche très légèrement! Par exemple la fonctionnalité «Gérer Cancel» force un peu la présence d’un bouton «cancel». Ça dit un peu comment le faire, mais la fonctionnalité est importante: quand l’usager appuie sur cancel, rien ne doit se produire, on revient à la fenêtre principale sans aucun message d’erreur ou changement de mode.

Pour donner une idée, les grosses application d'affaires ont souvent  plus de 100 bulles de fonctionnalités, et chaque bulle demande de 1 à 10 pages de documentation de la fonctionnalité requise.

Étudie bien ce diagramme, il y a peut-être manques dedans, et fait les corrections nécessaires (même à la main avec un crayon (si tu ne veux pas te battre avec Visio) et envoie-moi une photo du résultat si tu changes quelque chose.

Les meilleurs outils pour faire ce type de diagramme sont: Microsoft Visio et Libreoffice draw (qui me donnent des maux de têtes des fois!).

![DIAGRAMME DES REQUIS](Assets/Requis.png)