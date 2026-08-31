# Contrôles

# Digitalisation de fiches

Process pour ajouter une nouvelle fiche :

- Créer le JSON de la fiche en suivant la structure suivante

[[Structure JSON V3](https://app.notion.com/p/b37435212af944c0b6bae8c4215595df?pvs=21)](Contr%C3%B4les/Structure%20JSON%20V3%203cace96be58b804bb829ed72379dd93a.md)

- Ajouter les traductions des champs de la fiche dans **`‎lang/controlTemplates/translations.json`**
- Ajouter le lien du JSON dans le job de création de templates de controle :`app/Jobs/Migrations/CreateControlTemplatesJob.php`

```json
'general'      => [
    ControlTemplate::DEFAULT_CONTROL_TEMPLATE_ID => [
        'name'         => 'FICHE DE CONTRÔLE GÉNÉRALE',
        'jsonFilePath' => '/templates/general_control_template.json',
        // If you want to add a control template for specific subsidiaries
        //'subsidiaryIds' => [
        //    1,
        //    Subsidiary::query()->where('name', 'Specific subsidiary')->first()?->id
        //]
    ],
],
// Key is a part of the APP_URL of the client that have these control templates
  'etf'          => [
      2 => [
          'name'         => 'FICHE DE CONTRÔLE TIREFONNEUSE',
          'jsonFilePath' => '/templates/etf/tirefonneuses.json',
      ],
  ],
```

Pour ajouter un template à tous les clients, l’ajouter dans la partie ‘general’. Sinon, ajouter le dans une partie dont la clé est une partie de l’app url du client, (doit être unique pour chaque client).

Dans l’exemple ci-dessus, on ajoute la fiche de contrôle tirefonneuse pour etf uniquement.

Il est possible d’ajouter un template pour des filiales spécifiques en ajout un tableau d’id, par défaut il est ajouté à toutes les filiales.

- L’ajouter également dans le seeder : `database/seeder/FixControlTemplateIds`
- Ajouter la traduction du ‘name’ du template dans les fichiers de lang : `lang/*/messages.php`
- Lancer le job/seeder de création de template : `./dockerdo art db:seed --class=ControlTemplatesSeeder`
- Lier le template créé à un type de matériel, et tester la création / édition d’un contrôle (ajout d’images, vérification du fonctionnement de tous les champs)

[[Control Fields](https://app.notion.com/p/5c8d9896105a401788fe220547d620f7?pvs=21)](Contr%C3%B4les/Control%20Fields%203cace96be58b807f84a0efb1c64cbb77.md)

[[État des lieux](https://app.notion.com/p/0ad67a1df63f41028272e27ae1eec6aa?pvs=21)](Contr%C3%B4les/%C3%89tat%20des%20lieux%203cace96be58b80d4a44ddd49acff0f82.md)

[[Fonctionnement](https://app.notion.com/p/1d79f2c3bf9480419d67f7c0716ad9d0?pvs=21)](Contr%C3%B4les/Fonctionnement%203cace96be58b808ba2cde38ffb28e091.md)

[[Tables BDD](https://app.notion.com/p/1d79f2c3bf948048b4f1dde984a31b6c?pvs=21)](Contr%C3%B4les/Tables%20BDD%203cace96be58b80d3a038f5ad7fccfdb5.md)