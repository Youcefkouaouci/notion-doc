# Traitement inventories

**Workflow** : [https://www.figma.com/board/iVEnZGbDftWBGu1vewxLli/TreatmentInventories?node-id=0-1&node-type=canvas&t=yUmtkrIM06TwjQhi-0](https://www.figma.com/board/iVEnZGbDftWBGu1vewxLli/TreatmentInventories?node-id=0-1&node-type=canvas&t=yUmtkrIM06TwjQhi-0)

# Types d’inventaire

## Convention de nommage

Les codes sont basés sur 3 chiffres :

- Le 1er chiffre représente la source de l’inventaire :
    - 1XX ⇒ tracker
    - 2XX ⇒ téléphone
    - 3XX ⇒ connect
- Le 2ème chiffre définit l’interprétation vis-à-vis de l’inventaire
    - X1X ⇒ inventaire zone (classique)
    - X2X ⇒ inventaire téléphone
    - X3X ⇒ Détections
- Le 3ème chiffre définit un sous-code spécifique, tel que décrit ci-dessous, pour plus de clarté et pour différencier certains cas dans les règles d’affichage par exemple

## Différents codes de traitement

### Inventaire traité sur une zone ciblée

- **110** ⇒ Inventaire tracker
- **111** ⇒ Inventaire tracker capteur zone (un seul capteur zone pour la filiale)
- **310** ⇒ Inventaire Charlie Connect avec un capteur zone
- **210** ⇒ Inventaire téléphone avec un capteur zone
- **211** ⇒ Inventaire téléphone non envoyé avec un capteur zone

### Inventaire traité comme un Charlie Connect

- **130** ⇒ Inventaire tracker (avec scan BLE ou trame CP) sans capteur zone, ou avec plus de 2 de la même filiale
- **330** ⇒ Inventaire charlie Connect
- **331** ⇒ Charlie Connect communautaire
- **230** ⇒ Inventaire téléphone non envoyé

### Inventaire téléphone

- **220** ⇒ Inventaire téléphone avec que des capteurs ou au moins 2 capteurs zone
- **221** ⇒ Inventaire QR Code

### Détections

- **131** ⇒ Inventaire sans scan BLE / sans trames capteurs dont le tracker est associé à une zone
- **132** ⇒ Inventaire sans scan BLE / sans trames capteurs dont le tracker est associé à un matériel

# Format de stockage

Les inventaires sont sauvegardés sur 2 tables différentes : `inventories` et `inventories_assets`

## Inventories

La table inventories contient tous les paramètres communs à un inventaire :

- Zone de détection ou utilisateur l’ayant réalisé (inventaire téléphone)
- Date de réalisation (champ time)
- Code de statut (traité ou non, voir 1ère section)
- Codes de types d’inventaires (voir 2ème section)
- Etat de mouvement (optionnel) : démarrage, arrêt, choc..
- Equipe de détection
- ID de filiale (lié à la zone où est associé le tracker/capteur)
- Date exacte d’insertion sur la table (peut être différente de la date de réalisation de l’inventaire)

## Inventories assets

La table inventories assets contient la liste des assets détectés dans un inventaire. Chaque ligne référence :

- L’identifiant d’inventaire
- Des champs typeId ET un champ materialId OU zoneId rempli (en général, une ligne zoneId par inventaire, une ou plusieurs lignes de materialId)
- Site de détection
- Date de détection (parfois commune, parfois différente comme sur Connect)
- Position de l’asset (latitude et longitude)
- Batterie éventuelle
- Valeur RSSI (dBm)
- Date exacte d’insertion sur la table (peut être différente de la date de détection)