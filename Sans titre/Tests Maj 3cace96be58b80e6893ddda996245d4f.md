# Tests Maj

Les tests sont conduits sur l’instance dev.charlie.

**Pour prendre un des retours en compte :**

- créer une branche de fix depuis la branche de **DEV**
- noter votre **NOM** à la fin du commentaire en gras
- barrer le commentaire quand vous l’avez fixé
- **export** :
    - ~~capteur/tracker/qrcode : ca n’exporte pas que les capteur de la filiale que j’ai sélectionné, la ca exporte aussi les capteurs des autres filiales
    ⇒ niveau 1 : exporter que la connectivité du client de l’utilisateur
    ⇒ niveau 2 : exporter la connectivité du client non associé + la connectivité associé aux filiales sélectionné dans son select~~
    - ~~Matériel/zone : il manque les colonnes latitude/longitude dans les exports~~
- **~~carte** : on a encore le bouton “Contrôler” au lieu du bouton Exporter sur la modale de mouvement (ca fait lgtps qu’on l’avait changé ca pourtant)~~
- **Une zone qui a une position fixe reçoit des inventaires :** sur son détail on voit bien dans sa modale historique mouvement sa position de détection (différente de la position fixe dans mon cas)
    
    => par contre sur la carte aucun historique de mouvement apparait :
    
- **~~Zone avec position fixe :** elle fait un inventaire avec une adresse de détection différente de celle de la position
=> les matériels qui sont inventoriés doivent apparaitre à la position fixe de la zone : au niveau de leur adresse de détection, de leur modale historique mouvement etc…~~