# Meilisearch

# Introduction

Meilisearch est un outil d’optimisation de requête de recherche et de filtrage par sauvegarde des données sur des fichiers optimisées.

[Analyse Performance Cursor](https://app.notion.com/p/3369f2c3bf9480c0a8bde6ab6d541075?pvs=21)

[Analyse Performance ChatGPT](https://app.notion.com/p/3369f2c3bf9480589507eea5b4089a23?pvs=21)

# Documentation officielle

[Documentation - Meilisearch Documentation](https://www.meilisearch.com/docs/home)

# Utilisation

Lancer la commandes :

```json
./dockerdo art meili:setup
```

Celle-ci lancera à son tour un `SetupMeiliJob` (accessible via Horizon), qui lui-même exécutera un `SetupMeiliModelJob` pour chaque modèle.

En cas d’erreur sur certains paramètres, lancer `./dockerdo art db:seed --class=DeleteUnusedObjects`

En cas de besoin de rafraîchir un modèle spécifique (par ex capteur ici) :

```bash
php artisan scout:import "App\\Models\\Sensor"
```

Les données mises en cache sont accessible via le port 7700 du Docker : [http://localhost:7700/](http://localhost:7700/)

**Connexion Meili prod centralisé :**

[http://meilisearch.meilisearch.svc.cluster.local:7700/](http://meilisearch.meilisearch.svc.cluster.local:7700/)

API KEY est sur LastPass : [https://eu.onetimesecret.com/secret/16url2wsyiscnle8qpppofpotl1ubwj7bc8ddp9xsjmh4ob9jekqocvfkuuwf9](https://eu.onetimesecret.com/secret/16url2wsyiscnle8qpppofpotl1ubwj7bc8ddp9xsjmh4ob9jekqocvfkuuwf9)

# Implémentation

## Fichier scout.php

Contient l’utilisation des différentes variables d’environnement tel que le driver (ici Meilisearch), la taille du chunk, ou encore les configurations Algolia (moteur de recherche hébergé en cloud) et Typesense (non utilisé)

## Trait SearchableFilterable

Il contient la logique principale de recherche, dans 2 fonctions distinctes :

- `searchFilterSort`
- `scopeSearchFilterSort`

## Modèles

Les modèles utilisent le trait `SearchableFilterable`, et surchargent une fonction `toSearchableArray()` qui définit toutes les données recherchables, filtrables et triables et `getSearchableAttributes()` qui définit sur quoi rechercher concrètement.

Ils surchargent également une fonction `getFilterableAttributes()` qui définit sur quels champs on peut filtrer (filtres de recherche) et `getSortableAttributes()`, pour le tri de ces derniers.

Enfin `getSearchOptions()` est utilisé dans certains modèles (Material, Sensor, Tracker, Zone) et permet de changer le comportement de base. Elle permet notamment d’ignorer les espaces inclus dans la recherche.

## Contrôleurs

Les contrôleurs pour la vue (ViewControllers) appellent `searchFilterSort` sur la méthode index afin de filter et/ou trier le tableau en fonction des paramètres.

## Observers

Ils permettent de mettre à jour la table de cache des données lors d’un changement. (utilité à confirmer)

## **1. Installation et configuration**

### Installation et configuration

Nous avons commencé par installer les dépendances nécessaires :

Laravel Scout pour faire le lien entre Laravel et le moteur de recherche

Le client PHP de Meilisearch pour communiquer avec le serveur

La configuration a ensuite été réalisée via les variables d’environnement, en définissant le driver Scout sur Meilisearch ainsi que l’URL du serveur et la clé d’accès.

### **Indexation des modèles**

**Indexation des modèles**

Les modèles concernés par la recherche ont été configurés en utilisant le trait Searchable fourni par Scout. Cela permet d’automatiser l’indexation des données dans Meilisearch à chaque création, mise à jour ou suppression d’un enregistrement.

Cette approche garantit une synchronisation continue entre la base de données et le moteur de recherche.

### **Configuration avancée des index**

**Configuration avancée des index**

Pour chaque modèle, nous avons également mis en place trois méthodes spécifiques permettant de configurer finement le comportement de Meilisearch :

- getFilterableAttributes() : Définit les champs utilisables pour le filtrage (facettes), comme les identifiants, statuts ou relations.
Cela permet d’effectuer des recherches avec contraintes (ex : filtrer par site, statut, groupe, etc.).
- getSortableAttributes() : Liste les champs sur lesquels il est possible de trier les résultats.
On y retrouve principalement des champs lisibles côté utilisateur (noms, dates, références, etc.).
- getSearchableAttributes() : Définit les champs réellement utilisés pour la recherche full-text.

Cette liste inclut :

- des champs métier (référence interne, zones, équipes, etc.)
- des données textuelles pertinentes (adresse, labels…)
- ainsi que des attributs dynamiques issus des custom fields, récupérés dynamiquement

### Problème de performances rencontré

Ce comportement est lié au fonctionnement asynchrone de l’indexation via Laravel Scout et Meilisearch :

- Les opérations d’indexation sont envoyées sous forme de tâches (tasks) à Meilisearch
- Ces tâches sont traitées en arrière-plan (non bloquant)
- Le moteur ne garantit pas une indexation instantanée (near real-time, mais pas temps réel strict)

**Impact**

Résultats de recherche non synchronisés avec la base

Incohérences visibles pour les utilisateurs

Difficulté à garantir la fraîcheur des données dans les interfaces de recherche