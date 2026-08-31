# Champs personnalisés (EAV)

## Définition

Les **CustomFields** sont des **champs personnalisés** que l’on peut créer pour ajouter des informations spécifiques dans un formulaire.

Les **EAV** sont les **valeurs** remplies dans ces champs personnalisés.

Pour en savoir plus, consulter la page ci-dessous.

[Définition d’un EAV](https://app.notion.com/p/db302b8f53a54a688fc2169dccb87b40?pvs=21)

## Structure proposée (au 04/04/2025)

```json
customFields {
	id
	attribute
	type
	isRequired
	section
	subsidiaryId
	object
	objectId
	subObject
	fromObject
	fromObjectId
}

eav {
	id
	customFieldId
	objectId
	value
}
```

## Définition des clés

```json
customField :
id           => Identifiant
attribute    => Nom du champ (label)
type         => Type du champs personnalisé
isRequired   => Champs obligatoire
section      => Section dans un formulaire
subsidiaryId => Id Filiale
object       => Type de l'asset lié à ce champ
objectId     => Id de l'asset lié à ce champ
subObject    => Asset lié à l'object (Seulement si object = App\Models\Type)
fromObject   => Asset parent de l'objet
fromObjectId => Id de fromObject

eav :
id             => Identifiant
customFieldId  => Id du customField rempli
objectId       => Id de l'asset créé ou modifié
value          => Valeur rentrée dans le champ
```

API format:

```json
// Create CustomFields
{
    "subsidiaryId": 3,
    "attribute": "Datetime",
    "type": "datetime-local",
    "section": 1,
    "object": "App\\Models\\Material",
    "objectId": 4
    //"subObject" : "App\Models\Material"
    // "fromObject" : "App\\Models\\Type",
    // "fromObjectId" : 2
}

// Create EAV
{
    "customFieldId": 10,
    "objectId": 11,
    "value": "2025-10-01 15:22",
    "timezone": "Europe/Paris" // only for datetime-local
}
```

## Sections et types

- Les sections vont de 1 à 5 :
    - informations générales (1),
    - affectation (2), // apparaît dans infos générales sur le détail, mais dans Affectation dans create/edit
    - localisation (3),
    - état et conformité (4),
    - informations complémentaires (5)
    ⇒ 2 et 5 ne sont globalement pas utilisées
- Les types peuvent actuellement avoir comme valeur :
    - `string` : chaîne de caractères
    - `int` : entier
    - `date`
    - `datetime-local` : date au format UTC (prise en compte de la timezone dans les APIs)
- La valeur du champ `isRequired` permet de déterminer si celui-ci doit être renseigné dans le formulaire d’ajout/édition de l’asset

## Cas d’utilisation

Cas N°1 : Un champ personnalisé pour un type précis

```json
customFields {
	id : 1
	attribute : "Ref GMAO"
	type : "string"
	isRequired : true
	section : 1
	subsidiaryId : 1
	object : "App\Models\Type"
	objectId : 1
	subObject : null
	fromObject : null
}

eav {
	id : 1
	customFieldId : 1
	objectId : 1
	value : "bla"
}
```

Cas N°2 : Un champ personnalisé pour tous les types d’une catégorie (Matériel, Zone ou Site)

```json
customFields {
	id : 1
	attribute : "Ref GMAO"
	type : "string"
	isRequired : true
	section : 1
	subsidiaryId : 1
	object : "App\Models\Type"
	objectId : null
	subObject : "App\Models\Zone"
	fromObject : null
}

eav {
	id : 1
	customFieldId : 1
	objectId : 1
	value : "bla"
}
```

Cas N°3 : Un champ personnalisé pour tous les types

```json
customFields {
	id : 1
	attribute : "Ref GMAO"
	type : "string"
	isRequired : true
	section : 1
	subsidiaryId : 1
	object : "App\Models\Type"
	objectId : null
	subObject : null
	fromObject : null
}

eav {
	id : 1
	customFieldId : 1
	objectId : 1
	value : "bla"
}
```

Cas N°4 : Un champ personnalisé pour tous les matériels d’un type

```json
customFields {
	id : 1
	attribute : "Ref GMAO"
	type : "string"
	isRequired : true
	section : 1
	subsidiaryId : 1
	object : "App\Models\Material"
	objectId : null
	subObject : null
	fromObject : "App\Models\Type"
	fromObjectId : 1
}

eav {
	id : 1
	customFieldId : 1
	objectId : 1
	value : "bla"
}
```

Cas N°5 : Un champ personnalisé pour tous les matériels

```json
customFields {
	id : 1
	attribute : "Ref GMAO"
	type : "string"
	isRequired : true
	section : 1
	subsidiaryId : 1
	object : "App\Models\Material"
	objectId : null
	subObject : null
	fromObject : null
}

eav {
	id : 1
	customFieldId : 1
	objectId : 1
	value : "bla"
}
```

Cas N°6 : Un champ personnalisé pour un matériel précis

```json
customFields {
	id : 1
	attribute : "Ref GMAO"
	type : "string"
	isRequired : true
	section : 1
	subsidiaryId : 1
	object : "App\Models\Material"
	objectId : 1
	subObject : null
	fromObject : null
}

eav {
	id : 1
	customFieldId : 1
	objectId : 1
	value : "bla"
}
```