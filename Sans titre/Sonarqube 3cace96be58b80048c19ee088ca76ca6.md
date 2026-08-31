# Sonarqube

**SonarQube** est une plateforme d’analyse continue de la qualité du code. Elle permet de détecter automatiquement les **bugs, vulnérabilités, failles de sécurité et problèmes de maintenabilité** dans le code source.

Son objectif est d’aider les équipes de développement à produire un code plus **propre, sûr et durable** en fournissant des **rapports détaillés et des indicateurs de qualité**.

### Installation

- `./dockerdo up -d`
- Se connecter à localhost:9000 avec le compte **admin/admin**. Il vous sera demandé de changer le mot de passe ensuite, enregistrez-le bien dans votre gestionnaire !
- Créer un projet en local avec pour nom : Charlie_platform. Branche de base : `dev`
- Générer un token pour ce projet et le mettre dans le **.env** avec pour clé `SONARQUBE_TOKEN`
- `chmod +x tests/sonarqube/start_analysis.sh`

### Lancer une analyse

- `./tests/sonarqube/start_analysis.sh`

### Lien

Une fois le Docker lancé, accéder à : [http://localhost:9000](http://localhost:9000/)