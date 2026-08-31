# Filtres MongoDB

Filtres de recherche dans Compass, sur la base de données

## Recherche via requête (onglet Documents)

`$lt` : permet de chercher quelque chose inférieur à la valeur donnée (lower than)

Exemple :

```json
created_at: {
  $lt: ISODate("2026-07-17T00:00:00.000Z")
},
```

Remarque : la variante `$lte` permet d’inclure le jour courant (lower than or equals, inférieur ou égal)

`$exists` : vérifier existance d’une clé (ou `$ne: null`)

`$ne: []` : vérifier qu’un tableau n’est pas vide (not equals)

```json
"payload.ble_beacons": {
  $exists: true,
  $ne: []
}
```

## Aggrégations (onglet Aggregations)

Sélectionner l’option TEXT (c’est STAGES par défaut)

Vérifier la présence de doublons dans ble_beacons (ici pour les trames Digital Matter), en insérant :

```json
[
  {
    $match: {
      "payload.timestamp": { $exists: true },
      "payload.ble_beacons": {
        $exists: true,
        $ne: []
      }
    }
  },
  {
    $unwind: "$payload.ble_beacons"
  },
  {
    $group: {
      _id: {
        ident: "$payload.ident",
        timestamp: "$payload.timestamp",
        beacon_id: "$payload.ble_beacons.id"
      },
      occurrences: { $sum: 1 },
      records: {
        $push: {
          document_id: "$_id",
          record_seqnum: "$payload.record_seqnum",
          created_at: "$created_at",
          server_timestamp: "$payload.server_timestamp",
          rssi: "$payload.ble_beacons.rssi",
          state: "$payload.ble_beacons.state"
        }
      }
    }
  },
  {
    $match: {
      occurrences: { $gt: 1 }
    }
  },
  {
    $group: {
      _id: {
        ident: "$_id.ident",
        timestamp: "$_id.timestamp"
      },
      duplicate_beacons: {
        $push: {
          beacon_id: "$_id.beacon_id",
          occurrences: "$occurrences",
          records: "$records"
        }
      },
      duplicate_count: { $sum: 1 }
    }
  },
  {
    $sort: {
      "_id.timestamp": -1
    }
  }
]
```

Le résultat se trouvera à droite, sous **Pipeline Output**