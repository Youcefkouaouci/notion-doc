# Commandes utiles

# Métier

## Requete SQL taille des DB MySQL

```sql
SELECT
    table_schema AS database_name,
    ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS size_mb,
    ROUND(SUM(data_length + index_length) / 1024 / 1024 / 1024, 2) AS size_gb
FROM information_schema.tables
GROUP BY table_schema
ORDER BY size_mb DESC;
```

## Requete compass shell taille des DB MONGO

```jsx
db.adminCommand({ listDatabases: 1 }).databases.map(d => ({
  db: d.name,
  poids_Mo: Math.round(d.sizeOnDisk / 1024 / 1024 * 100) / 100
}))
```

## Réindexation d’un model sur meilisearch

Utiliser `->searchable()`

```json
Model::where(...)->searchable()
```

## Regénérer la documentation API

Une fois que la documentation [Swagger](https://swagger.io/) a été mise à jour, une commande automatique permet de regénérer dyanmiquement le fichier JSON de documentation qui sera affiché sur l’endpoint `api/documentation` de chaque namespace.

```bash
./dockerdo art l5-swagger:generate
```

Exemple d’URL : `localhost/api/documentation`

## Fiche de contrôle non générée

Parfois, un contrôle n’a pas été généré correctement, et on se retrouve avec une donnée buguée en DB : `fileId` nul, mais `controlFields` contenant les informations (alors qu’il n’est pas en brouillon !).

Si t'as besoin de regénérer un contrôle :

- Se connecter sur le pod worker du namespace (via le plugin Kubernetes de VSCode par exemple)
- Lancer les commandes suivantes (en remplaçant <ID> par l'Id du contrôle)

```php
php artisan tinker

use App\\Jobs\\Controls;
AfterCreate(<ID>)::dispatch();
```

Faire la dernière commande 2 fois, s'assurer que le job est bien passé via horizon et dans la table controls, qu'on a mtn un `fileId` pour le contrôle en question.

# Bases de données

[[Filtres MongoDB](https://app.notion.com/p/3b39f2c3bf9480078653f707f5f0ccbe?pvs=21)](Commandes%20utiles/Filtres%20MongoDB%203cace96be58b8065ad4ff5aaaba5e3ef.md)

## Erreur création de BDD (mysql)

En cas de création d’une DB mysql qui ne fonctionne pas (problème de droit) :

- Forcer la connexion avec l’utilisateur `root`

```bash
# root et password sont respectivement le nom du superadmin et son mot de passe
./vendor/bin/sail exec mysql mysql -uroot -ppassword
```

- Créer la DB avec `root` et donner les droits à `sail`

```sql
// affiche les utilisateurs
SELECT USER(), CURRENT_USER();
// crée la DB
CREATE DATABASE IF NOT EXISTS `dev`;
// donne les droits
GRANT ALL PRIVILEGES ON `dev`.* TO 'sail'@'%';
// applique les changements
FLUSH PRIVILEGES;
```

## Lister nombre occurences selon ID type

Nombre de lignes d’inventaires uniques contenant au moins un matériel dont le type correspond (ici 134)

```java
SELECT COUNT(DISTINCT ia.inventoryId) AS inventories_count
FROM inventories_assets ia
LEFT JOIN materials m ON m.id = ia.materialId
WHERE m.typeId = 134;
```

## Pourcentage de connexions utilisées (mysql)

```jsx
SELECT
  @@max_connections AS max_connections,
  VARIABLE_VALUE AS threads_connected,
  ROUND(VARIABLE_VALUE / @@max_connections * 100, 2) AS usage_percent
FROM performance_schema.global_status
WHERE VARIABLE_NAME = 'Threads_connected';
```

## Détail des connexions actuelles (mysql)

```jsx
SELECT
  USER,
  HOST,
  DB,
  COMMAND,
  COUNT(*) AS connections
FROM information_schema.PROCESSLIST
GROUP BY USER, HOST, DB, COMMAND
ORDER BY connections DESC;
```

## Récupérer des données sur une plage horaire

```json
{
  created_at: {
    $gte: ISODate("2026-04-09T16:30:00Z"),
    $lte: ISODate("2026-04-09T18:00:00Z")
  },
	"payload.deviceId" : "feb230fcf3cc57fe"
}
```

# Linux

## Problème sur le port 1883

Au lancement du Docker, si conflit sur le port 1883 (MQTT) indiquant qu’il est déjà utilisé, lancer :

```bash
sudo service mosquitto stop
```

## Extraction de logs

Les fichiers de logs peuvent parfois être très lourds, et rechercher via le terminal peut devenir pénible. Voici une commande pour filtrer ces logs de façon journalière

Exemple pour récupérer uniquement ceux en date du 19/03 :

```java
grep '^\[2026-03-19' storage/logs/laravel.log
```

# NPM run : fichier non existant

Si vous rencontrez cette erreur :

The file does not exist at "/home/charlie/Documents/Project/Charlie_platform/node_modules/.vite/deps/chunk-JHFHTA24.js?v=787eb33f" which is in the optimize deps directory. The dependency might be incompatible with the dep optimizer. Try adding it to `optimizeDeps.exclude`.

Voici le processus à effectuer dans ce cas :

- Stopper le `npm run` si toujours en cours
- `rm -fr node_modules/.vite`
- Relancer `npm run`