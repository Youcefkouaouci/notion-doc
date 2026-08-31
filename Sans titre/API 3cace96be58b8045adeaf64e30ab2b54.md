# API

Brands :

- Le nom d’une marque doit être unique pour le même modèle (matériel, zone, etc)
- Une marque doit avoir au moins un des champs ‘isForZone’, ‘isForMaterial’, ‘isForTracker’, ‘isForSensor’ à true

Format :

- Le nom d’un format doit être unique pour le même modèle (capteur, tracker, etc)
- Un format doit avoir au moins un des champs ‘isForSensor, ‘isForTracker’ à true

Materials :

- La référence interne doit être unique dans la même filiale
- Le code de statut doit appartenir au modèle matériels

Groups :

- Le nom d’un groupe doit être unique dans la même filiale

GpsConfig :

- En construction… 👷🏻‍♂️

Periodicities :

- La valeur et unité d’un périodicité doit être unique dans la même filiale

QrCodes :

- Le code doit être unique

Sensors :

- Le numéro de capteur doit être unique
- Le code de statut doit exister pour le modèle capteur
- Soit isForZone, soit isForMaterial doit être true

Sites :

- La date de début doit être antérieure à la date de fin

States :

- Un état doit avoir au moins un des champs ‘isForZone’, ‘isForMaterial’, ‘isForTracker’, ‘isForSensor’, ‘isForConformity’ à true
- La couleur doit être une couleur hexadécimale : ‘#XXXXXX’

Status :

- Le code de status doit être unique par modèle
- La couleur doit être une couleur hexadécimale : ‘#XXXXXX’

Subsidiaries :

Teams :

- Le nom doit être unique dans la même filiale

Templates :

Trackers :

- Le numéro de tracker doit être unique
- Le code de statut doit exister pour le modèle Tracker

Types :

- Un type doit avoir au moins un des champs ‘isForZone’, ‘isForMaterial’, ‘isForTracker’, ‘isForSensor’, ‘isForSite’ à true
- Le nom du type doit être unique dans la même filiale

Users :

- L’adresse mail doit être unique

Zones :

- Impossible d’associer un capteur et un tracker à la fois
- Le tracker ne doit pas être associé à une autre zone
- Le capteur ne doit pas être associé à une autre zone / un autre matériel

# Matériel/zone

- Considérer les changements de capteur / tracker
    - Cas 1 : je n’avais pas de cp et j’en affecte un
    - Cas 2 : j’avais un cp et je le désaffecte
    - Cas 3 : je remplace mon cp par un autre (ou un tracker, et inversement)
- **Contrôles : les dates de contrôle ne sont pas dans le formulaire, donc cette partie n’est pas à prendre en compte pour le moment côté mobile**
- **EAV : pour le moment pas implémenté côté mobile
⇒ voir comment on récupère ça : append ou APIs ?**

# Matériel

## Store

- Matériel
- Si j’ai une localisation (basé sur adresse OU latitude ET longitude)
Location : `address`, `latitude`, `longitude`, `materialId`
- Si j’ai au moins une date de dernier contrôle (`lastControls`)
Itère et crée les Control : `object`, `objectId`, `controlFields` (vide), `controlSheetId`, `date`, `isDone` (true)
    - Si j’ai une alerte à contrôler ou en quarantaine : met à jour `conformityId`
- Si j’ai au moins un EAV
Eav : `object`, `objectId`, `eavs` (tableau de champs attribut ⇒ valeur), `subsidiaryId`

Retour de l’API : le matériel, la localisation et les EAV

## Update

- Matériel (uniquement les champs updatés)
- Si j’ai une localisation (basé sur adresse OU latitude ET longitude)
Location : `address`, `latitude`, `longitude`, `materialId`**Si je n’en ai plus, la supprimer de la table location**
- Si j’ai au moins une date de dernier contrôle (`lastControls`)
Itère et crée les Control : `object`, `objectId`, `controlFields` (vide), `controlSheetId`, `date`, `isDone` (true)
    - Si j’ai une alerte à contrôler ou en quarantaine : met à jour `conformityId`
- Si j’ai au moins un EAV
Eav : `object`, `objectId`, `eavs` (tableau de champs attribut ⇒ valeur), `subsidiaryId`

Retour de l’API : le matériel mis à jour, la localisation, les EAV

# Zone (à MAJ)

## Store

- Zone
- Si j’ai une localisation (basé sur adresse OU latitude ET longitude)
Location : `address`, `latitude`, `longitude`, `zoneId`
- Si j’ai une date de dernier contrôle (lastControlDate)
Control : `object`, `objectId`, `controlFields` (vide), `controlSheetId`, `date`, `isDone` (true)**⇒ INFO : ça va être modifié car un type peut avoir plusieurs fiches de contrôle différentes**
- Si j’ai au moins un EAV
Eav : `object`, `objectId`, `eavs` (tableau de champs attribut ⇒ valeur), `subsidiaryId`

Retour de l’API : uniquement la zone

## Update

- Zone (uniquement les champs updatés)
- Si j’ai une localisation (basé sur adresse OU latitude ET longitude)
Location : `address`, `latitude`, `longitude`, `zoneId`**Si je n’en ai plus, la supprimer de la table location**
- Si j’ai au moins un EAV
Eav : `object`, `objectId`, `eavs` (tableau de champs attribut ⇒ valeur), `subsidiaryId`

Retour de l’API : uniquement la zone mise à jour

# Site (à MAJ)

## Store

- Site
- Si j’ai une localisation (basé sur adresse OU latitude ET longitude)
Location : `address`, `latitude`, `longitude`, `siteId`
- Si j’ai une date de dernier contrôle (lastControlDate)
Control : `object`, `objectId`, `controlFields` (vide), `controlSheetId`, `date`, `isDone` (true)**⇒ INFO : ça va être modifié car un type peut avoir plusieurs fiches de contrôle différentes**
- Si j’ai au moins un EAV
Eav : `object`, `objectId`, `eavs` (tableau de champs attribut ⇒ valeur), `subsidiaryId`

Retour de l’API : uniquement le site

## Update

- Site
- Si j’ai une localisation (basé sur adresse OU latitude ET longitude)
Location : `address`, `latitude`, `longitude`, `siteId`**Si je n’en ai plus, la supprimer de la table location**
- Si j’ai au moins un EAV
Eav : `object`, `objectId`, `eavs` (tableau de champs attribut ⇒ valeur), `subsidiaryId`

Retour de l’API : uniquement le site mis à jour

Brands.json

BrandsHistories.json

Formats.json

GPSCONFIG (à vérifier quand endpoints fini)

gpsConfig.json

Groups.json

Materials.json

MaterialsHistories.json

MaterialEav.json

MaterialEavHistories.json

Notifications.json

QrCode.json

Sensors.json

SensorsHistories.json

Sites.json

SitesHistories.json

States.json

Status.json

subsidiaries.json

subsidiariesEav.json

Teams.json

Templates.json

Token.json

Trackers.json

TrackersEav.json

TrackersHistories.json

TrackersEavHistories.json

Types.json

TypesHistories.json

users.json

userEav.json

usersHistories.json

usersEavHistories.json

Zones.json

zonesHistories.json

ZonesEav.json

zonesEavHistories.json