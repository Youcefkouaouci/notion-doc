# Seeders utiles

Certains seeders peuvent être bien pratiques pour débuguer une fonctionnalité complexe rapidement. Pour autant, il n’est pas nécessaire de les mettre sur le dépôt GitHub.

Il est alors possible de les instancier dans le seeder par défaut : `DatabaseSeeder`.

[**Load test seeders — guide de test**](Seeders%20utiles/Load%20test%20seeders%20%E2%80%94%20guide%20de%20test%203cace96be58b80c19b1af3c1ad1c8cac.md)

# Génération du mail journalier

La génération d’un mail journalier doit nécessiter plusieurs étapes : création d’une ou plusieurs alerte(s), mettre les assets dans les bonnes conditions souhaitées, appeler la commande..

Et si plusieurs itérations, il faut tout réinitialiser dans la base de données.

Grâce à ce seeder, il est possible de générer facilement le template du mail journalier :

```bash
$user = User::first();

        if (! $user) {
            $this->command->warn('No user found.');
            return;
        }

        $data = [
            Alert::TO_CONTROL_CODE => [
                [
                    'object' => 'App\Models\Material',
                    'days'   => 0,
                ],
            ],
            Alert::QUARANTINE_CODE => [
                [
                    'object' => 'App\Models\Material',
                    'days'   => 4,
                ],
            ],
            Alert::MOTIONLESS_CODE => [
                [
                    'object' => 'App\Models\Material',
                    'days'   => 2,
                ],
            ],
        ];

        Mail::to($user->email)->send(new DailyMail($user, $data));

        $this->command->info("DailyMail sent to {$user->email}");
```

# Suppression en masse de capteur

Fichier à mettre dans tmp/ sur s3, il faut mettre les numero de capteur dans la liste.

Voir exemple dans le fichier sensors_to_delete.csv

sensors_to_delete.csv