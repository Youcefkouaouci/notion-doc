# Historiques en décalé

Qu’est-ce qu’un historique en décalé ?

Dans le cas des inventaires décalés, il faut créer un historique n’étant pas le dernier pour un matériel / une zone. Exemple : Une zone a été détectée pour la dernière fois à 14h. Or on recoit un inventaire de cette zone à midi, il faut donc créer une historique à midi pour garder trace de l’état de la zone à cet instant (position, site de détection, etc).

Structure d’un historique

Une historique contient 2 tableaux: ‘before’ et ‘after’

‘before’ contient tous les champs de l’objet avant modification.

‘after’ contient seulement les champs qui ont été modifiés.

⚠️ Problème : Cela veut dire que si une zone a été détecté dans le site 1. Et qu’elle se fait détecter dans le même site. Le tableau ‘after’ ne contiendra pas detectionSiteId.

Fonctionnement idéal :

Prenons 2 historiques

Historique à 10h :

```json
{
	"before": [
		"latitude": 0,
		"longitude": 0,
		"time": 8h
	],
	"after": [
		"longitude": 10,
		"latitude": 10,
		"time": 10h
	]
}
```

Historique à 12h :

```json
{
	"before": [
		"latitude": 10,
		"longitude": 10,
		"time": 10h
	],
	"after": [
		"longitude": 20,
		"latitude": 20,
		"time": 12h
	]
}
```

Si on ajoute maintenant une historique à 11h, cette historique devra récupérer le tableau ‘before’ de l’historique à 12h. Mettre les modifications de cette historique à 11h, dans son tableau ‘after’. Et mettre à jour le tableau ‘before’ de l’historique à 12h avec ses modifications. Ce qui donnerait ceci.

Historique à 10h **INCHANGÉE** :

```json
{
	"before": [
		"latitude": 0,
		"longitude": 0,
		"time": 8h
	],
	"after": [
		"longitude": 10,
		"latitude": 10,
		"time": 10h
	]
}
```

Historique à 11h :

```json
{
	"before": [ // Tableau récupéré de l'historique à 12h
		"latitude": 10,
		"longitude": 10,
		"time": 10h
	],
	"after": [ // Tableau ajouté avec les modifications de 11h
		"longitude": 15,
		"latitude": 15,
		"time": 11h
	]
}
```

Historique à 12h :

```json
{
	"before": [ // Tableau mis à jour avec les données de 11h
		"latitude": 15,
		"longitude": 15,
		"time": 11h
	],
	"after": [
		"longitude": 20,
		"latitude": 20,
		"time": 12h
	]
}
```

Exemple :

Historique le 10 (détecté dans le site 1) :

```json
{
	"before": [
		"detectionSiteId": null
	],
	"after": [
		"detectionSiteId": 1
		"detectionDate": "2025-08-10"
	]
}
```

Historique le 12 :

```json
{
	"before": [
		"detectionSiteId": 1
	],
	"after": [
		"detectionDate": "2025-08-12"
	]
}
```

Une idée pourrait être de copier ‘detectionSiteId’ dans le after, si ‘after’ ne contient pas ‘detectionSiteId’. Sauf que ca ne fonctionne pas → car l’historique du 12 ne veut pas forcément dire que le matériel a été détecté dans le site 1 le 12, s’il vient d’un inventaire décalé.

Code actuel : Si ce n’est pas la dernière position, detectionSiteId = detectionSiteId du matériel

Il faudrait donc ajouter les données de détection (zone, site, équipe) dans les historiques à chaque inventaire, que ca ait changé ou non pour éviter les flous de données. En +, ca pourrait être + précis pour l’historique d’activité. (Le matériel a été détecté à tel instant dans tel site).