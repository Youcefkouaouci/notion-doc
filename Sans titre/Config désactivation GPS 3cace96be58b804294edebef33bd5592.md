# Config désactivation GPS

Maquettes : [https://www.figma.com/design/LLLbUGnbqSBuXPDJLr4rMT/Charlie-Solution?node-id=373-6319&p=f&t=2x36RMdBIcH3uRZT-0](https://www.figma.com/design/LLLbUGnbqSBuXPDJLr4rMT/Charlie-Solution?node-id=373-6319&p=f&t=2x36RMdBIcH3uRZT-0)

## Structure

- nom (*string*)
- Liste de(s) zone(s) (*array id*)
- Type de récurrence (*boolean*)
    - Ponctuelle
        - Date et heure de début
        - Date et heure de fin
    - Récurrente
        - Intervalle
            - jour/heure de début
            - jour/heure de fin
            - récurrence (toutes les x semaines)
            - date de début
            - date de fin (optionnel)
        - Jour précis
            - choix des jours
            - heure de début / heure de fin
            - récurrence (toutes les x semaines)
            - date de début
            - date de fin (optionnel)

## Modèle de donnée : MONGODB

## Types de config

### Ponctuel → Code 1

**Désactivation pour une période spécifique (ex. vacances)**

Exemple : Du lundi 03 mars 2025 au vendredi 07 mars 2025

```json
{
	"id": 1,
	"name": "ponctuel",
	"code": 1,
	"subsidiaryId": 1,
	"isActive": true,
	"zoneIds": [
		1,
		2
	],
	"startDate": "2025-03-03 08:00:00",
	"endDate": "2025-03-07 20:00:00"
}
```

### Intervalle → Code 2

**Désactivation avec heures fixes sur plusieurs jours**

Exemple : Du vendredi 18h au lundi 8h, toutes les semaines, ne s’arrête jamais

```json
{
	"id": 1,
	"name": "intervalle",
	"code": 2,
	"subsidiaryId": 1,
	"isActive": true,
	"zoneIds": [
		1,
		2
	],
	"period": {
		"start": {
			"day": 4, // Vendredi
			"hour": "18:00"
		},
		"end": {
			"day": 0, // Lundi
			"hour": "08:00"
		},
	},
	"frequency": 168, // Nombre d'heures dans une semaine
	"startDate": "2025-03-07 18:00:00", // Doit correspondre au même jour et heure
																			// que $period['start']
	"endDate": null
}
```

### Jours fixes → Code 3

**Désactivation avec heures fixes sur une journée**

Exemple : Tous les lundis, samedis et dimanches de 8h à 18h

```json
{
	"id": 1,
	"name": "jours fixes",
	"code": 3,
	"subsidiaryId": 1,
	"isActive": true,
	"zoneIds": [
		1,
		2
	],
	"days": [
		0, // Lundi
		5, // Samedi
		6  // Dimanche
	],
	"startHour": "08:00",
	"endHour": "18:00",
	"startDate": "2025-03-05 08:00:00",
	"endDate": null
}
```