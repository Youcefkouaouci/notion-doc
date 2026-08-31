# Post action - A MAJ

## 🚛 Zones

### 🆕 Created :

- Before create
    1. Si il renseigne une adresse, récupérer sa longitude et latitude
        
        Si il renseigne juste une localisation (coordonnée gps) : faire du géocoding pour récupérer l’adresse.
        
    2. Géofencing sur le site
        
        Dès qu’une adresse/géolocalisation est ajoutée, même si il renseigne un site (c’est le site géofencé qui prime)
        
- After Create
    1. Créer sa localisation
    2. Mettre à jour le status du capteur/tracker

### 💡 Updated :

- Before update
    1. Si l’adresse change, récupérer sa longitude et latitude
        
        Si il renseigne juste une localisation (coordonnée gps) : faire du géocoding pour récupérer l’adresse.
        
    2. Géofencing sur le site
        
        Dès qu’une adresse/géolocalisation est ajoutée, même si il renseigne un site (c’est le site géofencé qui prime)
        
- After update
    1. Update sa localisation
    2. Mettre à jour le status du capteur/tracker

### 🗑️ Deleted :

- After Deleted
    1. Mettre à jour le status du capteur/tracker

## 🔨 Materiels

### 🆕 Created :

- Before create
    1. Si il renseigne une adresse, récupérer sa longitude et latitude
        
        Si il renseigne juste une localisation (coordonnée gps) : faire du géocoding pour récupérer l’adresse.
        
    2. Géofencing sur le site
        
        Dès qu’une adresse/géolocalisation est ajoutée, même si il renseigne un site (c’est le site géofencé qui prime)
        
- After Create
    1. Mettre à jour le status du capteur/tracker

### 💡 Updated :

- Before update
    1. Si l’adresse change, récupérer sa longitude et latitude
        
        Si il renseigne juste une localisation (coordonnée gps) : faire du géocoding pour récupérer l’adresse.
        
    2. Géofencing sur le site
        
        Dès qu’une adresse/géolocalisation est ajoutée, même si il renseigne un site (c’est le site géofencé qui prime)
        
- After update
    1. Mettre à jour le status du capteur/tracker

### 🗑️ Deleted :

- After Deleted
    1. Mettre à jour le status du capteur/tracker

## 📯 Capteurs

### 🆕 Created :

- After Create
    1. Plateforme interne, Créer le capteur sur la plateforme interne (si besoin) et l’associer au client
        
        ❗Le faire dans un job
        

### 💡 Updated :

- After update
    1. Envoyer la battery à la plateforme interne lorsqu’elle change
        
        ❗Le faire dans un job
        
    2. Envoyer le nouveau status du capteur à la plateforme interne lorsqu’il change
        
        ❗Le faire dans un job
        

### 🗑️ Deleted :

- After Deleted
    1. Plateforme interne, Désassocier le capteur au client + update de son statut
        
        ❗Le faire dans un job
        

## 📯 Trackers

### 🆕 Created :

- After Create
    1. Plateforme interne, Créer le tracker sur la plateforme interne (si besoin) et l’associer au client
        
        ❗Le faire dans un job
        

### 💡 Updated :

- After update
    1. Envoyer la battery à la plateforme interne lorsqu’elle change
        
        ❗Le faire dans un job
        
    2. Envoyer le nouveau status du tracker à la plateforme interne lorsqu’il change
        
        ❗Le faire dans un job
        

### 🗑️ Deleted :

- After Deleted
    1. Plateforme interne, Désassocier le tracker au client + update de sion statut
        
        ❗Le faire dans un job