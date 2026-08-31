# Laravel Nightwatch

[https://nightwatch.laravel.com/](https://nightwatch.laravel.com/)

**Laravel Nightwatch** est un outil de surveillance et d’observabilité conçu pour les applications Laravel. Il permet de suivre en temps réel les performances, les requêtes, les tâches en arrière-plan, les erreurs et d’autres événements importants afin d’identifier rapidement les problèmes et d’optimiser le fonctionnement de l’application.

Intégré nativement à l’écosystème Laravel, Nightwatch offre une visibilité détaillée sur l’état de santé des applications et facilite leur maintenance en production.

ℹ️ Chez les clients, Laravel Nightwatch est désactivé par défaut afin d’éviter une surcharge du volume d’événements. En effet, le nombre d’événements est limité à 300 000 sur une période de 30 jours glissants.

Plusieurs modules de Nightwatch ne sont actuellement pas utilisés ou ne sont pas connectés, notamment la partie **Queues, Tasks**. Les informations disponibles se concentrent donc principalement sur les requêtes, les erreurs et les performances applicatives.

L’outil sera principalement utilisé pour le **débogage en production**, lorsque les informations fournies par **New Relic (NR)** ne sont pas suffisamment granulaires pour identifier précisément un problème. En revanche, pour les développements et les investigations en environnement local, il est recommandé de privilégier **Laravel Telescope** ou **Laravel Debugbar**, qui offrent une meilleure visibilité et un niveau de détail plus adapté au débogage.

### Activation chez les clients

Il faut mettre la variable `NIGHTWATCH_ENABLED` à true dans le .env

Se connecter au pod du worker et lancer la commande :

```php
php artisan nightwatch:agent
```

On retrouve comme principaux modules :

- **Dashboard** : vue d’ensemble de l’application avec les indicateurs clés, les performances et les éventuels problèmes détectés.
- **Requests** : permet d’analyser les requêtes HTTP, leur durée d’exécution, les erreurs associées et les points de ralentissement.
- **Exceptions** : centralise les erreurs et exceptions rencontrées afin de faciliter leur diagnostic et leur résolution.
- **Queues** : surveille les tâches exécutées en arrière-plan (jobs), leur temps de traitement et les éventuels échecs.
- **Database** : fournit des informations sur les requêtes SQL exécutées, leur durée et les éventuels problèmes de performance.
- **Cache** : affiche l’activité du cache et aide à identifier les opérations pouvant impacter les performances.
- **Logs** : regroupe les journaux générés par l’application pour faciliter l’analyse et le débogage.