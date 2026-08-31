# Rôles (ajout/update)

**Créer  d’un nouveau rôle**

1. Se connecter au worker plateforme du client
2. Lancer la commande ci-dessous :

```jsx
php artisan db:seed --class=CreatePartnersRoleSeeder
```

1. [0] : Ajouter un rôle
2. A la question “est ce que c’est un partenaire ?”, répondre : **OUI**
3. Sélectionner les endpoints auxquels le rôle aura accès en tapant sur la touche espace

**Modifier un nouveau existant**

1. Se connecter au worker plateforme du client
2. Lancer la commande ci-dessous :

```jsx
php artisan db:seed --class=CreatePartnersRoleSeeder
```

1. [1] : Modifier un rôle, et sélectionner le rôle à modifier
2. Assigner les nouveaux endpoints au scope du rôle
3. Après validation, lancer une commande pour clear le cache :

```jsx
php artisan permission:cache-reset
```