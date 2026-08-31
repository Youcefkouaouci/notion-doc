# Inventaires retardés

Un inventaire peut être décalé si un tracker est à court de batterie ou ne dispose pas de connexion réseau. De même, sur les inventaires mobiles, l'absence de réseau peut également provoquer un décalage.

Un inventaire peut être décalé dans plusieurs cas : lorsque sa date de détection est postérieure à sa date d'inventaire, ou lorsqu'il s'agit d'un inventaire décalé mais que sa dernière position enregistrée est antérieure à la date d'inventaire.

Les champs à mettre à jour dans la base de données varient selon les situations :

- **Cas 1** : Lorsque la date de détection et la dernière position de l'équipement sont postérieures à la date d'inventaire.
- **Cas 2** : Lorsque la date de détection est postérieure à la date d'inventaire, mais que la dernière position enregistrée est antérieure.

⚠️ SI IL N’Y A PAS DE UPDATE, IL N’Y AURA PAS D’HISTORIQUE DE CRÉE

Il peut y avoir des erreurs à cause des historiques qui s’insère automatiquement avec les observers. Il faut peut etre essayer pour Location uniquement, de l’ajouter la bonne date avec la fonction recordOldHistory

### CAS 1 :

On ne fait pas le traitement sur le geofencing et sur l’alerte de mouvement

- **Current inventories**
    - On ne met pas à jour l’inventaire actuel
- **Sensors/Trackers**
    - On ne met pas à jour sa batterie
- **Zones**
    - lastMovementDate → 🛑
    - statusCode → 🛑
    - siteId → 🛑
- **Matériels**
    - lastMovementDate → 🛑
    - statusCode → 🛑
    - siteId → 🛑
    - teamId → 🛑
    - zoneId → 🛑
- **Locations**
    - time → 🛑
    - latitude → 🛑
    - longitude → 🛑
    - trackerId → 🛑
    - sensorId → 🛑

### CAS 2 :

Le traitement sur le geofencing du site et sur l’alerte de mouvement

- **Current inventories**
    - On ne met pas à jour l’inventaire actuel
- **Sensors/Trackers**
    - On ne met pas à jour sa batterie
- **Zones**
    - lastMovementDate → ✅
    - statusCode → ✅
    - siteId → ✅ **( GEOFENCE + MISE À JOUR DU SITE ACTUELLE )**
- **Matériels**
    - lastMovementDate → ✅
    - statusCode → ✅
    - siteId → ✅ **( GEOFENCE + MISE À JOUR DU SITE ACTUELLE )**
    - teamId → 🛑
    - zoneId → 🛑
- **Locations →** 🛑
    - time → ✅ ( INCORRECT )
    - latitude → ✅ ( INCORRECT )
    - longitude → ✅ ( INCORRECT )
    - trackerId → ✅ ( INCORRECT )
    - sensorId → ✅ ( INCORRECT )
- **Historique**
    - time → ✅
    - latitude → ✅
    - longitude → ✅
    - trackerId → ✅
    - sensorId → ✅