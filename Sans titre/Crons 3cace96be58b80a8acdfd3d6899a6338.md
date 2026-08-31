# Crons

Les notifications sont déclenchées via les alertes configurées sur l’utilisateur cible de type : geofencing ou perdu/retrouvé ou dans le récapitulatif journalier, et lorsque l’utilisateur est connecté sur l’application Gestion.

# Notifications Push

Méthode d’envoi : `sendPushNotification`  dans `NotificationManager`

Paramètres : titre, corps (contenu), jeton firebase, identifiant d’objet, type de notification / object

Envoyées par les alertes Geofencing et Retrouvé

## Geofencing

### Logique

- Si j’ai un seul asset, son ID est passé dans objectId, et le type sera `geofencing`
- Si plusieurs assets geofencés, pas d’ID d’objet passé, et le type sera `geofencing`
    - Variante proposée : passer un array `objectIds` contenant l’ensemble des assets retrouvés (parsé en string dans la data transmise), puis décortiqué côté mobile, et filtrer dessus.
    ⇒ Peut être fait dans une version ultérieure

### Redirection

- Un seul asset : on redirige sur son détail
- Plusieurs assets : on envoie sur la liste des assets concernés

### Paramètres

#### Actuel

| title | Alerte géofencing (traduit) |
| --- | --- |
| body | Contenu textuel généré dynamiquement (et traduit) |
| data | { |

```
‘`id`’ : $objectId ?? 1,
‘`type`’ : $type ?? null
```

} |

| deviceToken | Jeton du client |

#### Souhaité

| title | Alerte géofencing (traduit) |
| --- | --- |
| body | Contenu textuel généré dynamiquement (et traduit) |
| data | { |

```
‘`inputMaterialIds`’ : ‘1,2,3’,
‘`outputMaterialIds`’ : ‘4,5’,
‘`inputZoneIds`’ : ‘1’,
‘`outputZoneIds`’ : ‘’,
‘`type`’ : ‘geofencing’
```

} |

| deviceToken | Jeton du client |

## Retrouvé

### Logique

- Si j’ai un seul asset retrouvé, son ID est passé dans objectId, et le type sera `found`
- Si j’ai plusieurs assets retrouvés, pas d’ID d’objet passé, et le type sera `found`
    - Variante proposée : passer un array `objectIds` contenant l’ensemble des assets retrouvés (parsé en string dans la data transmise), puis décortiqué côté mobile, et filtrer dessus.
    ⇒ Peut être fait dans une version ultérieure

### Redirection

- Un seul asset : on redirige sur son détail
- Plusieurs assets : on redirige sur la liste des assets ?

### Paramètres

#### Actuel

| title | Alerte retrouvé (traduit) |
| --- | --- |
| body | Contenu textuel généré dynamiquement (et traduit) |
| data | { |

```
‘`id`’ : $objectId ?? 1,
‘`type`’ : $type ?? null
```

} |

| deviceToken | Jeton du client |

#### Souhaité

| title | Alerte retrouvé (traduit) |
| --- | --- |
| body | Contenu textuel généré dynamiquement (et traduit) |
| data | { |

```
‘`materialIds`’ : ‘1,2,3’,
‘`zoneIds`’ : ‘1’,
‘`type`’ : ‘found’
```

} |

| deviceToken | Jeton du client |

## Récap journalier (mailDaily)

### Logique

Pas d’utilisation de assetsIds, type `dailyRecap` ?

### Redirection

Pas de redirection : accueil (homeScreen)

### Paramètres

#### Actuel

| title | Alerte ! (traduit) |
| --- | --- |
| body | Vous avez reçu :alertsCount alertes sur vos assets aujourd\'hui. (traduit) |
| data | { |

```
‘`id`’ : $objectId ?? 1,
‘`type`’ : $type ?? null
```

} |

| deviceToken | Jeton du client |

#### Souhaité

| title | Alerte ! (traduit) |
| --- | --- |
| body | Vous avez reçu :alertsCount alertes sur vos assets aujourd\'hui. (traduit) |
| data | { |

```
‘`type`’ : ‘dailyRecap’
```

} |

| deviceToken | Jeton du client |

## Décisions

Ouvre directement le détail de la notif, avec un slider pour le mobile, et affiche la notif avec 2 boutons pour le WEB

⇒ les listes de mat/zone seront pré-filtrées

Table notifications :

- Avoir un nouveau champ `data` (json) qui contiendrait la liste des identifiants d’assets à notifier (mat/zone) et des liens vers les pages de détail, et un nouveau champ optionnel `type`
- Geofencing
    - `inputMaterialIds` (/materials) : matériel(s) entré(s) sur le site
    - `outputMaterialIds` (/materials) : matériel(s) sorti(s) du site
    - `inputZoneIds` (/zones) : zone(s) entrée(s) sur le site
    - `outputZoneIds` (/zones) : zone(s) sortie(s) du site
- Retrouvé :
    - `materialIds` : matériel(s) retrouvé(s)
    - `zoneIds` : zone(s) retrouvée(s)
- Côté web : 2 boutons au max, on a le site de détection pour distinguer
    - Les liens vers les détails sont générés à partir des listes d’assets
- Côté mobile : on différencie les onglets matériel/zone (slider)

# Notifications locale (table BDD)

Créées via le job MailDaily (fonction sendNotifications)

| userId | ID de l’utilisateur notifié |
| --- | --- |
| title | Titre de la notif (traduit) |
| content | Contenu de la notif (dynamique et traduit) |
| url | Eventuel lien de redirection (page matériels..) |