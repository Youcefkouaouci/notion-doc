# Traitement MQTT

```json
{
  "topic": "2468101214161820",
  "messages": {
    "s": "GT:2468101214161820",
    "ts": "2024-12-02T08:00:00.0Z",
    "m": "init_model",
    "loc": [
      23.987654,
      48.987654
    ],
    "v": {
      "ID_FRAME": {
        "value": "id:3"
      },
      "temperature": {
        "value": 10,
        "unit": "degC"
      },
      "battery": {
        "value": 3.967,
        "unit": "V",
        "remaining": 0
      },
      "GPS": {
        "validPosition": 1,
        "speed": {
          "value": 0.05,
          "unit": "kmh"
        },
        "onMove": 16
      },
      "network": {
        "rsrp": -80,
        "rsrq": -13
      }
    }
  },
  "statusCode": 100,
  "created_at": "2024-12-04T16:09:01.369Z",
  "updated_at": null
}
```

## Explication des champs

- `topic` contient le numéro du tracker
- `messages` : contient les informations renvoyées par le tracker
    - `s` : information sur le type de trame ( ici GT → tracker ) + numero du tracker
    - `ts` : date de scan du tracker
    - `m` : model ( utilisé uniquement pour le débogage )
    - `loc`
        - *latitude*: Latitude du tracker
        - *longitude*: Longitude du tracker
    - `v` :
        - `ID_FRAME` : ID de la trame
            - `value` : unique par trame tracker → sert à récupérer les trames capteurs
        - `temperature` : température renvoyée par le tracker
            - `value` : Valeur
            - `unit` : Unité d’envoie
        - `battery` : battery renvoyée par le tracker
            - `value` :
            - `unit` : Unité
            - `remaining` : battery en pourcentage
        - `GPS` :
            - `validPosition` :
            - `speed` :
                - `value` :
                - `unit` :
            - `onMove` : status du mouvement
            
            ```
                    16  => 'En mouvement',
                    128 => 'Stop mouvement',
                    132 => 'Début mouvement',
                    138 => 'Choc',
            ```
            
        - `network` :
            - `rsrp` :
            - `rsrq` :
- `statusCode` : code qui détermine le statut de traitement de la ligne
- `createdAt` : timestamp déterminant l’insertion physique de la ligne sur la DB
- `updatedAt` : date de mise à jour de la ligne de donnée (traitement)

```json
{
  "topic": "2468101214161820",
  "messages": {
    "s": "CP:354679092915795",
    "ID_FRAME": "id:865",
    "ble_payload": [
        "P ID 01A050;0;0;-63;",
        "C ID 019D50;0;0;-84;",
        "C MOV 076541;0;0;-78;6FF5707F2500A0C095020494420303043454130",
    ]
  },
  "statusCode": 100,
  "created_at": "2024-12-04T16:09:01.369Z",
  "updated_at": null
}
```

## Explication des champs

- `topic` contient le numéro du tracker
- `messages` : contient les informations renvoyées par le tracker
    - `s` : information sur le type de trame ( ici CP → capteur ) + numero du tracker
    - `ID_FRAME` : ID de la trame ( C’est le même ID de la trame tracker )
    - `ble_payload` :
        - *numeroCapteur*;*battery*;*battery*;*rssi*;*batteryVoltage*
- `statusCode` : code qui détermine le statut de traitement de la ligne
- `createdAt` : timestamp déterminant l’insertion physique de la ligne sur la DB
- `updatedAt` : date de mise à jour de la ligne de donnée (traitement)