# Historiques

# Types de champs historisés

Les historiques sont générés à chaque création, édition ou suppression d’élément.

## Matériel / Zone / Site

### Ce qui est affiché

Ce qui est affiché sur la page de détail des assets, onglet **Activité** :

- Changement sur chaque champ (un ou plusieurs) tels que réf interne, commentaire
- Tout ce qui finit par ID (changement d’ID de clé étrangère) : capteur/tracker rattaché, changement de type, d’état de conformité/suivi, de QR code..
    - Changement du `LastMovementInventoryAssetId` lors d’un nouvel inventaire
    - Changement de filiale (par le biais du type)
- Tout ce qui finit par CODE : `statusCode`
- Historiques des contrôles réalisés (finalisés)

### Ce qui n’est PAS affiché actuellement

- Changement sur les dates de détection (`detectionDate`) des matériels et zones

### Identification des champs non nécessaires

- Mouvement de l’asset (`lastMovementInventoryAssetId`)
- Par défaut, tous les historiques liés à l’asset semblent récupérés (`MaterialsController`) :

```php
$activities = $material->histories()->orderBy('created_at', 'desc')->get();
$controlActivities = $material->controls()->with(['histories' => function ($query) {
     $query->where('source', 'lastControlManagement');
}])->orderBy('created_at', 'desc')->get();
$histories = $controlActivities->pluck('histories')->flatten();
```

### Propositions

- **Récupérer uniquement les modifications manuelles, donc ceux où `created_by` ou `updated_by` n’est pas nul**
⇒ ne pas afficher tout ce qui est lié à la détection
⇒ 2ème temps : les alertes doivent être affichées (action système)
- Filtrer par date et récupérer les X dernières activités seulement
- “Paginer” le résultat et en afficher X par page, avec un bouton “Voir plus” pour charger

## Clients principalement concernés

- VCGP UK (timeout)

# Format de stockage

Format type des historiques :

```json
{
  "_id": {
    "$oid": "67a36a641e655a5eba0ed73e"
  },
  "materialId": 72,
  "action": "updated",
  "source": "",
  "before": {
    "id": 72,
    "internalReference": "02BureauLille",
    "isFixed": false,
    "statusCode": "201",
    "buyingDate": null,
    "lastMovementDate": "2024-11-29 17:48:11",
    "comment": null,
    "siteId": null,
    "typeId": 1,
    "stateId": null,
    "conformityId": 1,
    "sensorId": 223,
    "trackerId": null,
    "zoneId": null,
    "qrCodeId": null,
    "teamId": null,
    "created_at": "2023-06-28 18:55:13",
    "updated_at": "2025-02-05 11:36:23",
    "deleted_at": null,
    "created_by": null,
    "updated_by": null,
    "deleted_by": null
  },
  "after": {
    "isFixed": 0,
    "zoneId": 531,
    "updated_at": "2025-02-05 13:40:50",
    "updated_by": 212
  },
  "created_at": {
    "$date": "2025-02-05T13:40:52.953Z"
  },
  "updated_at": {
    "$date": "2025-02-05T13:40:52.953Z"
  }
}
```

Interprétation : le champ zoneId a été mis à jour avec la valeur 531 par l’utilisateur 212.