# Serveur MQTT - A MAJ

## Installer mosquitto

## Lancer le serveur mqtt

1. Créer le fichier **mqtt-listen.service** dans le dossier **/etc/systemd/system**
    
    ```
    [Unit]
    Description=Laravel mqtt listen
    
    [Service]
    User=www-data
    Group=www-data
    Restart=always
    ExecStart=/var/www/Charlie_platform/dockerdo art mqtt:listen
    WorkingDirectory=/var/www/Charlie_platform
    Environment=QUEUE_CONNECTION=database
    
    [Install]
    WantedBy=multi-user.target
    ```
    
2. sudo systemctl daemon-reload
3. sudo systemctl restart mqtt-listen
4. sudo systemctl status mqtt-listen
    1. Vérifier que le system est bien **active**

**⚠️ EN CAS DE MODIFICATION DU SCRIPT MQTT, IL FAUT RELANCER : REPARTIR DE L’ÉTAPE 3**

## Laravel queue

1. sudo systemctl restart laravel-queue
2. sudo systemctl status laravel-queue
    1. Vérifier que le system est bien **active**

## Installer cron

1. sudo crontab -e
2. Coller le script suivant

```
* * * * * sudo bash -c "cd /var/www/Charlie_platform && ./dockerdo art schedule:run >> /dev/null 2>&1"
```