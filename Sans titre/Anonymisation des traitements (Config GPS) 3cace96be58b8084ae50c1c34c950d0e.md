# Anonymisation des traitements (Config GPS)

Pour tous les types d’inventaire, pour chaque zone, si le temps de l’inventaire se trouve dans une configuration gps active de la zone, on met la latitude et longitude de la zone à null

Pour les inventaires GT (MQTT GT TRACKER, MQTT GT SENSOR, CONNECT GT, PHONE GT,  PHONE CONNECT GT)

Si la zone devant être anonymisée est liée à un tracker, OU si la zone devant être anonymisée est la seule zone de l’inventaire, on met la latitude et la longitude de tous les capteurs à null