# CHAPITRE 8.5 : Algorithme Ascenseur
> Contenue:
> - INFORMATIQUE - Algorithmique

Le but de cet exercice est de trouver ou de créer l'algorithme employé par un ascenceur.

```
LES ENTRÉES DE DONNÉES:
  - Mur a l’étage - REQUÊTE de monter (étage de la demande)
  - Mur a l’étage - REQUÊTE de descendre (étage de la demande)
  - Dans la cabine - DEMANDE un étage

L’ASCENSEUR A TROIS MODES:
  - Mode Monter
  - Mode Descendre
  - Mode Arrêter à l’étage 1

L’ASCENSEUR A SERIE D'ACTIONS AUTOMATIQUES (à chaque étage d'arret):
  - Si arrivé à un étage demandé ou requis: ouvre la porte pendant 20 secondes.
  - Éteindre les boutons de demande.
  - Éteindre le bouton de requete dans la direction du mode.

MODE MONTER
   - Embarquer ceux qui veulent monter
   - Monter au plus haut étage demandé
   - Rester en mode monter jusqu'a la plus haute requete (monter ou descendre)
   - Si aucune requete de descendre
        Retourner à l'étage 1
   - sinon
        Passer en mode descendre

MODE DESCENDRE
   - Embarquer ceux qui veulent descendre
   - Aller aux plus bas étage demandé
   - Rester en mode descendre jusqu'a la plus basse requete (monter ou descendre)
   - Si aucune requete de monter
         Retourner à l'étage 1
   - Sinon
         Passer en mode monter

EN MODE ARRETER A L'ETAGE 1
   - Attendre requete
   - Si requete monter
        passer en mode monter
   - Si requete de descendre    # si l'étage 1 n'est pas le plus bas
        passer en mode descendre
```