# Laravel Horizon

**Laravel Horizon** est un tableau de bord et un outil de gestion pour les files d’attente Laravel (aussi appelées queues).

Il permet de **superviser, monitorer et gérer les jobs de queue** en temps réel, avec des statistiques sur les performances et les échecs. Horizon est particulièrement utile pour les applications utilisant des queues avec Redis.

### Installation

- Dans le **.env**, mettre `QUEUE_CONNECTION=redis`
- `./dockerdo art horizon:install`

### Lancement du worker

- `./dockerdo art horizon`

### Lien

Visualisation de l’état de la queue (jobs réussis, échoués, en attente..)

[http://localhost/horizon/dashboard](http://localhost/horizon/dashboard)