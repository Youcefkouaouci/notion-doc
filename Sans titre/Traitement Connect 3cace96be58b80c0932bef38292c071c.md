# Traitement Connect

# Trame globale générale

## Trame brute

Voici la trame type de donnée qui sera stockée lors de l’appel à l’API d’insertion des données provenant de Charlie Connect (ou communautaire) :

```json
{
  "manufacturer": "charlieConnectAndroid",
  "integrator": "Charlie",
  "payload": {
    "jsonVersion": 1,
    "appVersion": "2.4.0",
    "timestampRanging": "2025-11-19T15:18:41.137Z",
    "timestampInventory": "2025-11-19T15:20:57.587997Z",
    "isCommunautary": false,
    "informations": [
      {
        "number": "C ID 00BDB7",
        "latitude": 49.23034627921879,
        "longitude": 2.8916223999112844,
        "detectionDate": "2025-11-19T15:19:12.379Z",
        "timestampGps": "2025-11-19T15:19:05.607Z"
      },
      {
        "number": "C ID 00BDB6",
        "latitude": 49.23026933334768,
        "longitude": 2.8915502317249775,
        "detectionDate": "2025-11-19T15:19:22.536Z",
        "timestampGps": "2025-11-19T15:19:15.553Z"
      }
    ]
}
```

## Explication des champs

- `informations` contient la liste des capteurs, eux-mêmes sous forme d’objets JSON. Leur clé est le numéro du capteur, et leur valeur un ensemble de données :
    - `detectionDate` : dernière date de détection sur l’antenne du capteur
    - `timestampGps` : timestamp de la dernière localisation acquise et associée au capteur
    - `latitude` : latitude rattachée au capteur
    - `longitude` : longitude rattachée au capteur
    - `batteryVoltage` : voltage remonté par le capteur, en millivolts (mV)
    - `battery[Value]` : valeur de batterie, en pourcentage
    - `nbFrames` : nombre de frames/émissions remontées par le capteur de type MOV
    - `nbMoves` : nombre de fronts montants au dessus du seuil d’accélération défini (en mG) remontés par le capteur de type MOV
- `jsonVersion` : version du fichier JSON courant
- `appVersion` : version de l’application qui a transmis la donnée (débogage)
- `timestampRanging` : timestamp de début du ranging (débogage)
- `timestampInventory` : timestamp de l’appel à l’API d’envoi des données (débogage)
- `createdAt` : timestamp déterminant l’insertion physique de la ligne sur la DB
- `updatedAt` : date de mise à jour de la ligne de donnée (traitement)
- `statusCode` : code qui détermine le statut de traitement de la ligne
- `isCommunautary` : booléen qui détermine si la trame provient du réseau communautaire ou non

## Variante 1 : Géolocalisation dans la trame

Contenu du champ `informations` :

```json
{
  "P ID 015367":
  {
    "detectionDate":"2024-11-26 17:54:11.503",
    "latitude":50.6338716,
    "longitude":3.0215714,
    "batteryVoltage":3087
  },
  "L ID 005C90":
  {
    "detectionDate":"2024-11-26 17:54:11.503",
    "latitude":50.6338716,
    "longitude":3.0215714
  },
  "C ID 003F6F":
  {
    "detectionDate":"2024-11-26 17:54:11.503",
    "latitude":50.6338716,
    "longitude":3.0215714,
    "batteryVoltage":2949
  },
  "C MOV 123456":
  {
	  "detectionDate":"2024-11-26 17:54:11.503",
	  "nbFrames": 12876,
	  "nbMoves": 123
  }
}
```

## Variante 2 : Aucune géolocalisation dans la trame

Contenu du champ `informations` :

```json
{
  "P ID 015367":
  {
    "detectionDate":"2024-11-26 17:54:11.503",
    "batteryVoltage":3087
  },
  "L ID 005C90":
  {
    "detectionDate":"2024-11-26 17:54:11.503",
  },
  "C ID 003F6F":
  {
    "detectionDate":"2024-11-26 17:54:11.503",
    "batteryVoltage":2949
  },
  "C MOV 123456":
  {
	  "detectionDate":"2024-11-26 17:54:11.503",
	  "nbFrames": 12876,
	  "nbMoves": 123
  }
}
```

# Clés RSA nécessaires

Pour l’ensemble des clés RSA, de production et de test, que ce soit la privée ou publique, consultez les notes dans Lastpass.