# DB en local

### **Étapes**

1. **Sur demoV3 : Créer la base de données MySQL**

```jsx
sudo create-db nom_de_la_db
```

1. Se connecter à une base de données clients et l'exporter :
2. Importer cette base de données sur demoV3
3. Récupérer l'URI de la db mongo du client
    
    ⇒ Remplacer ce qu'il y a après le / par ?authSource=admin&replicaSet=replicaset&tls=true
    
4. Puis en ligne de commande faire :
    
    `mongodump --uri "URI client modifiée" --db nom_de_la_db_mongo_du_client --out ./backup_nom_du_client`
    
5. Importer la DB mongo sur demoV3 :
    
    `mongorestore --uri "URI de la db mongo demov3" ./backup_nom_du_client`
    
6. Modifier le .env de demoV3:
    
    DB_DATABASE=nom de la db mysql
    
    MDB_DATABASE=nom de la db mongodb
    

./dockerdo stop

./dockerdo start

Important : Après avoir importé la base de données, remplacer les email des utilisateurs et supprimer les firebase token :

UPDATE users SET email = CONCAT('basile.melchior+', id, '@charlie-solutions.com'), firebaseToken = '' WHERE email NOT IN ('administrateur-charlie@charlie-solutions.com', 'technical@charlie-solutions.com')

Se mettre dev :

Lancer les commandes du sprint (migrate / seeder / meilisetup)