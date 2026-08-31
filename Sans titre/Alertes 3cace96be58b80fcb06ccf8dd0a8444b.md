# Alertes

## Différents types d’alerte

- Contrôle / quarantaine :
- Perdu / retrouvé :
- Geofencing :

## Paramètres

| Alerts | WorkflowV2 | WorkflowV3 | Description | Parameters | Effect | Schedule |
| --- | --- | --- | --- | --- | --- | --- |
| Alerte Immobile | [https://www.figma.com/board/5Y63EUlEYHJ6z4aZGFe2we/Alerte-Matériel-Immobile-(V2)?node-id=0-1&t=du77wuiJ6QL7tGIc-0](https://www.figma.com/board/5Y63EUlEYHJ6z4aZGFe2we/Alerte-Mat%C3%A9riel-Immobile-(V2)?node-id=0-1&t=du77wuiJ6QL7tGIc-0) | [https://www.figma.com/board/5621nbJN2vOQTqboyb5Gik/Alerte-immobile-V3?t=qdTtoKOyjgNfNUiL-0](https://www.figma.com/board/5621nbJN2vOQTqboyb5Gik/Alerte-immobile-V3?t=qdTtoKOyjgNfNUiL-0) | L’alerte se déclenche lorsque le matériel ou la zone n’a **pas été bougé de position depuis X jours**. |  |  |  |

*On considère que le matériel à bougé lorsque sa position à changé de plus de 150 mètre.*

*X est choisi par l’utilisateur.* | - le nombre de jours X configuré dans l’alerte

- choix multi-select types matériels / zone
- choix multi-select utilisateur
- fréquence de notification / notification supplémentaire par utilisateur | Si diff entre date du jour et last_position_date > X : les matériels/zones dont le type a une alerte passent en statut **“immobile”** | Tous les jours à 8h dans le mail récap. |
| Alerte À Contrôler | [https://www.figma.com/board/a862ULEh5mClvJGUbs5f4z/Alerte-Matériel-à-Contrôler-V2?node-id=0-1&t=RHlsOZoXUv6kGbGR-0](https://www.figma.com/board/a862ULEh5mClvJGUbs5f4z/Alerte-Mat%C3%A9riel-%C3%A0-Contr%C3%B4ler-V2?node-id=0-1&t=RHlsOZoXUv6kGbGR-0) | [https://www.figma.com/board/2pfa9nExMhGE2ZDDNf7T4B/Alerte-à-Contrôler-%2F-en-quarantaine-V3?t=qdTtoKOyjgNfNUiL-0](https://www.figma.com/board/2pfa9nExMhGE2ZDDNf7T4B/Alerte-%C3%A0-Contr%C3%B4ler-%2F-en-quarantaine-V3?t=qdTtoKOyjgNfNUiL-0) | Alerte qui se déclenche **X jours (ou moins)** avant la date du prochain contrôle. L’état de l’élément passe à l’état de conformité **À Controler**.

*X est choisi par l’utilisateur.* | - le nombre de jours X configuré dans l’alerte

- choix multi-select types matériels / zones / sites / Équipe
- choix multi-select utilisateur
- fréquence de notification / notification supplémentaire par utilisateur | Si diff entre (la date du jour et la date out_control) -1 > 0 et que cette diff > X, alors l’alerte se déclenche : L’état de conformité de l’élément passe à **“À Contrôler”**. | Tous les jours à 8h dans le mail récap. |
    
    | Alerte En Quarantaine |  | [https://www.figma.com/board/2pfa9nExMhGE2ZDDNf7T4B/Alerte-à-Contrôler-%2F-en-quarantaine-V3?t=qdTtoKOyjgNfNUiL-0](https://www.figma.com/board/2pfa9nExMhGE2ZDDNf7T4B/Alerte-%C3%A0-Contr%C3%B4ler-%2F-en-quarantaine-V3?t=qdTtoKOyjgNfNUiL-0) | Alerte qui se déclenche lorsque la date de prochain contrôle est dépassée. L’état de l’élément passe à l’état **En Quarantaine**. | Alerte automatique sur tous les éléments qui ont une date out_control non null et qui est dépassé
    
    | Passage dans l’état de conformité “En Quarantaine” pour les éléments dont date out_control < date du jour
    
- Pour les éléments ayant une alerte À Contrôler : Notification envoyée aux utilisateurs choisis dans l’alerte À Contrôler
    
    Pour les éléments n’ayant pas d’alerte À Contrôler : pas de notification envoyée | Tous les jours à 8h dans le mail récap. |
    
    | Alerte Perdu | [https://www.figma.com/board/KwPVY888Lxm01MVa2YJcux/Alerte-Materiel-Perdu-(V2)?node-id=0-1&t=uCZuXGMlV6ifkmVS-0](https://www.figma.com/board/KwPVY888Lxm01MVa2YJcux/Alerte-Materiel-Perdu-(V2)?node-id=0-1&t=uCZuXGMlV6ifkmVS-0) | [https://www.figma.com/board/q2pcktlrM8y6rW9jVlKh1Y/Alerte-Perdu-(V3)?node-id=0-1&p=f&t=CUnhtISmqJmGf8ua-0](https://www.figma.com/board/q2pcktlrM8y6rW9jVlKh1Y/Alerte-Perdu-(V3)?node-id=0-1&p=f&t=CUnhtISmqJmGf8ua-0) | L’alerte se déclenche lorsque l’élément n’a **pas été détecté depuis X jours**.
    
    Le statut du matériel passe à **Perdu**.
    

*X est choisi par l’utilisateur.* | - Le nombre de jours X configuré dans l’alerte

- choix multi-select types matériels
- choix multi-select utilisateur
- fréquence de notification / notification supplémentaire par utilisateur | Si diff entre detection_date et date du jour > X, alors l’alerte se déclenche et l’élément passe en statut “Perdu” | Tous les jours à 8h dans le mail récap. |
| Alerte Retrouvé | [https://www.figma.com/board/kzM1cifSOAJGDTVCuyBTdt/Alerte-Matériel-Retrouvé-(V2)?node-id=0-1&t=FTPuqfJnuZO881lh-0](https://www.figma.com/board/kzM1cifSOAJGDTVCuyBTdt/Alerte-Mat%C3%A9riel-Retrouv%C3%A9-(V2)?node-id=0-1&t=FTPuqfJnuZO881lh-0) | [https://www.figma.com/board/XHwIYVpR3WtOkZ7kDQ4M6z/Alerte-Retrouvé?t=qdTtoKOyjgNfNUiL-0](https://www.figma.com/board/XHwIYVpR3WtOkZ7kDQ4M6z/Alerte-Retrouv%C3%A9?t=qdTtoKOyjgNfNUiL-0) | L’alerte se déclenche lorsqu’un élément dans un statut “Perdu” se fait à nouveau détecté.
Le statut du matériel passe à “Retrouvé” | | Notification aux utilisateurs qui étaient configuré sur l’alerte Perdu de l’élément concerné, sinon pas de notification.

Le statut “Retrouvé” reste 3 jours. | Dans les traitements. |

| Alerte Géofencing |  | [https://www.figma.com/board/jsk8bRNxAV9BVr0suRnKJ8/Alerte-geofencing-V3?t=qdTtoKOyjgNfNUiL-0](https://www.figma.com/board/jsk8bRNxAV9BVr0suRnKJ8/Alerte-geofencing-V3?t=qdTtoKOyjgNfNUiL-0) | L’alerte se déclenche lorsque l’élément est détecté dans ou à l’extérieur d’un site. | - choix multi-select de matériels ou zones

- choix multi select de site avec choix d’entrée et/ou sortie
- fréquence de notification : a chaque fois / une seule fois
- choix multi-select utilisateur | Lors de la détection d’un élément dans ou à l’extérieur du site concerné, déclenchement de l’alerte en associant ou dé-sassociant l’élément au site de détection en question + notification aux utilisateurs concerné | Dans les traitements |

## QUESTIONS

Si on a une alerte sur le type, et qu’un utilisateur crée une alerte sur un matériel de ce type : Les utilisateurs non sélectionnés sur l’alerte de ce matériel ne seront pas notifiés sur l’alerte du type.

Potentielle idée :

On reste sur la règle : plus restreint en priorité

et dans le tableau des alertes, si on a une alerte sur un type et une alerte sur un matériel de ce type, on ajoute comme informations dans l’alerte de type tous les matériels qui ont une alerte spécifique et qui ne rentreront pas dans ce process d’alerte

## Règles de décision sur les conflits

- Règle la plus restreinte en priorité
Ex. : matériel prend le dessus sur type de matériel ; utilisateur prend le dessus sur l’équipe
    - Mettre en place des règles fronts (empêcher au maximum les conflits)
        - Rendre non dispo (disabled) certains champs comme le nb de jours pour la notif si j’ai une alerte sur un type et que je veux en créer une sur un matériel / une zone
    - Equipe et utilisateur : n’avoir qu’un sur les 2 en V3.0
        - v3.2 : possibilité des 2 et règle du plus petit ou addition des règles
- Plusieurs durées : prendre la durée la plus grande pour changer l’état / le statut
Ex. : j’ai une alerte sur le matériel X à 10jours et une alerte sur le même matériel à 5 jours, ça doit mettre à jour l’état à 10 jours
- Règle distinction du nombre de jours avant le déclenchement de l’alerte VS le nombre de jours (plusieurs niveaux possibles) de notification
    - Exemples :
        - A CONTROLER : le nb de jours pour la MAJ de l’état doit être ≤ au plus petit niveau de notification
        - IMMOBILE : le nb de jours pour la MAJ de l’état doit être ≥ au plus petit niveau de notification
- Alerte retrouvé / geofencing : comment alerter en mode réactif sans spamer l’utilisateur ?
⇒ **Regrouper les matériels pour notifier par trame (ex 5 matériels : 1 notif au lieu de 5) dans le traitement @Cyril Buhlmann**
⇒ Alerte mail, notif et push
- Autres alertes : envoi à 6h avec un mail récap et une notif par alerte

# Structure JSON

La table `alerts` sera composée comme suit :

```jsx
"name": "Example",
"description": "This is an example description",
"code": X,
"object": "App\\Models\\Zone",
"objectIds": [
	X, Y, Z
],
"daysbeforeXXX": X,
"isActive": true,
"notify": [
   "App\Models\User": [
		  {
            "id": X,
            "notifications": [
                {
                    "days": X,
                    "method": []
                },
                {
                    "days": Y,
                    "method": [
                        "email"
                    ]
                }
              ]
         },
   ],
   "App\Models\Team": []
],
```

## Champ FACULTATIFS :

description

---

## **Champ obligatoires :**

code : correspond au type de l’alerte (controle, immobile, mouvement)

| Code | Type | Dénomination |
| --- | --- | --- |
| 1 | TO_CONTROL | A contrôler |
| 2 | QUARANTINE | En quarantaine |
| 3 | LOST | Perdu |
| 4 | MOTIONLESS | Immobile |
| 5 | GEOFENCING | Geofencing |

object, objectIds : Le type d’objet associé à l’alerte, et la liste des IDs des objets associés

```jsx
   "object": "App\\Models\\Zone",
   "objectIds": [
        1,
        2,
        3
    ],
```

notify : qui notifier (utilisateurs et équipes)

```json
"notify": [
      "App\Models\User": [
		     {
            "id": 1,
            "notifications": [
                {
                    "days": 7,
                    "method": []
                },
                {
                    "days": 14,
                    "method": [
                        "email"
                    ]
                }
              ]
         },
         {
            "id": 2,
            "notifications": [
                {
                    "days": 7,
                    "method": []
                },
                {
                    "days": 12,
                    "method": [
                        "email"
                    ]
                }
              ]
         }
       ]
         "App\Models\Team":
       [
	       {
            "id": 1,
            "notifications": [
                {
                    "days": 7,
                    "method": [
                    ]
                },
                {
                    "days": 14,
                    "method": [
                        "email"
                    ]
                },
                {
                    "days": 62,
                    "method": [
                        "email",
                        "push"
                    ]
                }
             ]
          }
       ]
   ]
```

## **CAS PARTICULIERS**

### Alerte à contrôler

- daysBeforeControl → nombre de jours avant la date de prochain contrôle pour le passage à l’état “À CONTROLER”
- L’attribut notify possède maintenant 2 tableaux :
    - toControl → les notifications pour l’alerte à contrôler (X jours **AVANT**)
    - quarantine → les notifications pour l’alerte quarantaine (X jours **APRÈS**)

```json
"notify": [
	"toControl": [
      "App\Models\User": [
			 {
            "id": 1,
            "notifications": [
                {
                    "days": 7,
                    "method": []
                },
                {
                    "days": 14,
                    "method": [
                        "email"
                    ]
                }
              ]

         "App\Models\Team":
	       {
            "id": 2,
            "notifications": [
                {
                    "days": 7,
                    "method": [
                    ]
                },
                {
                    "days": 14,
                    "method": [
                        "email"
                    ]
                },
                {
                    "days": 62,
                    "method": [
                        "email",
                        "push"
                    ]
                }
           ],
         ]
         ,
   "quarantine": [
      "App\Models\User": [
			 {
            "id": 1,
            "notifications": [
                {
                    "days": 7,
                    "method": []
                },
                {
                    "days": 14,
                    "method": [
                        "email"
                    ]
                }
              ]
        },
         "App\Models\Team":
	       {
            "id": 2,
            "notifications": [
                {
                    "days": 7,
                    "method": [
                    ]
                },
                {
                    "days": 14,
                    "method": [
                        "email"
                    ]
                },
                {
                    "days": 62,
                    "method": [
                        "email",
                        "push"
                    ]
                }
           ],
         ],
   }
```

### Alerte immobile

- daysWithoutMovements → nombre de jours sans bouger
- radius → rayon du cercle autour de la première détection indiquant le périmètre dont il ne faut pas sortir (minimum 50 mètres, avec des paliers de 25 mètres en 25 mètres)

### Alerte perdu

- daysWithoutDetections → nombre de jours sans détection

### Alerte géofencing

- sitesGeofenced → Liste des sites à géofencer

```json
"sitesGeofenced": [
	"1": [
		"in": true, // Alerte quand un matériel entre dans ce site
		"out": false, // Alerte quand un matériel sort de ce site
		"isReccuring": false
	],
	"2": [
		"in": true,
		"out": true,
		"isReccuring": true
	]
]
```

- isRecurring → true / false → indique si on envoie l’alerte à chaque fois (true) ou une seule fois (false)

### Alerte mouvement

start → Début de la période

end → Fin de la période

### Alerte start/stop

start → Début de la période

end → Fin de la période

OLD propositions

- Proposition Cyril
    
    ```json
    {
        "title": "perdu",
        "description": "Ma super description",
        "code": 100,
        "isFoundingAlert": [
            1, 2, 3
        ],
        "object": "App\\Models\\Zones",
        "data": [
            1,
            2,
            3
        ],
        "usersToNotify": [
            {
                "id": [1, 2],
                "notifications": [
                    {
                        "days": 7,
                        "method": [
                            "email"
                        ]
                    },
                    {
                        "days": 4,
                        "method": [
                            "email"
                        ]
                    },
                    {
                        "days": 2,
                        "method": [
                            "email",
                            "push"
                        ]
                    }
                ]
            },
            {
                "id": 1,
                "notifications": [
                    {
                        "days": 7,
                        "method": [
                            "email",
                            "push"
                        ]
                    },
                    {
                        "days": 4,
                        "method": [
                            "email",
                            "push"
                        ]
                    },
                    {
                        "days": 2,
                        "method": [
                            "email",
                            "push"
                        ]
                    }
                ]
            }
        ]
    }
    ```
    
    `type d’alerte` : on aura un code pour chaque alerte
    
- **Proposition Maxime**
    
    Etant donné qu’il peut y avoir une même alerte pour :
    
    - un ensemble d’utilisateurs, on peut imaginer une liste d’utilisateurs à notifier
    - un ensemble de matériels (sur une typologie par exemple)
    - un ensemle de sites (cas des alertes de geofencing)
    
    | Code | Type | Dénomination |
    | --- | --- | --- |
    | 1 | TO_CONTROL | A contrôler |
    | 2 | QUARANTINE | En quarantaine |
    | 3 | LOST | Perdu |
    | 4 | MOTIONLESS | Immobile |
    | 5 | TURNED_UP | Retrouvé |
    | 6 | GEOFENCING | Geofencing |
    
    On peut imaginer la structure suivante, pour les alertes 1,3 et 4 :
    
    ```json
    {
    	"name": "Superbe nom d'alerte à contrôler",
    	"typeCode" : 1,
    	"numberOfDays" : 3,
    	"types" :
    		{
    		  "object": "Material",
    		  "objectIds" : [1,2,3]
    		},
    		{
    		  "object": "Type",
    			"subObject": "Material",
    		  "objectIds" : [2,3]
    		},
    }
    ```
    
    - `name` est un nom optionnel qui peut être donné à l’alerte pour pouvoir l’identifier facilement
    - `typeCode` contient le code définissant le type d’alerte utilisé
    - `numberOfDays` : nombre de jours pour déclencher l’événement de l’alerte
    - `types` : liste des typologies concernées
        - `object` peut avoir les valeurs Material, Zone ou Type (et parfois Team)
        - `subObject` contient le sous-type, dans le cas où l’objet est un Type
        - `objectIds` contient la liste des identifiants concernés
    
    <aside>
    
    💡
    
    - Ici, l’alerte à contrôler s’applique sur :
        - les matériels dont l’identifiant est 1, 2 et 3
        - les types de matériel dont l’identifiant est 2 et 3
    - Si une alerte avec un nombre de jours différents existe, elle sera sur une ligne séparée. Toutes les 2 seront déclenchées, et c’est la première dans le temps qui appliquera le changement d’état du matériel ou de la zone
    </aside>
    
    <aside>
    
    💡
    
    Alerte *quarantaine* (code 2) : pas de config nécessaire à stocker, car on déclenche dès que la date de prochain contrôle est dépassée.
    
    Alerte *retrouvé* (code 5) : pas de config nécessaire à stocker, car on déclenche dès que c’est retrouvé.
    
    </aside>
    
    Pour l’alerte de geofencing (6) :
    
    ```json
    {
    	"name": "Superbe nom d'alerte de geofencing",
    	"typeCode" : 6,
    	"types" : [
    		{
    		  "object": "Material",
    		  "objectIds" : [1,2,3]
    		},
    		{
    		  "object": "Type",
    			"subObject": "Material",
    		  "objectIds" : [2,3]
    		},
    		{
    		  "object": "Site",
    		  "objectIds" : [1,2]
    		},
    	],
    	"trigger" : "input"
    }
    ```
    
    `trigger` est un paramètre qui permet de savoir quand on souhaite déclencher l’événement par rapport au(x) site(s). Il peut prendre les valeurs *input*, *output* ou *both*.
    
    <aside>
    
    💡
    
    - Ici, l’alerte de geofencing sur les sites 1 et 2 s’applique sur :
        - les matériels dont l’identifiant est 1, 2 et 3
        - les types de matériel dont l’identifiant est 2 et 3
    - Toutes les alertes groupées pour de même matériels ou types auront leur propre ligne
    - On peut imaginer une interdiction d’ajouter une nouvelle alerte si le matériel en question est déjà dans une autre avec le même site.
    </aside>